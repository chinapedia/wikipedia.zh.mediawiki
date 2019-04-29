---- This module is meant to allow the goodies listed in
---- http://www.mediawiki.org/wiki/Extension:Scribunto/Lua_reference_manual#Title_objects
---- to be accessed by people who don't want to program a Lua module.
---- Usage is:  {{#invoke:Page|(function)|parameters}}
---- (function) is one of the function names from the table above:
---- id, interwiki, namespace, fragment, nsText, subjectNsText, text, prefixedText, fullText ...

---- parameters are:
---- page = (name of page to load; leave blank to call mw.title.getCurrentTitle()
----    this is "text" passed to mw.title.new or "title" passed to mw.title.makeTitle
---- makeTitle = nonblank to call mw.title.makeTitle otherwise mw.title.new is called
---- namespace = (parameter passed to new/makeTitle)
---- fragment = (parameter passed to makeTitle)
---- interwiki = (parameter passed to makeTitle)
---- p1 = first parameter passed to functions within the title object
---- p2 = second parameter " " " "
---- p3 etc. (for inNamespaces)

function main(frame, field)
    local args, pargs = frame.args, ( frame:getParent() or {} ).args or {};
    local makeTitle=args.makeTitle or pargs.makeTitle or "";
    local namespace=args.namespace or pargs.namespace or "";
    local fragment=args.fragment or pargs.fragment or "";
    local interwiki=args.interwiki or pargs.interwiki or "";
    local nowiki=args.nowiki or pargs.nowiki or false;
    local page=args.page or args[1] or pargs.page or pargs[1] or "";
    local id= tonumber( args.id or pargs.id );
    local pn = {};
    local title -- holds the result of the mw.title.xxx call
    
    for i = 1,9 do pn[i] = args['p'..i] or pargs['p'..i]; end
    if not id and not mw.ustring.match( page, '%S' ) then page = nil; end
    
    if id then
        title = mw.title.new(id);
        if not title then return "error: failed to mw.title.new(" .. id .. ")"; end
    elseif not page then
        title = mw.title.getCurrentTitle();
        if not title then return "error: failed to getCurrentTitle()"; end
    elseif makeTitle then
        title = mw.title.makeTitle(namespace, page, fragment, interwiki);
        if not title then
            return mw.ustring.format("error: failed to makeTitle(%s,%s,%s,%s)", namespace, page, fragment, interwiki);
        end
    else
        title=mw.title.new(page, namespace);
        if not title then return "error: failed to mw.title.new(" .. page .. "," .. namespace .. ")"; end
    end
    
    local result, success = title[field];
    if type(result) == "function" then
        success, result = pcall( result, title, unpack(pn) );
        if not success then
            return mw.ustring.format("error: failed to title:%s(%s)", field, table.concat(pn, ',' ));
        end
    end
    if nowiki and result ~= nil then
        return mw.text.nowiki( tostring( result ) );
    else
        return tostring(result or "");
    end
end

local p = {};

-- main function does all the work
function p.id(frame) return main(frame, "id"); end
function p.interwiki(frame) return main(frame, "interwiki"); end
function p.namespace(frame) return main(frame, "namespace"); end
function p.fragment(frame) return main(frame, "fragment"); end
function p.nsText(frame) return main(frame, "nsText") end
function p.subjectNsText(frame) return main(frame, "subjectNsText"); end
function p.text(frame) return main(frame, "text"); end
function p.prefixedText(frame) return main(frame, "prefixedText"); end
function p.fullText(frame) return main(frame, "fullText"); end
function p.rootText(frame) return main(frame, "rootText"); end
function p.baseText(frame) return main(frame, "baseText"); end
function p.subpageText(frame) return main(frame, "subpageText"); end
function p.canTalk(frame) return main(frame, "canTalk"); end
function p.exists(frame) return main(frame, "exists"); end
function p.fileExists(frame) return main(frame, "fileExists"); end
function p.isContentPage(frame) return main(frame, "isContentPage"); end
function p.isExternal(frame) return main(frame, "isExternal"); end
function p.isLocal(frame) return main(frame, "isLocal"); end
function p.isRedirect(frame) return main(frame, "isRedirect"); end
function p.isSpecialPage(frame) return main(frame, "isSpecialPage"); end
function p.isSubpage(frame) return main(frame, "isSubpage"); end
function p.isTalkPage(frame) return main(frame, "isTalkPage"); end
function p.isSubpageOf(frame) return main(frame, "isSubpageOf"); end
function p.inNamespace(frame) return main(frame, "inNamespace"); end
function p.inNamespaces(frame) return main(frame, "inNamespaces"); end
function p.hasSubjectNamespace(frame) return main(frame, "hasSubjectNamespace"); end
function p.contentModel(frame) return main(frame, "contentModel"); end
function p.basePageTitle(frame) return main(frame, "basePageTitle"); end
function p.rootPageTitle(frame) return main(frame, "rootPageTitle"); end
function p.talkPageTitle(frame) return main(frame, "talkPageTitle"); end
function p.subjectPageTitle(frame) return main(frame, "subjectPageTitle"); end
function p.subPageTitle(frame) return main(frame, "subPageTitle"); end
function p.partialUrl(frame) return main(frame, "partialUrl"); end
function p.fullUrl(frame) return main(frame, "fullUrl"); end
function p.localUrl(frame) return main(frame, "localUrl"); end
function p.canonicalUrl(frame) return main(frame, "canonicalUrl"); end
function p.getContent(frame) return main(frame, "getContent"); end

return p