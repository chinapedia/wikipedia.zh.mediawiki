-------------------------------------------------------------------------
-- This is a table of sites that are available through interwiki links --
-- from Wikipedia. It can be accessed from Lua via the mw.loadData()   --
-- function. It is currently used in [[Module:UrlToWiki|Module:UrlToWiki]] and          --
-- [[Module:UserLinks|Module:UserLinks]]. Feel free to add to its functionality and to  --
-- include new sites.                                                  --
-------------------------------------------------------------------------
 
-- Example entry:
 
--  wikipedia = {                               -- This is a code that you can use to easily identify the project in the table.
--      domain            = "wikipedia.org",    -- The base domain name of the website, without any language codes.
--      domain_primary    = true                -- Whether this is the primary entry for the domain.
--      iw_prefix         = {"w", "wikipedia"}, -- A table of valid interwiki prefixes for the site. See [[Help:Interwiki_linking|Help:Interwiki linking]].
--      title_prefix      = "/wiki/",           -- The text between the domain name and the project's article titles.
--      takes_lang_prefix = true                -- Whether the project has separate subdomains for different languages, e.g. es.wikipedia.org
--  },
 
interwiki_table = {
 
------------------------
-- Wikimedia projects --
------------------------
 
    wikipedia = {
        domain            = "wikipedia.org",
        domain_primary    = true,
        iw_prefix         = {"w", "wikipedia"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wiktionary = {
        domain            = "wiktionary.org",
        domain_primary    = true,
        iw_prefix         = {"wikt", "wiktionary"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wikinews = {
        domain            = "wikinews.org",
        domain_primary    = true,
        iw_prefix         = {"n", "wikinews"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wikibooks = {
        domain            = "wikibooks.org",
        domain_primary    = true,
        iw_prefix         = {"b", "wikibooks"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wikiquote = {
        domain            = "wikiquote.org",
        domain_primary    = true,
        iw_prefix         = {"q", "wikiquote"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wikisource = {
        domain            = "wikisource.org",
        domain_primary    = true,
        iw_prefix         = {"s", "wikisource"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wikispecies = {
        domain            = "species.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"species", "wikispecies"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikiversity = {
        domain            = "wikiversity.org",
        domain_primary    = true,
        iw_prefix         = {"v", "wikiversity"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wikivoyage = {
        domain            = "wikivoyage.org",
        domain_primary    = true,
        iw_prefix         = {"voy", "wikivoyage"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = true
    },
    wmf = {
        domain            = "wikimediafoundation.org",
        domain_primary    = true,
        iw_prefix         = {"wmf", "wikimedia", "foundation"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    commons = {
        domain            = "commons.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"commons"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikidata = {
        domain            = "wikidata.org",
        domain_primary    = true,
        iw_prefix         = {"d", "wikidata"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    meta = {
        domain = "meta.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"m", "metawikipedia", "meta"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    mediawiki = {
        domain = "mediawiki.org",
        domain_primary    = true,
        iw_prefix         = {"mw", "mediawikiwiki"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
 
------------------------
-- Wikimedia chapters --
------------------------
 
    wmar = {
        domain            = "wikimedia.org.ar",
        domain_primary    = true,
        iw_prefix         = {"wmar"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmau = {
        domain            = "wikimedia.org.au",
        domain_primary    = true,
        iw_prefix         = {"wmau"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmbd = {
        domain            = "bd.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmbd"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmbe = {
        domain            = "be.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmbe"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmca = {
        domain            = "wikimedia.ca",
        domain_primary    = true,
        iw_prefix         = {"wmca"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmde = {
        domain            = "wikimedia.de",
        domain_primary    = true,
        iw_prefix         = {"wmde"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmfi = {
        domain            = "fi.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmfi"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmhk = {
        domain            = "wikimedia.hk",
        domain_primary    = true,
        iw_prefix         = {"wmhk"},
        title_prefix      = "/index.php/",
        takes_lang_prefix = false
    },
    wmhu = {
        domain            = "wikimedia.hu",
        domain_primary    = true,
        iw_prefix         = {"wmhu"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmin = {
        domain            = "wiki.wikimedia.in",
        domain_primary    = true,
        iw_prefix         = {"wmin"},
        title_prefix      = "/",
        takes_lang_prefix = false
    },
    wmid = {
        domain            = "wikimedia.or.id",
        domain_primary    = true,
        iw_prefix         = {"wmid"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmil = {
        domain            = "wikimedia.org.il",
        domain_primary    = true,
        iw_prefix         = {"wmil"},
        title_prefix      = "/",
        takes_lang_prefix = false
    },
    wmit = {
        domain            = "wikimedia.it",
        domain_primary    = true,
        iw_prefix         = {"wmit"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmnl = {
        domain            = "nl.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmnl"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmno = {
        domain            = "no.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmno"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmpl = {
        domain            = "pl.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmpl"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmru = {
        domain            = "ru.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmru"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmrs = {
        domain            = "rs.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmrs"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmse = {
        domain            = "se.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmse"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wmch = {
        domain            = "wikimedia.ch",
        domain_primary    = true,
        iw_prefix         = {"wmch"},
        title_prefix      = "/",
        takes_lang_prefix = false
    },
    wmtw = {
        domain            = "tw.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmtw"},
        title_prefix      = "/wiki/index.php5/",
        takes_lang_prefix = false
    },
    wmuk = {
        domain            = "uk.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wmuk"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
 
---------------
-- Wikimania --
---------------
 
    wikimania2005 = {
        domain            = "wikimania2005.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2005"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2006 = {
        domain            = "wikimania2006.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2006"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2007 = {
        domain            = "wikimania2007.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2007"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2008 = {
        domain            = "wikimania2008.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2008"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2009 = {
        domain            = "wikimania2009.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2009"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2010 = {
        domain            = "wikimania2010.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2010"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2011 = {
        domain            = "wikimania2011.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2011"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2012 = {
        domain            = "wikimania2012.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2012"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2013 = {
        domain            = "wikimania2013.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2013", "wmania"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    wikimania2014 = {
        domain            = "wikimania2014.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"wm2014"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
 
---------------------------
-- Other Wikimedia wikis --
---------------------------
 
    betawikiversity = {
        domain            = "beta.wikiversity.org",
        domain_primary    = true,
        iw_prefix         = {"betawikiversity"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    outreach = {
        domain            = "outreach.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"outreach"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    otrswiki = {
        domain            = "otrs-wiki.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"OTRSwiki"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    quality = {
        domain            = "quality.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"quality"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    spcom = {
        domain            = "spcom.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"spcom"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    spcom = {
        domain            = "spcom.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"spcom"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    tswiki = {
        domain            = "wiki.toolserver.org",
        domain_primary    = true,
        iw_prefix         = {"tswiki"},
        title_prefix      = "/view/",
        takes_lang_prefix = false
    },
    incubator = {
        domain            = "incubator.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"incubator"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    strategy = {
        domain            = "strategy.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"strategy"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    rev = {
        domain            = "www.mediawiki.org",
        domain_primary    = false,
        iw_prefix         = {"rev"},
        title_prefix      = "/wiki/Special:Code/MediaWiki/",
        takes_lang_prefix = false
    },
    test = {
        domain            = "test.wikipedia.org",
        domain_primary    = true,
        iw_prefix         = {"testwiki"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
    test2 = {
        domain            = "test2.wikipedia.org",
        domain_primary    = true,
        iw_prefix         = {"test2wiki"},
        title_prefix      = "/wiki/",
        takes_lang_prefix = false
    },
 
------------------------------
-- Wikimedia non-wiki sites --
------------------------------
 
    bugzilla = {
        domain            = "bugzilla.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"bugzilla", "mediazilla"},
        title_prefix      = "/show_bug.cgi?id=",
        takes_lang_prefix = false
    },
    download = {
        domain            = "dumps.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"download"},
        title_prefix      = "/",
        takes_lang_prefix = false
    },
    gerrit = {
        domain            = "gerrit.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"gerrit"},
        title_prefix      = "/r/#/c/",
        takes_lang_prefix = false
    },
    mail = {
        domain            = "lists.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"mail"},
        title_prefix      = "/mailman/listinfo/",
        takes_lang_prefix = false
    },
    mailarchive = {
        domain            = "lists.wikimedia.org",
        domain_primary    = false,
        iw_prefix         = {"mailarchive"},
        title_prefix      = "/pipermail/",
        takes_lang_prefix = false
    },
    otrs = {
        domain            = "ticket.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"otrs", "ticket"},
        title_prefix      = "/otrs/index.pl?Action=AgentTicketZoom&TicketID=",
        takes_lang_prefix = false
    },
    toolserver = {
        domain            = "toolserver.org",
        domain_primary    = true,
        iw_prefix         = {"tools"},
        title_prefix      = "/",
        takes_lang_prefix = false
    },
    sulutil = {
        domain            = "toolserver.org",
        domain_primary    = true,
        iw_prefix         = {"sulutil"},
        title_prefix      = "/~quentinv57/sulinfo/",
        takes_lang_prefix = false
    },
    svn = {
        domain            = "svn.wikimedia.org",
        domain_primary    = true,
        iw_prefix         = {"svn"},
        title_prefix      = "/viewvc/mediawiki/",
        takes_lang_prefix = false
    }
}
 
return interwiki_table