#JSOUP
*Jsoup is a Java based library to work with HTML based content.
*It provides a very convenient API to extract and manipulate data, using the best of DOM, CSS, and jquery-like methods.

####Jsoup library provides the following:
1.**Multiple Read Support** - It reads and parses HTML using URL, file, or string.
2.**CSS Selectors** It can find and extract data, using DOM traversal or CSS selectors.
3.**DOM Manipulation** It can manipulate the HTML elements, attributes, and text.
4.**Prevent XSS attacks**It can clean user-submitted content against a given safe white-list, to prevent XSS attacks.
5.**Tidy**It outputs tidy HTML.
6.**Handles invalid data** - jsoup can handle unclosed tags, implicit tags and can reliably create the document structure.

##Environmental Setup
More information to refer this link[jsoup environment](https://www.tutorialspoint.com/jsoup/jsoup_environment.htm)

##Input
###Parsing String
*Parsing an HTML String into a Document object.
####Syntax
`Document document = Jsoup.parse(html);`
***document** - document object represents the HTML DOM.
***Jsoup** - main class to parse the given HTML String.
***html** - HTML String.
####Example
*JsoupTester.java*
```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

public class JsoupTester {
   public static void main(String[] args) {
      String html = "<html><head><title>Sample Title</title></head>"
         + "<body><p>Sample Content</p></body></html>";
      Document document = Jsoup.parse(html);
      System.out.println(document.title());
      Elements paragraphs = document.getElementsByTag("p");
      for (Element paragraph : paragraphs) {
            System.out.println(paragraph.text());
      }
   }
}
```
####Verify the result
Compile
`C:\jsoup>javac JsoupTester.java`
Run
`C:\jsoup>java JsoupTester`
Result
``
Sample Title
Sample Content
``
To refer this link[jsoup parse string](https://www.tutorialspoint.com/jsoup/jsoup_parse_string.htm)

###Parsing Body
*Parsing an HTML fragement String into a Element object as html body.
####Syntax
``
Document document = Jsoup.parseBodyFragment(html);
Element body = document.body();
``
***body** - represents element children of the document's body element and is equivalent to document.getElementsByTag("body").
To refer this link[jsoup parse body](https://www.tutorialspoint.com/jsoup/jsoup_parse_body.htm)

###Loading URL
*Fetching an HTML from the web using a url and then find its data.
####Syntax
``
String url = "http://www.google.com";
Document document = Jsoup.connect(url).get();
``
***url** - url of the html page to load.
####Example
```java
import java.io.IOException;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class JsoupTester {
   public static void main(String[] args) throws IOException {
      String url = "http://www.google.com";
      Document document = Jsoup.connect(url).get();
      System.out.println(document.title());
   }
}
```
####Verify the result
Result
`Google`
To refer this link[jsoup loading url](https://www.tutorialspoint.com/jsoup/jsoup_load_url.htm)

###Loading File
*Fetching an HTML from the disk using a file and then find its data.
####Syntax
``
String url = "http://www.google.com";
Document document = Jsoup.connect(url).get();
``
***url** - url of the html page to load.
####Example
```java
import java.io.File;
import java.io.IOException;
import java.net.URISyntaxException;
import java.net.URL;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class JsoupTester {
   public static void main(String[] args) throws IOException
      , URISyntaxException {
      URL path = ClassLoader.getSystemResource("test.htm");
      File input = new File(path.toURI());
      Document document = Jsoup.parse(input, "UTF-8");
      System.out.println(document.title());
   }
}
```
```html
<html>
   <head>
      <title>Sample Title</title>
   </head>
   <body>
      <p>Sample Content</p>
   </body>
</html>
```
####Verify the result
Result
`Sample Title`
To refer this link[jsoup loading file](https://www.tutorialspoint.com/jsoup/jsoup_load_file.htm)

##Extracting Data
###Using DOM Methods
To refer this link[jsoup DOM methods](https://www.tutorialspoint.com/jsoup/jsoup_use_dom.htm)
###Using Selector Syntax
To refer this link[jsoup selector syntax](https://www.tutorialspoint.com/jsoup/jsoup_use_selector.htm)
###Extract Attributes
To refer this link[jsoup extract attributes](https://www.tutorialspoint.com/jsoup/jsoup_extract_attribute.htm)
###Extract Text
To refer this link[jsoup extract text](https://www.tutorialspoint.com/jsoup/jsoup_extract_text.htm)
###Extract HTML
To refer this link[jsoup extract html](https://www.tutorialspoint.com/jsoup/jsoup_extract_html.htm)
###Working with URLs
To refer this link[jsoup work with urls](https://www.tutorialspoint.com/jsoup/jsoup_use_url.htm)

##Modifying Data
###Set Attributes
To refer this link[jsoup set attributes](https://www.tutorialspoint.com/jsoup/jsoup_set_attributes.htm)
###Set HTML
To refer this link[jsoup set html](https://www.tutorialspoint.com/jsoup/jsoup_set_html.htm)
###Set Text
To refer this link[jsoup set text](https://www.tutorialspoint.com/jsoup/jsoup_set_text.htm)

##Cleaning HTML
###Sanitize HTML
Following example will showcase prevention of XSS attacks or cross-site scripting attack.
####Syntax
`String safeHtml =  Jsoup.clean(html, Whitelist.basic());`
***Jsoup** - main class to parse the given HTML String.
***html** - Initial HTML String.
***safeHtml** - Cleaned HTML.
***Whitelist** - Object to provide default configurations to safeguard html.
***clean()** - cleans the html using Whitelist.
####Example
*JsoupTester.java*
```java
import org.jsoup.Jsoup;
import org.jsoup.safety.Whitelist;

public class JsoupTester {
   public static void main(String[] args) {
      String html = "<p><a href='http://example.com/'"
         +" onclick='checkData()'>Link</a></p>";

      System.out.println("Initial HTML: " + html);
      String safeHtml =  Jsoup.clean(html, Whitelist.basic());

      System.out.println("Cleaned HTML: " +safeHtml);
   }
}
```
####Verify the result
Compile
`C:\jsoup>javac JsoupTester.java`
Run
`C:\jsoup>java JsoupTester`
Result
``
Initial HTML: <p><a href='http://example.com/' onclick='checkData()'>Link</a></p>
Cleaned HTML: <p><a href="http://example.com/" rel="nofollow">Link</a></p>
``
To refer this link[jsoup sanitize html](https://www.tutorialspoint.com/jsoup/jsoup_sanitize_html.htm)
