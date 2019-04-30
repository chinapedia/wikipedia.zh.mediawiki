-- This module implements [[Template:Tracklist|Template:Tracklist]]

local yesno = require('Module:Yesno')
local checkType = require('libraryUtil').checkType

local SHOW_WARNINGS = false
local INPUT_ERROR_CATEGORY = '输入错误的曲目表'

--------------------------------------------------------------------------------
-- Helper functions
--------------------------------------------------------------------------------

-- Add a mixin to a class.
local function addMixin(class, mixin)
	for k, v in pairs(mixin) do
		if k ~= 'init' then
			class[k] = v
		end
	end
end

--------------------------------------------------------------------------------
-- Validation mixin
--------------------------------------------------------------------------------

local Validation = {}

function Validation.init(self)
	self.warnings = {}
	self.categories = {}
end

function Validation:addWarning(msg, category)
	table.insert(self.warnings, msg)
	table.insert(self.categories, category)
end

function Validation:addCategory(category)
	table.insert(self.categories, category)
end

function Validation:getWarnings()
	return self.warnings
end

function Validation:getCategories()
	return self.categories
end

-- Validate a track length. If a track length is invalid, a warning is added.
-- A type error is raised if the length is not of type string or nil.
function Validation:validateLength(length)
	checkType('validateLength', 1, length, 'string', true)
	if length == nil then
		-- Do nothing if no length specified
		return nil
	end

	local hours, minutes, seconds

	-- Try to match times like "1:23:45".
	hours, minutes, seconds = length:match('^(%d+):(%d%d):(%d%d)$')
	if hours and hours:sub(1, 1) == '0' then
		-- Disallow times like "0:12:34"
		self:addWarning(string.format(
			"无效时间'%s'（时间格式'h:mm:ss'不能以零开头）",
			mw.text.nowiki(length)
		), INPUT_ERROR_CATEGORY)
		return nil
	end

	if not seconds then
		-- The previous attempt didn't match. Try to match times like "1:23".
		minutes, seconds = length:match('^(%d?%d):(%d%d)$')
		if minutes and minutes:find('^0%d$') then
			-- Special case to disallow lengths like "01:23". This check has to
			-- be here so that lengths like "1:01:23" are still allowed.
			self:addWarning(string.format(
				"无效时间'%s'（时间格式'mm:ss'不能以零开头）",
				mw.text.nowiki(length)
			), INPUT_ERROR_CATEGORY)
			return nil
		end
	end

	-- Add a warning and return if we did not find a match.
	if not seconds then
		self:addWarning(string.format(
			"无效时间'%s'（时间格式必须为'm:ss'、'mm:ss'或'h:mm:ss'）",
			mw.text.nowiki(length)
		), INPUT_ERROR_CATEGORY)
		return nil
	end

	-- Check that the minutes are less than 60 if we have an hours field.
	if hours and tonumber(minutes) >= 60 then
		self:addWarning(string.format(
			"无效时长'%s'（如果指定了小时数，则分钟数必须小于60）",
			mw.text.nowiki(length)
		), INPUT_ERROR_CATEGORY)
		return nil
	end
	
	-- Check that the seconds are less than 60
	if tonumber(seconds) >= 60 then
		self:addWarning(string.format(
			"无效时长'%s'（秒数必须小于60）",
			mw.text.nowiki(length)
		), INPUT_ERROR_CATEGORY)
	end

	return nil
end

--------------------------------------------------------------------------------
-- Track class
--------------------------------------------------------------------------------

local Track = {}
Track.__index = Track
addMixin(Track, Validation)

Track.fields = {
	number = true,
	title = true,
	note = true,
	lyrics = true,
	music = true,
	writer = true,
	arranger = true,
	producer = true,
	extra = true,
	longnote = true,
	length = true,
}

Track.cellMethods = {
	number = 'makeNumberCell',
	title = 'makeTitleCell',
	writer = 'makeWriterCell',
	lyrics = 'makeLyricsCell',
	music = 'makeMusicCell',
	arranger = 'makeArrangerCell',
	producer = 'makeProducerCell',
	extra = 'makeExtraCell',
	longnote = 'makeLongNoteCell',
	length = 'makeLengthCell',
}

function Track.new(data)
	local self = setmetatable({}, Track)
	Validation.init(self)
	for field in pairs(Track.fields) do
		self[field] = data[field]
	end
	self.number = assert(tonumber(self.number))
	self:validateLength(self.length)
	return self
