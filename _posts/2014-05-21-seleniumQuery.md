#[seleniumQuery](http://seleniumquery.github.io) - Cross-Driver Selenium Java interface

###*Cross-driver* jQuery-like Java interface for Selenium WebDriver

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
     // sets Firefox as the driver -- this is optional, if omitted, will default
     // to HtmlUnit or whatever you set at the, also optional, config files
     //
     $.driver().useFirefox().withoutJavaScript(); // JS will be disabled!

     $.url("http://www.google.com/?hl=en");

     $(":text[name='q']").val("selenium"); // the keys are actually typed
     $(":button:contains('Google Search')").click();

     String resultsText = $("#resultStats").text();
     System.out.println(resultsText);

     // Besides the short syntax and the jQuery behavior you already know,
     // other very useful function in seleniumQuery is .waitUntil(),
     // handy for dealing with Ajax enabled pages:
     //
     $(":input[name='q']").waitUntil().is(":enabled");
     // The line above waits for no time, as that input is always enabled in google.com

     $.quit(); // quits the currently used driver (firefox)
  }
}
```
The code above can be found at the sample [seleniumQuery demos project](https://github.com/seleniumQuery/seleniumQuery-demos).

To get seleniumQuery's latest snapshot, add this to your **`pom.xml`**:
```xml
<!-- The project dependency -->
<dependencies>
    <dependency>
        <groupId>io.github.seleniumquery</groupId>
        <artifactId>seleniumquery</artifactId>
        <version>0.9.0-SNAPSHOT</version>
    </dependency>
</dependencies>
<!-- The repository the snapshots will be downloaded from.
    Can either go in your pom.xml or settings.xml -->
<repositories>
	<repository>
		<id>sonatype-nexus-snapshots</id>
		<name>Sonatype Nexus Snapshots</name>
		<url>https://oss.sonatype.org/content/repositories/snapshots/</url>
		<snapshots>
			<enabled>true</enabled>
			<updatePolicy>always</updatePolicy>
		</snapshots>
	</repository>
</repositories>
```

Find more on [`seleniumQuery's github repository`](https://github.com/seleniumQuery/seleniumQuery).
