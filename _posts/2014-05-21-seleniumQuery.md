#[seleniumQuery](http://seleniumquery.github.io)
###*Cross-Driver* jQuery-like Java interface for Selenium WebDriver

seleniumQuery is a Java library/framework that brings a ***cross-driver*** **jQuery-like** interface for [Selenium WebDriver](http://docs.seleniumhq.org/projects/webdriver/).

Example snippet:

```java
// getting the value
String oldStreet = $("input.street").val();
// setting the value
$("input.street").val("4th St!");
```

Allows querying elements by:

- **CSS3 Selectors** - `$(".myClass")`, `$("#table tr:nth-child(3n+1)")`;
- **jQuery/Sizzle enhancements** - `$(":text:eq(3)")`, `$(".myClass:contains('My Text!')")`;
- **XPath** - `$("//div/*/label/preceding::*")`;
- and even some own **seleniumQuery selectors**: `$("#myOldDiv").is(":not(:present)")`.

Built using Selenium WebDriver's native capabilities **only**:

- No `jQuery.js` is embedded at the page, no side-effects are generated;
    - Doesn't matter if the page uses jQuery or not (or even if the JavaScript global variable `$` is other library like `Prototype.js`).
- Capable of handling/testing **JavaScript-disabled pages**
    - Test pages that use [Unobtrusive JavaScript](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript).
    - Most functions don't even require the browser/driver to have JavaScript enabled!

##Quickstart: A running example

Try it out now with the running example below:

```java
import static io.github.seleniumquery.SeleniumQuery.$; // this will allow the short syntax

public class SeleniumQueryExample {
  public static void main(String[] args) {
    // sets Firefox as the driver (this is optional, if omitted, will default to HtmlUnit)
    $.driver().useFirefox().withoutJavaScript(); // JavaScript will be disabled!

    $.url("http://www.google.com/?hl=en");

    $(":text[name='q']").val("selenium"); // the keys are actually typed!
    $(":button:contains('Google Search')").click();
    // Another way: $(":text[name='q']").val("selenium").submit();

    // Besides the short syntax and the jQuery behavior you already know,
    // other very useful function in seleniumQuery is .waitUntil(),
    // handy for dealing with user-waiting actions (specially in Ajax enabled pages):
    String resultsText = $("#resultStats").waitUntil().is(":visible").then().text();
    System.out.println(resultsText);

    $.quit(); // quits the currently used driver (firefox)
  }
}
```

The code above can be found at the [seleniumQuery demos project](https://github.com/seleniumQuery/seleniumQuery-demos). To get the latest version, add to your **`pom.xml`**:

```xml
<dependency>
    <groupId>io.github.seleniumquery</groupId>
    <artifactId>seleniumquery</artifactId>
    <version>0.9.0</version>
</dependency>
```

Find more on [`seleniumQuery's github repository`](https://github.com/seleniumQuery/seleniumQuery).