end

function Track:getLyricsCredit()
	return self.lyrics
end

function Track:getMusicCredit()
	return self.music
end

function Track:getWriterCredit()
	return self.writer
end

function Track:getArrangerCredit()
	return self.arranger
end

function Track:getProducerCredit()
	return self.producer
end

function Track:getExtraField()
	return self.extra
end

function Track:getLongNoteField()
	return self.longnote
end

function Track:getLengthField()
	return self.length
end

-- Note: called with single dot syntax
function Track.makeSimpleCell(wikitext)
	return mw.html.create('td')
		:css('vertical-align', 'top')
		:wikitext(wikitext or ' ')
end

function Track:makeNumberCell()
	return mw.html.create('td')
		:css('padding-right', '10px')
		:css('text-align', 'right')
		:css('vertical-align', 'top')
		:wikitext(self.number .. '.')
end

function Track:makeTitleCell()
	local titleCell = mw.html.create('td')
	titleCell
		:css('vertical-align', 'top')
		:wikitext(self.title and string.format('%s', self.title) or '-{zh-hans:《;zh-hant:〈;}-无题-{zh-hans:》;zh-hant:〉;}-')
	if self.note then
		titleCell
			:tag('span')
				:css('font-size', '85%')
				:wikitext(string.format('（%s）', self.note))
	end
	return titleCell
end

function Track:makeWriterCell()
	return Track.makeSimpleCell(self.writer)
end

function Track:makeLyricsCell()
	return Track.makeSimpleCell(self.lyrics)
end

function Track:makeMusicCell()
	return Track.makeSimpleCell(self.music)
end

function Track:makeArrangerCell()
	return Track.makeSimpleCell(self.arranger)
end

function Track:makeProducerCell()
	return Track.makeSimpleCell(self.producer)
end

function Track:makeExtraCell()
	return Track.makeSimpleCell(self.extra)
end

function Track:makeLongNoteCell()
	local longnoteCell = mw.html.create('td')
	longnoteCell
		:css('vertical-align', 'top')
		:tag('span')
			:css('font-size', '85%')
			:wikitext(self.longnote or ' ')
	return longnoteCell
end

function Track:makeLengthCell()
	return mw.html.create('td')
		:css('padding-right', '10px')
		:css('text-align', 'right')
		:css('vertical-align', 'top')
		:wikitext(self.length or ' ')
end

function Track:exportRow(options)
	options = options or {}
	local columns = options.columns or {}
	local row = mw.html.create('tr')
	row:css('background-color', options.color or '#fff')
	for i, column in ipairs(columns) do
		local method = Track.cellMethods[column]
		if method then
			row:node(self[method](self))
		end
	end
	return row
end

--------------------------------------------------------------------------------
-- TrackListing class
--------------------------------------------------------------------------------

local TrackListing = {}
TrackListing.__index = TrackListing
addMixin(TrackListing, Validation)

TrackListing.fields = {
	all_position = true,
	all_writing = true,
	all_lyrics = true,
	all_music = true,
	all_arranger = true,
	all_producer = true,
	all_note = true,
	collapsed = true,
	headline = true,
	font_size = true,
	extra_column = true,
	total_length = true,
	title_width = true,
	writing_width = true,
	lyrics_width = true,
	music_width = true,
	arranger_width = true,
	producer_width = true,
	extra_width = true,
	longnote_width = true,
	category = true,
}

TrackListing.deprecatedFields = {
	writing_credits = true,
	lyrics_credits = true,
	music_credits = true,
	arranger_credits = true,
	producer_credits = true,
	longnote_column = true,
}

