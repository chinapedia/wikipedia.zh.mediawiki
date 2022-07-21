本模板產生的HTML記號包含了[[HCard|HCard 微格式]]，能夠讓電腦[[語法分析|解析]]地點名稱和位置，具有可自動將文章分類至適當類別的功能。在HCard中有[[Geo|Geo微格式]]，能讓電腦分析[[经纬度]]資料，因此可在地圖上查詢，或下載至[[全球定位系统]]（GPS）裝置。關於[[微格式]]的更多使用資訊，請參閱[[Wikipedia:專題/微格式|維基百科的微格式專題]]。

hCard 使用以下的 HTML class：
{{flatlist|
* {{Code|adr}}
* {{Code|county-name}}
* {{Code|fn}}
* {{Code|label}}
* {{Code|locality}}
* {{Code|nickname}}
* {{Code|note}}
* {{Code|org}}
* {{Code|vcard}}
}}

Geo由{{tl2|coord}}產生，並使用以下的HTML class：
{{flatlist|
* {{Code|geo}}
* {{Code|latitude}}
* {{Code|longtitude}}
}}

'''请勿将这些class更名或删除。'''

當指定經緯度數值時，請避免太過詳細。
<includeonly>{{sandbox other||
[[Category:使用微格式的模板|{{PAGENAME}}]]
}}</includeonly><noinclude>{{Documentation}}</noinclude>