<span id="{{{1|127.0.0.1}}}" class="template-IPvandal">{{#iferror:{{#expr:{{{1}}} round 0}}
|<!--IPV6-->{{<includeonly>safesubst:</includeonly>User-multi<noinclude>/template</noinclude>
 | User      = {{{1|{{{User|{{{user|}}}}}}}}}
 | demo      = {{{demo|}}}
 |t |c |<!--If param 1 does not contain a slash-->{{#if:{{#titleparts:{{{1|}}}|1|2}}||c64}} |dc |efl |whois |rbl |http |bu |bl
}}
|<!--IPV4-->{{<includeonly>safesubst:</includeonly>User-multi<noinclude>/template</noinclude>
 | User      = {{{1|{{{User|{{{user|}}}}}}}}}
 | demo      = {{{demo|}}}
 |t |c |dc |efl |whois |rdns |rbl |http |bu |bl
}}
}}</span><noinclude>
{{Documentation}}
</noinclude>