--[[=========================================================================
Italicize a taxon name appropriately by invoking italicizeTaxonName.
The algorithm used is:
* If the name has italic markup at the start or the end, do nothing.
* Else
  * Remove (internal) italic markup.
  * If the name is made up of four words and the third word is a
    botanical connecting term, de-italicize the connecting term and add italic
    markup to the outside of the name.
  * Else if the name is made up of three words and the second word is a
    botanical connecting term or a variant of "cf.", de-italicize the
    connecting term and add italic markup to the outside of the name. 
  * Else just add italic markup to the outside of the name.
=============================================================================]]

local p = {}

local cTerms3 = {
	subspecies = "subsp.",
	["subsp."] = "subsp.",
	subsp = "subsp.",
	["ssp."] = "subsp.",
	ssp = "subsp.",
	varietas = "var.",
	["var."] = "var.",
	var = "var.",
	subvarietas = "subvar.",
	["subvar."] = "subvar.",
	subvar = "subvar.",
	forma = "f.",
	["f."] = "f.",
	f = "f.",
	subforma = "subf.",
	["subf."] = "subf.",
	subf = "subf."
	}
local cTerms2 = {
	subgenus = "subg.",
	["subg."] = "subg.",
	subg = "subg.",
	section = "sect.",
	["sect."] = "sect.",
	subsection ="subsect.",
	["subsect."] = "subsect.",
	series = "ser.",
	["ser."] = "ser.",
	subseries ="subser.",
	["subser."] = "subser.",
	["cf."] = "cf.",
	cf = "cf.",
	["c.f."] = "cf."
	}

--[[=========================================================================
Italicize a taxon name appropriately.
=============================================================================]]
function p.main(frame)
	local name = frame.args[1] or ''
	local linked = frame.args['linked'] == 'yes'
	return p.italicizeTaxonName(name, linked)
end

function p.italicizeTaxonName(name, linked)
	local italMarker = "''"
	-- trim the name and replace any use of the HTML italic tags by Wikimedia markup
	name = string.gsub(string.gsub(mw.text.trim(name), "<i>", italMarker), "</i>", italMarker)
	local result = name
	if name ~= '' then
		if string.sub(name, 1, 2) == "''" or string.sub(name, -2) == "''" then
			-- do nothing if the name already has italic markers at the start or end
		else
			name = string.gsub(name, "''", "") -- first remove internal italics
			local words = mw.text.split(name, " ", true)
			local deitalicized = false
			if #words == 4 then
				-- test for the third word of a four word name being a connecting term
				if cTerms3[words[3]] then
					-- de-italicize the connecting term by adding internal italic markup
					result = words[1] .. " " .. words[2] .. italMarker .. " " .. cTerms3[words[3]] .. italMarker .. " " .. words[4]
					deitalicized = true
				end
			elseif #words == 3 then
				-- test for the second word of a three word name being a connecting term
				if cTerms2[words[2]] then
					-- de-italicize the connecting term by adding internal italic markup
					result = words[1] .. " " .. italMarker .. cTerms2[words[2]] .. italMarker .. " " .. words[3]
					deitalicized = true
				end
			else
				-- do nothing
				result = name
			end
			-- add outside markup
			if linked then
				if deitalicized then
					result = "[["_.._name_.._"|" .. italMarker .. result .. italMarker .. "]]"
				else
					result = italMarker .. "[["_.._name_.._"|" .. name .. "]]" .. italMarker
				end
			else
				result = italMarker .. result .. italMarker
			end
		end
	end
	return result
end

return p