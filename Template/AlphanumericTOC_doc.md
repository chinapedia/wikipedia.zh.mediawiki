<includeonly>{{pp-template}}</includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
==Purpose==
This TOC template was created as a customizable substitute for the growing zoo of CompactTOCs.  Rather than have dozens of stylistic varieties, it is preferrable to have a single template which can be adjusted to fit the editor's wishes.

==Usage==
Insert <code><nowiki>{{AlphanumericTOC}}</nowiki></code> at the point in the article where you want the TOC to appear.  If using with a list, many editors have found it helpful to insert a TOC at both the beginning and end of the list.

===Parameters===
Toggling the style and display of elements within the TOC is accomplished by adding parameters with a null value (in the form <code>|''parameter''=|</code>).  This is a short list which will be expanded upon further in the following text:
*block v. inline formatting: <code>multiline</code>, <code>nobreak</code>;
*table alignment: <code>align</code>;
*addition of prefixes to the links: <code>prefixLink</code>, <code>prefixDesc</code>;
*suppressing the automatic table of contents: <code>notoc</code>; and,
*each of the links also has its own parameter which when used suppresses the display of the link.

===Block and inline formatting===
When the template is used without any parameters, it appears as:
{{AlphanumericTOC}}
This replicates what you would see with a template like <code>{{[[:Template:CompactTOCrefs|CompactTOCrefs]]}}</code>.  The templates <code>{{[[:Template:CompactTOC2|CompactTOC2]]}}</code>, <code>{{[[:Template:CompactTOC5T|CompactTOC5T]]}}</code>, and <code>{{[[:Template:CompactTOCrefs2|CompactTOCrefs2]]}}</code> display the text in a single inline list.  To accomplish this, add the parameter <code>nobreak</code> to the template:
<pre>
 {{AlphanumericTOC|
     nobreak=|}}
</pre>
{{AlphanumericTOC|nobreak=|}}

For a TOC which displays in a block format, like <code>{{[[:Template:CompactTOC4|CompactTOC4]]}}</code> and <code>{{[[:Template:CompactTOC5|CompactTOC5]]}}</code>, add the parameter <code>multiline</code>:
<pre>
 {{AlphanumericTOC|
     multiline=|}}
</pre>
{{AlphanumericTOC|multiline=|}}

'''Note:''' If these parameters are used in combination, <code>multiline</code> will always override any effects from <code>nobreak</code>.

===Aligning the TOC===
As is apparent from the examples already given, the natural state of the TOC is to appear along the left side of the page without any alignment.  Some of the existing TOCs, including <code>{{[[:Template:CompactTOC|CompactTOC]]}}</code>, <code>{{[[:Template:CompactTOC3|CompactTOC3]]}}</code>, and <code>{{[[:Template:CompactTOCrefs|CompactTOCrefs]]}}</code>, are aligned to the center of the page.  This can be replicated by adding the parameter <code>align</code> with a value of 'center':
<pre>
 {{AlphanumericTOC|
     align=center|}}
</pre>
{{AlphanumericTOC|align=center|}}
The TOC may also be aligned to the right or the left, causing the article text to wrap around it, but floating the TOC is generally discouraged.  Guidelines may be found at [[Wikipedia:Section#Floating the TOC]].

===Prefixing links or link descriptions===
The TOC templates <code>{{[[:Template:CompactTOCprefix|CompactTOCprefix]]}}</code> and <code>{{[[:Template:CompactTOC2wprefix|CompactTOC2wprefix]]}}</code> include the ability to add a prefix to the link with or without displaying it in the TOC.  This can also be accomplished with this template by using the parameters <code>prefixLink</code> and <code>prefixDesc</code>; the former adds the prefix to the actual link, and the latter adds the prefix to the text displayed on the page.  Examples:
<pre>
 {{AlphanumericTOC|
     prefixLink=1.|}}
</pre>
{{AlphanumericTOC|prefixLink=1.|}}
<pre>
 {{AlphanumericTOC|
     prefixLink=hidden|
     prefixDesc=visible|}}
</pre>
{{AlphanumericTOC|prefixLink=hidden|prefixDesc=visible|}}
<pre>
 {{AlphanumericTOC|
     prefixDesc=+ |}}
</pre>
{{AlphanumericTOC|prefixDesc=+ |}}

===Suppression of the normal TOC===
In the cases where it might not be desirable to suppress the automatically generated table of contents this template uses the parameter <code>notoc</code> to prevent suppression.  If you want to allow the software to generate a table of contents, use the following:
<pre>
 {{AlphanumericTOC|
     notoc=|}}
</pre>

===Selective link removal===
One of the reasons for having so many different versions of CompactTOC has been that some articles do not have a 'References' section, or the TOC is being used for a list contained within a larger article.  This template solves the problem by providing a parameter for each link to be removed.  They are as follows:
*<code>numbers</code>: removes the numbers link
*<code>a</code>, <code>b</code>, etc.: removes the link for that letter; alternatively it can be used to create unlinked letters (see example below)
*<code>sections</code>: removes all links appearing after the letters
*<code>top</code>: removes the link to the 'Top of Page'
*<code>seealso</code>: removes the link to the 'See also' section
*<code>references</code>: removes the link to the 'References' section
*<code>externallinks</code>: removes the link to the 'External links' section

Some examples:
<pre>
 {{AlphanumericTOC|
     numbers=|
     sections=|}}
</pre>
{{AlphanumericTOC|numbers=|sections=|}}
<pre>
 {{AlphanumericTOC|
     numbers=|
     i=|
     n=|
     x=|
     z=|
     references=|}}
</pre>
{{AlphanumericTOC|numbers=|i=|n=|x=|z=|references=|}}
<pre>
 {{AlphanumericTOC|
     numbers=|
     i=I|
     j=J|
     v=V|
     x=X|
     nobreak=|
     top=|}}
</pre>
{{AlphanumericTOC|numbers=|i=I|j=J|v=V|x=X|nobreak=|top=|}}
<pre>
 {{AlphanumericTOC|
     multiline=|
     align=center|
     g=|
     seealso=|
     externallinks=|}}
</pre>
{{AlphanumericTOC|multiline=|align=center|g=|seealso=|externallinks=|}}

===Optional user defined section links===
Optional section links may be defined using the parameters <code>sec1</code>, <code>sec2</code>, <code>sec3</code>, <code>sec4</code>, and <code>sec5</code>, as follows:

<pre>
 {{AlphanumericTOC|
     numbers=|
     seealso=|
     externallinks=|
     sec1=Added section|
     sec2=Plus one|}}
</pre>
{{AlphanumericTOC|numbers=|seealso=|externallinks=|sec1=Added section|sec2=Plus one|}}

==編輯歷史==
Major revisions:
*Created & documented March 4, 2006 by [[User:Moverton|Moverton]]
*Changed to use #if [[m:ParserFunctions|ParserFunctions]] June 17, 2006 by [[User:Moverton|Moverton]] — This change should not impact the function or appearance of any existing usage.
*Added optional user defined section links November 17, 2006 by [[User:Moverton|Moverton]] — This change should not impact the function or appearance of any existing usage.
*Added optional <code>top</code> parameter December 27, 2006 by [[User:Moverton|Moverton]] — This allows for optional removal of the link to the 'Top of Page'; it should not impact the function of any existing usage.
<includeonly>
*2007年9月15日 (六) 09:20 (UTC)移植至中文版

<!-- ADD CATEGORIES BELOW THIS LINE -->
[[Category:目錄模板|{{PAGENAME}}]]
</includeonly>