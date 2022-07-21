/*
You can import this gadget to other wikis by using mw.loader.load and specifying the local alias for Special:Contributions. For example:
var markblocked_contributions = 'Special:Contributions';
mw.loader.load('//en.wikipedia.org/w/index.php?title=MediaWiki:Gadget-markblocked.js&bcache=1&maxage=259200&action=raw&ctype=text/javascript');

This gadget will pull the user accounts and IPs from the history page and will strike out the users that are currently blocked.
 */
(function($, mw) {
	function markBlocked(container) {
		var contentLinks;

		// Collect all the links in the page's content
		if (container) {
			contentLinks = $(container).find('a');
		} else if (mw.util.$content) {
			contentLinks = mw.util.$content.find('a').add('#ca-nstab-user a');
		} else {
			contentLinks = $();
		}

		setCSS('\
			.user-blocked-temp {' + (window.mbTempStyle || 'opacity: 0.7; text-decoration: line-through') + '}\
			.user-blocked-indef {' + (window.mbIndefStyle || 'opacity: 0.4; font-style: italic; text-decoration: line-through') + '}\
			.user-blocked-partial {' + (window.mbPartialStyle || 'text-decoration: underline; text-decoration-style: dotted') + '}\
			.user-blocked-tipbox {' + (window.mbTipBoxStyle || 'font-size:smaller; background:#FFFFF0; border:1px solid #FEA; padding:0 0.3em; color:#AAA') + '}\
			', 'markBlockedStyle-1', 'add');
		if (typeof window.mbTooltip === 'undefined') {
			i18n = {
				'en': '; blocked ($1) by $2: $3 ($4 ago)',
				'zh': '；由$2封禁$1：$3（$4前）',
				'zh-hans': '；由$2封禁$1：$3（$4前）',
				'zh-hant': '；由$2封鎖$1：$3（$4前）',
			};
			i18n['zh-cn'] = i18n['zh-hans'];
			i18n['zh-my'] = i18n['zh-hans'];
			i18n['zh-sg'] = i18n['zh-hans'];
			i18n['zh-hk'] = i18n['zh-hant'];
			i18n['zh-mo'] = i18n['zh-hant'];
			i18n['zh-tw'] = i18n['zh-hant'];
			var mbTooltip = i18n[mw.config.get('wgUserLanguage')] || i18n.zh;
		} else {
			var mbTooltip = window.mbTooltip;
		}
		if (typeof window.mbTooltipPartial === 'undefined') {
			i18n = {
				'en': '; partially blocked ($1) by $2: $3 ($4 ago)',
				'zh': '；由$2部分封禁$1：$3（$4前）',
				'zh-hans': '；由$2部分封禁$1：$3（$4前）',
				'zh-hant': '；由$2部分封鎖$1：$3（$4前）',
			};
			i18n['zh-cn'] = i18n['zh-hans'];
			i18n['zh-my'] = i18n['zh-hans'];
			i18n['zh-sg'] = i18n['zh-hans'];
			i18n['zh-hk'] = i18n['zh-hant'];
			i18n['zh-mo'] = i18n['zh-hant'];
			i18n['zh-tw'] = i18n['zh-hant'];
			var mbTooltipPartial = i18n[mw.config.get('wgUserLanguage')] || i18n.zh;
		} else {
			var mbTooltipPartial = window.mbTooltipPartial;
		}
		if (typeof window.mbInfinity === 'undefined') {
			i18n = {
				'en': 'infinity',
				'zh': '无限期',
				'zh-hans': '无限期',
				'zh-hant': '無限期'
			}
			i18n['zh-cn'] = i18n['zh-hans'];
			i18n['zh-my'] = i18n['zh-hans'];
			i18n['zh-sg'] = i18n['zh-hans'];
			i18n['zh-hk'] = i18n['zh-hant'];
			i18n['zh-mo'] = i18n['zh-hant'];
			i18n['zh-tw'] = i18n['zh-hant'];
			var mbInfinity = i18n[mw.config.get('wgUserLanguage')] || i18n.zh
		} else {
			var mbInfinity = window.mbInfinity;
		}

		// Get all aliases for user: & user_talk:
		var userNS = [];
		for (var ns in mw.config.get('wgNamespaceIds')) {
			if (mw.config.get('wgNamespaceIds')[ns] == 2 || mw.config.get('wgNamespaceIds')[ns] == 3) {
				userNS.push(ns.replace(/_/g, ' ') + ':');
			}
		}

		// Let wikis that are importing this gadget specify the local alias of Special:Contributions
		var markblocked_contributions = window.markblocked_contributions || 'Special:(?:Contribs|Contributions|用户贡献|用戶貢獻|使用者贡献|使用者貢獻)';
		// RegExp for all titles that are  User:| User_talk: | Special:Contributions/ (for userscripts)
		var userTitleRX = new RegExp('^(' + userNS.join('|') + '|' + markblocked_contributions + '\\/)+([^\\/#]+)$', 'i');

		// RegExp for links
		// articleRX also matches external links in order to support the noping template
		var articleRX = new RegExp(mw.config.get('wgArticlePath').replace('$1', '') + '([^#]+)');
		var scriptRX = new RegExp('^' + mw.config.get('wgScript') + '\\?title=([^#&]+)');

		var userLinks = {};
		var user,
			url,
			ma,
			pgTitle;

		// Find all "user" links and save them in userLinks : { 'users': [<link1>, <link2>, ...], 'user2': [<link3>, <link3>, ...], ... }
		contentLinks.each(function(i, lnk) {
			if ($(lnk).hasClass('mw-changeslist-date') || $(lnk).parent('span').hasClass('mw-history-undo') || $(lnk).parent('span').hasClass('mw-rollback-link')) return;
			url = $(lnk).attr('href');
			if (!url)  return;
			if (mw.util.isIPv6Address(url.replace(/^(?:https?:\/\/)/i, ''))) return;
			if (new URL(url, window.location.origin).origin !== window.location.origin) return;
			if (ma = articleRX.exec(url)) {
				pgTitle = ma[1];
			} else if (ma = scriptRX.exec(url)) {
				pgTitle = ma[1];
			} else {
				return;
			}
			pgTitle = decodeURIComponent(pgTitle).replace(/_/g, ' ');
			user = userTitleRX.exec(pgTitle);
			if (!user) return;
			user = user[2];
			if (mw.util.isIPv6Address(user)) user = user.toUpperCase();
			$(lnk).addClass('userlink');
			if (!userLinks[user]) userLinks[user] = [];
			userLinks[user].push(lnk);
		});

		// Convert users into array
		var users = [];
		for (var u in userLinks) {
			users.push(u);
		}
		if (users.length === 0) return;

		// API request
		var serverTime,
			apiRequests = 0;
		var waitingCSS = setCSS('a.userlink {opacity:' + (window.mbLoadingOpacity || 0.85) + '}', 'markBlockedStyle-2', 'add');
		while (users.length > 0) {
			apiRequests++;
			$.post(
				mw.util.wikiScript('api') + '?format=json&action=query', {
				list: 'blocks',
				bklimit: 100,
				bkusers: users.splice(0, 50).join('|'),
				bkprop: 'user|by|timestamp|expiry|reason|restrictions'
				// no need for 'id|flags'
			}, markLinks);
		}

		return; // the end

		// Callback: receive data and mark links
		function markLinks(resp, status, xhr) {

			serverTime = new Date(xhr.getResponseHeader('Date'));
			var list,
				blk,
				tip,
				links,
				lnk,
				blTime;
			if (!resp || !(list = resp.query) || !(list = list.blocks)) return;

			for (var i = 0; i < list.length; i++) {
				blk = list[i];
				var partial = blk.restrictions && !Array.isArray(blk.restrictions); //Partial block
				if (/^in/.test(blk.expiry)) {
					clss = partial ? 'user-blocked-partial' : 'user-blocked-indef';
					blTime = blk.expiry;
				} else {
					clss = partial ? 'user-blocked-partial' : 'user-blocked-temp';
					blTime = inHours(parseTS(blk.expiry) - parseTS(blk.timestamp));
				}
				tip = mbTooltip;
				if (partial) tip = mbTooltipPartial;
				tip = tip.replace('$1', blTime).replace('infinity', mbInfinity)
					.replace('$2', blk.by)
					.replace('$3', blk.reason)
					.replace('$4', inHours(serverTime - parseTS(blk.timestamp)));
				links = userLinks[blk.user];
				for (var k = 0; links && k < links.length; k++) {
					lnk = $(links[k]);
					lnk = lnk.addClass(clss);
					if (window.mbTipBox) {
						$('<span class=user-blocked-tipbox>#</span>').attr('title', tip).insertBefore(lnk);
					} else {
						lnk.attr('title', lnk.attr('title') + tip);
					}
				}
			}

			if (--apiRequests === 0) { // last response
				setCSS('', 'markBlockedStyle-2', 'remove');
				$('#ca-showblocks').parent().remove(); // remove added portlet link
			}
		}

		// --------AUX functions

		// 避免标签爆炸（mw.hook导致重复添加样式表）
		function setCSS(css, id, method) {
			var style = document.createElement('style');
			switch (method) {
			case 'add':
				if (document.getElementById(id))
					return;
				style.id = id;
				style.appendChild(document.createTextNode(css));
				document.head.appendChild(style);
				break;
			case 'remove':
				document.getElementById(id) && $('#' + id).remove(); // 原生document.getElementById(id).remove()方法不兼容IE
				break;
			default:
				return;
			}
		}

		// 20081226220605  or  2008-01-26T06:34:19Z   -> date
		function parseTS(ts) {
			var m = ts.replace(/\D/g, '').match(/(\d\d\d\d)(\d\d)(\d\d)(\d\d)(\d\d)(\d\d)/);
			return new Date(Date.UTC(m[1], m[2] - 1, m[3], m[4], m[5], m[6]));
		}

		function inHours(ms) { // milliseconds -> "2:30" or 5,06d or 21d
			var mm = Math.floor(ms / 60000);
			if (!mm) return Math.floor(ms / 1000) + '秒';
			var hh = Math.floor(mm / 60);
			mm = mm % 60;
			var dd = Math.floor(hh / 24);
			hh = hh % 24;
			if (dd) {
				if (dd < 10 && hh) return dd + '日' + hh + '小時';
				return dd + '日';
			}
			return hh + '小時' + zz(mm) + '分';
		}

		function zz(v) { // 6 -> '06'
			if (v <= 9) v = '0' + v;
			return v;
		}

	} // -- end of main function


	// Start on some pages
	switch (mw.config.get('wgAction')) {
	case 'edit':
	case 'submit':
		break;
	case 'view':
		if (mw.config.get('wgNamespaceNumber') === 0) {
			break;
		}
		// Otherwise continue with default
	default: // 'history', 'purge'
		$.when($.ready, mw.loader.using('mediawiki.util')).then(function() {
			if (window.mbNoAutoStart) {
				var portletLink = mw.util.addPortletLink('p-cactions', '', 'XX', 'ca-showblocks');
				$(portletLink).click(function(e) {
					e.preventDefault();
					markBlocked();
				});
			} else {
				mw.hook('wikipage.content').add(function(e) {
					if (e.attr('id') === 'mw-content-text') markBlocked();
				});
			}
		});
	}
})(jQuery, mw);