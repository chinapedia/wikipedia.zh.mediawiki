local p = {}

function p.titleToJson(title) 
-- Load mediawiki page and decodes it as json 
	local t = mw.title.new(title) 
	if not t.exists then 
		return nil 
	else 
		return mw.text.jsonDecode(t:getContent(), mw.text.JSON_TRY_FIXING) 
	end 
end

function p.MISSING(frame)
	data = p.titleToJson(frame.args.data);
	args1 = frame.args[1];
	init = data[args1][frame.args[2]];
	if frame.args[2] then
		inittext = string.format('初始值：%d', init);
	end
	if frame.args[3] then
		redlinks = data[args1][frame.args[3]];
		done = (init - redlinks) / init *100;
		done= done-done%0.1;
		donetext = '；'..done..'%完成';
	end
	if donetext then
		text = inittext..donetext;
	else
		text = inittext;
	end
	return text
end

function p.bar(frame)
	data = p.titleToJson(frame.args.data);
	args1 = frame.args[1];
	init = data[args1][frame.args[2]];
	redlinks = data[args1][frame.args[3]];
	done = (init - redlinks) / init *100;
	done= done-done%0.1;
	return done	
end

function p.total(frame)
	data = p.titleToJson(frame.args.data);
	local redlinks = 0;
	local inittotal =0;
	for key, cont in pairs(data) do 
		redlinks = redlinks+ cont[frame.args[2]];
		inittotal = inittotal+cont[frame.args[1]];
	end
	inittotaltext = string.format('初始值：%d', inittotal);
	totaldone = (inittotal - redlinks) / inittotal *100;
	totaldone= totaldone-totaldone%0.1;
	totaldonetext = '；'..totaldone..'%完成';
	return inittotaltext..totaldonetext
end

function p.totalbar(frame)
	data = p.titleToJson(frame.args.data);
	local redlinks = 0;
	local inittotal =0;
	for key, cont in pairs(data) do 
		redlinks = redlinks+ cont[frame.args[2]];
		inittotal = inittotal+cont[frame.args[1]];
	end
	totaldone = (inittotal - redlinks) / inittotal *100;
	totaldone= totaldone-totaldone%0.1;
	return totaldone
end

return p