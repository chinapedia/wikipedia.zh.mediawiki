local retval = {
	main_box_raw_auto_width = 'border-spacing:2px;',
    box_label = 'text-align:left; font-size:small; line-height:1.5em;',
	header_raw = 'background-color:#B0C4DE;text-align:center;vertical-align:middle;font-size:90%;',
	sub_header_raw = 'background-color:#DCDCDC;text-align:center;vertical-align:middle;font-size:85%;',
	header_color = 'background-color:#B0C4DE;',
	nav_box = 'margin:0;float:right;clear:right;width:315px;margin-bottom:0.5em;margin-left:1em;',
	nav_box_child = 'margin:0;float:right;clear:right;width:305px;margin-bottom:0.5em;',
	nav_box_wide =  '',
	nav_box_header = 'background-color:#B0C4DE;',
	nav_box_wide_header = 'background-color:#B0C4DE;',
	nav_box_label = 'background-color:#DCDCDC;',
	image_box_raw = 'text-align:center;border-bottom:1px solid #aaa;line-height:1.5em;font-size:85%;',
	image_box_plain_raw = 'text-align:center;line-height:1.5em;font-size:85%;',
	internal_border = '1px dotted #aaa;font-size:85%;',
	section_border = '1px solid #aaa;font-size:85%;'
}

retval.main_box_raw = 'width:315px;' .. retval.main_box_raw_auto_width
retval.header_bar = 'style="' .. retval.header_raw .. '"'
retval.sub_header_bar = 'style="' .. retval.sub_header_raw .. '"'
retval.image_box = 'style="' .. retval.image_box_raw .. '"'
retval.image_box_plain = 'style="' .. retval.image_box_plain_raw .. '"'

return retval