function TrackListing.new(data)
	local self = setmetatable({}, TrackListing)
	Validation.init(self)

	-- Check for deprecated arguments
	for deprecatedField in pairs(TrackListing.deprecatedFields) do
		if data[deprecatedField] then
			self:addCategory('使用废弃参数的曲目表')
			break
		end
	end

	-- Validate total length
	if data.total_length then
		self:validateLength(data.total_length)
	end
	
	-- Add properties
	for field in pairs(TrackListing.fields) do
		self[field] = data[field]
	end
	
	-- Evaluate boolean properties
	self.collapsed = yesno(self.collapsed, false)
	self.showCategories = yesno(self.category) ~= false
	self.category = nil

	-- Make track objects
	self.tracks = {}
	for i, trackData in ipairs(data.tracks or {}) do
		table.insert(self.tracks, Track.new(trackData))
	end

	-- Find which of the optional columns we have.
	-- We could just check every column for every track object, but that would
	-- be no fun^H^H^H^H^H^H inefficient, so we use four different strategies
	-- to try and check only as many columns and track objects as necessary.
	do
		local optionalColumns = {}
		local columnMethods = {
			lyrics = 'getLyricsCredit',
			music = 'getMusicCredit',
			writer = 'getWriterCredit',
			arranger = 'getArrangerCredit',
			producer = 'getProducerCredit',
			extra = 'getExtraField',
			longnote = 'getLongNoteField',
			length = 'getLengthField',
		}
		local doneWriterCheck = false
		for i, trackObj in ipairs(self.tracks) do
			for column, method in pairs(columnMethods) do
				if trackObj[method](trackObj) then
					optionalColumns[column] = true
					columnMethods[column] = nil
				end
			end
			if not doneWriterCheck and optionalColumns.writer then
				doneWriterCheck = true
				optionalColumns.lyrics = nil
				optionalColumns.music = nil
				columnMethods.lyrics = nil
				columnMethods.music = nil
			end
			if not next(columnMethods) then
				break
			end
		end
		self.optionalColumns = optionalColumns
	end

	return self
end

function TrackListing:makeIntro()
	local s = ''
		if self.all_writing then
			s = s .. string.format(
				'全碟词曲：%s　',
				self.all_writing
			)
		elseif self.all_lyrics and self.all_music then
			s = s .. string.format(
				'全碟-{zh-cn:作词;zh-hk:填詞;zh-tw:作詞;}-：%s　全碟作曲：%s　',
				self.all_lyrics,
				self.all_music
			)
		elseif self.all_lyrics then
			s = s .. string.format(
				'全碟-{zh-cn:作词;zh-hk:填詞;zh-tw:作詞;}-：%s　',
				self.all_lyrics
			)
		elseif self.all_music then
			s = s .. string.format(
				'全碟作曲：%s　',
				self.all_music
			)
		end
		if self.all_arranger then
			s = s .. string.format(
				'全碟编曲：%s　',
				self.all_arranger
			)
		end
		if self.all_producer then
			s = s .. string.format(
				'全碟监制：%s　',
				self.all_producer
			)
		end
		if self.all_note then
			if self.all_note == 'except' or yesno(self.all_note) == true then
				s = s .. string.format(
					'<small>（下面注明例外曲目）</small>'
				)
			else
				s = s .. string.format(
					'%s',
					self.all_note
				)
			end
		end
	return s
end

function TrackListing:renderTrackingCategories()
	if not self.showCategories or mw.title.getCurrentTitle().namespace ~= 0 then
		return ''
	end

	local ret = ''

	local function addCategory(cat)
		ret = ret .. string.format('[[Category:%s|Category:%s]]', cat)
	end

	for i, category in ipairs(self:getCategories()) do
		addCategory(category)
	end

	for i, track in ipairs(self.tracks) do
		for j, category in ipairs(track:getCategories()) do
			addCategory(category)
		end
	end

	return ret
end

function TrackListing:renderWarnings()
	if not SHOW_WARNINGS then
		return ''
	end

	local ret = {}

	local function addWarning(msg)
		table.insert(ret, string.format(
			'<strong class="error">曲目表错误：%s</strong>',
			msg
		))
	end

	for i, warning in ipairs(self:getWarnings()) do
		addWarning(warning)
	end

	for i, track in ipairs(self.tracks) do
		for j, warning in ipairs(track:getWarnings()) do
			addWarning(warning)
		end
	end

	return table.concat(ret, '<br>')
end

