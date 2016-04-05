# [seleniumQuery](http://seleniumquery.github.io)

### *Cross-Driver* jQuery-like Java interface for Selenium WebDriver

seleniumQuery is a Java library/framework that brings a ***cross-driver*** **jQuery-like** interface for [Selenium WebDriver](http://docs.seleniumhq.org/projects/webdriver/).

### Example snippet:

```java
// getting the value
String oldStreet = $("input.street").val();
// setting the value
$("input.street").val("4th St!");
```

### No special configuration needed - use it in your project right now:

On a regular `WebElement`...

```java
// an existing WebElement...
WebElement existingWebElement = driver.findElement(By.id("myId"));
// call jQuery functions
String elementVal = $(existingWebElement).val();
boolean isButton = $(existingWebElement).is(":button"); // enhanced selector!
for (WebElement child: $(existingWebElement).children()) {
  System.out.println("That element's child: "+child);
}
```

Or an existing `WebDriver`...

```java
// an existing WebDriver...
WebDriver driver = new FirefoxDriver();
// set it up
$.driver().use(driver);
// and use all the goods
for (WebElement e: $(".myClass:contains('My Text!'):not(:button)")) {
  System.out.println("That element: " + e);
}
```

## What can you do with it?

Allows querying elements by:

- **CSS3 Selectors** - `$(".myClass")`, `$("#table tr:nth-child(3n+1)")`;
- **jQuery/Sizzle enhancements** - `$(":text:eq(3)")`, `$(".myClass:contains('My Text!')")`;
- **XPath** - `$("//div/*/label/preceding::*")`;
- and even some own **seleniumQuery selectors**: `$("#myOldDiv").is(":not(:present)")`.

Built using Selenium WebDriver's native capabilities **only**:

- No `jQuery.js` is embedded at the page, no side-effects are generated;
    - Doesn't matter if the page uses jQuery or not (or even if the JavaScript global variable `$` is other library like `Prototype.js`).
- Capable of handling/testing JavaScript-disabled pages
    - Test pages that use [Unobtrusive JavaScript](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript).
    - Most functions don't even require the browser/driver to have JavaScript enabled!


## Quickstart: A running example

Try it out now with the running example below:

{% gist 78cc1ce6be5214d91403 %}


## Download and execute the **[seleniumQuery showcase project](https://github.com/acdcjunior/seleniumQuery-showcase)**

...and see seleniumQuery in action right now.

To get the latest version, add to your **`pom.xml`**:

```xml
<dependency>
    <groupId>io.github.seleniumquery</groupId>
    <artifactId>seleniumquery</artifactId>
    <version>0.15.0</version>
</dependency>
```

## Find more on [seleniumQuery's github repository](https://github.com/seleniumQuery/seleniumQuery).
