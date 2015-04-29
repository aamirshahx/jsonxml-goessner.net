## Update/Issues:

> Issue: Now using indexed for loop iterating over array objects instead of for..in loop in json2xml.
> Update: CDATA processing tests added to xmljson_test.html.
> Update: Supporting CDATA sections in xml2json and json2xml.
> Bug: Not properly reading over CDATA sections in xml2json .. resolved.

## Usage:

function xml2json(xml,  // element or document DOM node
                  tab)  // tab or indent string for pretty output formatting
                        // omit or use empty string "" to supress.
                        // returns JSON string

function json2xml(obj,  // javascript object
                  tab)  // tab or indent string for pretty output formatting
                        // omit or use empty string "" to supress.
                        // returns XML string

The test application xmljson_test.html uses xml strings, which have to be parsed first. This can be accomplished by the following function � tested by Firefox 1.5 and IE6:

>
>
> function parseXml(xml) {
>
>   var dom = null;
>
>   if (window.DOMParser) {
>
>      try {
>
>         dom = (new DOMParser()).parseFromString(xml, "text/xml");
>
>      }
>
>      catch (e) { dom = null; }
>
>   }
>
>   else if (window.ActiveXObject) {
>
>      try {
>
>         dom = new ActiveXObject('Microsoft.XMLDOM');
>
>         dom.async = false;
>
>         if (!dom.loadXML(xml)) // parse error ..
>
>            window.alert(dom.parseError.reason + dom.parseError.srcText);

>      }

>      catch (e) { dom = null; }

>   }

>   else

>      alert("cannot parse xml string!");

>   return dom;

> }

With that helper function a conversion can be performed as follows:

> var xml = '<e name="value">text</e>',

>    dom = parseXml(xml),

>    json = xml2json(dom),

>    xml2 = json2xml(eval(json));

###Article
Read more about [Converting between XML and JSON](http://www.xml.com/pub/a/2006/05/31/converting-between-xml-and-json.html).