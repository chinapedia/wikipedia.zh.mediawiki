-- This module is specifically the Wikidata property "prevalence" (P1193), due
-- to its particular need for ranges and area-based qualifiers, and the lack of
-- support for these in the main Wikidata module.

-- Completely untested.
local p = {}

--local wikidata = require( 'Module:Wikidata' )

p.main = function ( frame )
	--local entity = mw.wikibase.getEntity( 'Q133087' )
	local entity = mw.wikibase.getEntity( frame.args.qId or nil )
	if entity then
		local prevalenceClaims = entity.claims and entity.claims.P1193
		-- TODO: Get best claim, not always just the first one.
		-- Probably use getBestStatements.
		if prevalenceClaims then
			local pRange = ''
			-- Run through all prevalence claims
			for i, prevalenceClaim in pairs( prevalenceClaims ) do
				local prevalenceValue = prevalenceClaim.mainsnak.datavalue.value
				if prevalenceValue then
					if string.len( pRange ) > 0 then
						-- Split multiple claims
						-- Maybe line break instead?
						pRange = pRange .. ', '
					end
					local lowerBound = prevalenceValue.lowerBound * 100
					local upperBound = prevalenceValue.upperBound * 100
					pRange = pRange .. lowerBound
					if lowerBound ~= upperBound then
						pRange = pRange .. ' to ' .. upperBound
					end
					
					pRange = pRange .. '%'
					if prevalenceClaim.qualifiers then
						-- Qualifiers for prevalence are currently unstandardized.
						-- Keep guessing until the right one is found.
						local quals = prevalenceClaim.qualifiers.P276 or -- location
							prevalenceClaim.qualifiers.P1001 or          -- applies to jurisdiction
							prevalenceClaim.qualifiers.P17               -- country
						if quals then
							pRange = pRange .. ' ('
							for k, qual in pairs(quals) do
								if k > 1 then
									pRange = pRange .. ', '
								end
								local qualId = qual.datavalue.value[ 'numeric-id' ]
								local link = mw.wikibase.sitelink( 'Q' .. qualId )
								local label = ({
									-- Certain geographic locales might need a
									-- manual-ish override for labels. 
									[ 132453 ] = 'developed world'
								})[ qualId ] or mw.wikibase.label( 'Q' .. qualId )
								if link then
									label = '[['_.._link_.._'|' .. label .. ']]'
								end
								pRange = pRange .. label
								
							end
							pRange = pRange .. ')'
						end
					end
				end
				--[[
				-- Todo: References
				if prevalenceClaim.references then 
					
				end
				]]--
				
			end
			return pRange
		end
	end
	return ''
end

return p