function TrackListing:__tostring()
	-- Find columns to output
	local columns = {'number', 'title'}
	if self.optionalColumns.writer then
		columns[#columns + 1] = 'writer'
	else
		if self.optionalColumns.lyrics then
			columns[#columns + 1] = 'lyrics'
		end
		if self.optionalColumns.music then
			columns[#columns + 1] = 'music'
		end
	end
	if self.optionalColumns.arranger then
		columns[#columns + 1] = 'arranger'
	end
	if self.optionalColumns.producer then
		columns[#columns + 1] = 'producer'
	end
	if self.optionalColumns.extra then
		columns[#columns + 1] = 'extra'
	end
	if self.optionalColumns.longnote then
		columns[#columns + 1] = 'longnote'
	end
	if self.optionalColumns.length then
		columns[#columns + 1] = 'length'
	end

	-- Find colspan and column width
	local nColumns = #columns
	local c = #columns
	if self.optionalColumns.longnote then
		c = c - 1
	end
	if self.optionalColumns.length then
		c = c - 1
	end
	local nOptionalColumns = c - 2
	local titleColumnWidth
	local longnoteColumnWidth
	if c >= 7 then
		if self.optionalColumns.longnote then
			titleColumnWidth = 20
			longnoteColumnWidth = 20
		else
			titleColumnWidth = 25
			longnoteColumnWidth = 0
		end
	elseif c >= 6 then
		if self.optionalColumns.longnote then
			titleColumnWidth = 20
			longnoteColumnWidth = 20
		else
			titleColumnWidth = 30
			longnoteColumnWidth = 0
		end
	elseif c >= 5 then
		if self.optionalColumns.longnote then
			titleColumnWidth = 25
			longnoteColumnWidth = 24
		else
			titleColumnWidth = 34
			longnoteColumnWidth = 0
		end
	elseif c >= 4 then
		if self.optionalColumns.longnote then
			titleColumnWidth = 25
			longnoteColumnWidth = 30
		else
			titleColumnWidth = 40
			longnoteColumnWidth = 0
		end
	elseif c >= 3 then
		if self.optionalColumns.longnote then
			titleColumnWidth = 30
			longnoteColumnWidth = 40
		else
			titleColumnWidth = 60
			longnoteColumnWidth = 0
		end
	else
		if self.optionalColumns.longnote then
			titleColumnWidth = 30
		else
			titleColumnWidth = 100
		end
		longnoteColumnWidth = 0
	end
	local optionalColumnWidth = (100 - titleColumnWidth - longnoteColumnWidth) / nOptionalColumns
	titleColumnWidth = titleColumnWidth .. '%'
	if longnoteColumnWidth ~= 0 then
		longnoteColumnWidth = longnoteColumnWidth .. '%'
	else
		longnoteColumnWidth = '40em'
	end
	optionalColumnWidth = optionalColumnWidth .. '%'

	-- Find intros
	local nIntros = 0
	if self.all_writing then
		nIntros = nIntros + 1
	else
		if self.all_lyrics then
			nIntros = nIntros + 1
		end
		if self.all_music then
			nIntros = nIntros + 1
		end
	end
	if self.all_arranger then
		nIntros = nIntros + 1
	end
	if self.all_producer then
		nIntros = nIntros + 1
	end
	if self.all_note then
		nIntros = nIntros + 1
	end

	-- Root of the output
	local root = mw.html.create()

	-- Intro (if above header)
	if nIntros ~= 0 and self.all_position ~= 'below' then
		root:tag('div')
			:css('padding-left', '1em')
			:node(self:makeIntro())
	end

	-- Start of track listing table
	local tableRoot = root:tag('table')
	tableRoot
		:addClass('tracklist')
		:addClass(self.collapsed and 'collapsible collapsed' or nil)
		:css('display', 'block')
		:css('border-spacing', '0px')
		:css('border-collapse', 'collapse')
		:css('font-size', self.font_size or '100%')
		:css('border', self.collapsed and '#aaa 1px solid' or nil)
		:css('padding', self.collapsed and '3px' or '4px')

	-- Header row
	if self.headline or self.collapsed then
		tableRoot:tag('tr'):tag('th')
			:addClass('tlheader mbox-text')
			:attr('colspan', nColumns)
			:css('text-align', 'left')
			:css('background-color', '#fff')
			:wikitext(self.headline or '曲目表')
	end

	-- Intro row (if below header)
	if nIntros ~= 0 and self.all_position == 'below' then
		tableRoot:tag('tr'):tag('th')
			:attr('colspan', nColumns)
			:css('padding-left', '2em')
			:css('text-align', 'left')
			:css('background-color', '#fff')
			:css('font-weight', 'normal')
			:node(self:makeIntro())
	end

	-- Headers
	local headerRow = tableRoot:tag('tr')

	---- Track number
	headerRow
		:tag('th')
			:addClass('tlheader')
			:attr('scope', 'col')
			:css('width', '2em')
			:css('padding-left', '10px')
			:css('padding-right', '10px')
			:css('text-align', 'right')
			:css('background-color', '#eee')
			:css('white-space', 'nowrap')
			:wikitext('曲序')

	---- Title
	headerRow:tag('th')
		:addClass('tlheader')
		:attr('scope', 'col')
		:css('width', self.title_width or titleColumnWidth)
		:css('text-align', 'left')
		:css('background-color', '#eee')
		:css('white-space', 'nowrap')
		:wikitext('曲目')

	---- Optional headers: writer, lyrics, music, arranger, producer and extra
	local function addOptionalHeader(field, headerText, width)
		if self.optionalColumns[field] then
			headerRow:tag('th')
				:addClass('tlheader')
				:attr('scope', 'col')
				:css('width', width or optionalColumnWidth)
				:css('text-align', 'left')
				:css('background-color', '#eee')
				:css('white-space', 'nowrap')
				:wikitext(headerText)
		end
	end
	addOptionalHeader('writer', '词曲', self.writing_width)
	addOptionalHeader('lyrics', '-{zh-cn:作词;zh-hk:填詞;zh-tw:作詞;}-', self.lyrics_width)
	addOptionalHeader('music', '作曲', self.music_width)
	addOptionalHeader('arranger', '编曲', self.arranger_width)
	addOptionalHeader('producer', '监制', self.producer_width)
	addOptionalHeader(
		'extra',
		self.extra_column or '{{{extra_column}}}',
		self.extra_width
	)

	---- Notes
	if self.optionalColumns['longnote'] then
		headerRow:tag('th')
			:addClass('tlheader')
			:attr('scope', 'col')
			:css('width', self.longnote_width or longnoteColumnWidth)
			:css('padding-right', '10px')
			:css('text-align', 'left')
			:css('background-color', '#eee')
			:css('white-space', 'nowrap')
			:wikitext('备注')
	end

	---- Track length
	if self.optionalColumns['length'] then
		headerRow:tag('th')
			:addClass('tlheader')
			:attr('scope', 'col')
			:css('width', '4em')
			:css('padding-right', '10px')
			:css('text-align', 'right')
			:css('background-color', '#eee')
			:css('white-space', 'nowrap')
			:wikitext('时长')
	end

	-- Tracks
	for i, track in ipairs(self.tracks) do
		tableRoot:node(track:exportRow({
			columns = columns,
			color = i % 2 == 0 and '#f7f7f7' or '#fff'
		}))
	end

	-- Total length
	if self.total_length then
		tableRoot
			:tag('tr')
				:tag('td')
					:attr('colspan', nColumns - 1)
					:css('padding', 0)
					:tag('span')
						:css('width', '4em')
						:css('float', 'right')
						:css('padding-left', '10px')
						:css('background-color', '#eee')
						:css('margin-right', '2px')
						:wikitext("'''总时长：'''")
						:done()
					:done()
				:tag('td')
					:css('padding', '0 10px 0 0')
					:css('text-align', 'right')
					:css('background-color', '#eee')
					:wikitext(string.format("'''%s'''", self.total_length))
	end
	
	-- Warnings and tracking categories
	root:wikitext(self:renderWarnings())
	root:wikitext(self:renderTrackingCategories())

	return tostring(root)
end

--------------------------------------------------------------------------------
-- Exports
--------------------------------------------------------------------------------

local p = {}

function p._main(args)
	-- Process numerical args so that we can iterate through them.
	local data, tracks = {}, {}
	for k, v in pairs(args) do
		if type(k) == 'string' then
			local prefix, num = k:match('^(%D.-)(%d+)$')
			if prefix and Track.fields[prefix] and (num == '0' or num:sub(1, 1) ~= '0') then
				-- Allow numbers like 0, 1, 2 ..., but not 00, 01, 02...,
				-- 000, 001, 002... etc.
				num = tonumber(num)
				tracks[num] = tracks[num] or {}
				tracks[num][prefix] = v
			else
				data[k] = v
			end
		end
	end
	data.tracks = (function (t)
		-- Compress sparse array
		local ret = {}
		for num, trackData in pairs(t) do
			trackData.number = num
			table.insert(ret, trackData) 
		end
		table.sort(ret, function (t1, t2)
			return t1.number < t2.number
		end)
		return ret
	end)(tracks)

	return tostring(TrackListing.new(data))
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = 'Template:Tracklist'
	})
	return p._main(args)
end

return p