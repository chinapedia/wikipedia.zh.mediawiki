--
-- This module will implement {{Testcase table}}
--
local p = {}

function p.testcase(frame)
	local args = frame:getParent().args
	local basepagename = mw.ustring.gsub(mw.title.getCurrentTitle().text, '/.*$', '');
	local tableclass = ''
	local tablestyle = ''
	local template1 = args['_template1'] or args['_template'] or (basepagename)
	local template2 = args['_template2'] or (template1 .. '/sandbox')
	local template3 = args['_template3']
	local heading1 = args['_heading1'] or '{{[[Template:'_.._template1_.._'|' .. template1 ..']]}}'
	local heading2 = args['_heading2'] or '{{[[Template:'_.._template2_.._'|' .. template2 ..']]}}'
	local heading3 = args['_heading3'] or (template3 and '{{[[Template:'_.._template3_.._'|' .. template3 ..']]}}')
	local heading0 = ''
	local rowheader = ''
	local after = args['_after'] or ''
	local caption = args['_caption'] or '並排比較'
	local t = {}
	
	if( args['_rowheader'] ) then
		rowheader = '<th scope=row>' .. args['_rowheader'] .. '</th>'
		heading0 = '<th>' .. (args['_heading0'] or '') .. '</th>'
	end
	if( args['_class'] ) then
		tableclass = ' class="' .. args['_class'] .. '"'
	end
	if( args['_style'] ) then
		tablestyle = ' style="' .. args['_style'] .. '"'
	end
	for k, v in pairs(args) do
		t[k] = v
	end
	local expanded1 = frame:expandTemplate{ title = template1, args = t }
	if args._resetRefs then
		frame:extensionTag('references')
	end
	local expanded2 = frame:expandTemplate{ title = template2, args = t }
	if (template3) then
		if args._resetRefs then
			frame:extensionTag('references')
		end
		local expanded3 = frame:expandTemplate{ title = template3, args = t }
   	    return mw.ustring.format( [==[
<table%s%s><caption>%s</caption>
<tr>%s<th style="width:33%%">%s</th><th style="width:33%%">%s</th><th style="width:33%%">%s</th></tr>
<tr style="vertical-align:top">%s<td>
%s%s</td><td>
%s%s</td><td>
%s%s</td></tr></table>]==],
		tableclass, tablestyle, caption,
		heading0, heading1, heading2, heading3, rowheader,
		expanded1, after,
		expanded2, after,
		expanded3, after
        )
	else
		return mw.ustring.format( [==[
<table%s%s><caption>%s</caption>
<tr>%s<th style="width:50%%">%s</th><th style="width:50%%">%s</th></tr>
<tr style="vertical-align:top">%s<td>
%s%s</td><td>
%s%s</td></tr></table>]==],
		tableclass, tablestyle, caption,
		heading0, heading1, heading2, rowheader,
		expanded1, after,
		expanded2, after
	)
	end
end

return p