_This is a work in progress…_

# Front-end Code Guide

For HTML, CSS (Sass) and JavaScript.

## Overview

The purpose of this guide is to help you write readable, maintainable and scalable code. It is a living document which should reviewed on an ongoing basis.

Please [open an issue on GitHub](https://github.com/michaelthorne/codeguide/issues/new) if you’d like to contribute.

## Table of Contents

- [1. General](#general)
- [2. Browsers](#browsers)
- [3. HTML](#html)
 - [3.1 General](#html-general)
 - [3.2 Terminology](#html-terminology)
 - [3.3 Syntax](#html-syntax)
 - [3.4 Document Type Definition (DTD)](#html-document-type-definition)
 - [3.5 Language](#html-language)
 - [3.6 Character Encoding](#html-character-encoding)
 - [3.7 Internet Explorer Compatibility Mode](#html-internet-explorer-compatibility-mode)
 - [3.8 Attribute Order](#html-attribute-order)
 - [3.9 Boolean Attributes](#html-boolean-attributes)
 - [3.10 Semantics](#html-semantics)
 - [3.11 Using WAI-ARIA in HTML](#html-using-wai-aria)
 - [3.12 Validation](#html-validation)
- [4. CSS](#css)
 - [4.1 General](#css-general)
 - [4.2 Terminology](#css-terminology)
 - [4.3 Syntax](#css-syntax)
 - [4.4 Commenting](#css-commenting)
 - [4.5 Naming Conventions](#css-naming-conventions)
 - [4.6 Declaration Order](#css-declaration-order)
 - [4.7 Selectors](#css-selectors)
- [5. Sass](#sass)
- [6. JavaScript](#javascript)
- [7. Linting](#linting)
- [8. References](#references)
- [9. Inspiration & Credits](#inspiration-and-credits)

<a name="general"></a>
## 1. General

- There must always be a clear separation of concerns: structure, presentation and behavior
- Indentation must be 4 spaces (and not tabs)
- Make meaningful use of whitespace
- Consider a sensible maximum for line-length e.g. **80 character** wide columns
- Remove any trailing whitespace from the end of each line
- [EditorConfig](http://editorconfig.org) can help maintain the basic whitespace conventions
- When in doubt use existing, common patterns or refer to other [guidelines](#6-inspiration--credits)

<a name="browsers"></a>
## 2. Browsers

Through the practice of [progressive enhancement and graceful degradation](http://alistapart.com/article/understandingprogressiveenhancement) a website _should_ render in any web browser. But the experience for each visitor will differ based on the features supported in the version of the browser in use.

### Currently supported browsers:

- Chrome
- Firefox
- Internet Explorer 9+
- Microsoft Edge
- Opera
- Safari

> Do websites need to look exactly the same in every browser?

[No](http://dowebsitesneedtolookexactlythesameineverybrowser.com). Although your HTML should render without CSS or JavaScript – the content must be accessible and form submissions must work.

<a name="html"></a>
## 3. HTML

<a name="html-general"></a>
### 3.1 General

The basic structure of an HTML document:

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <title>Hello, World!</title>
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    
    <link rel="apple-touch-icon" href="apple-touch-icon.png">
    <link rel="stylesheet" href="main.css">
</head>
<body>
    <header role="banner">
    
    </header>

    <main role="main">

    </main>

    <footer role="contentinfo">
    
    </footer>

    <script src="main.js"></script>
</body>
</html>
```

<a name="html-terminology"></a>
### 3.2 Terminology

#### HTML Elements

Elements typically consist of a start and end tag, attributes and contents. The contents of an element are determined by it’s content model. Attributes and their values are not considered to be part of the contents of an element.

Example of an element: `<p>This is the content of a paragraph element.</p>`

> A void element is an element whose content model never allows it to have contents under any circumstances. Void elements can have attributes. – [W3C](http://www.w3.org/TR/html-markup/syntax.html#void-element)

Examples of void elements in HTML: `<hr>`, `<img>`, `<input>`, `<link>`, `<meta>`

#### HTML Tags

Tags are used to mark the start and end of HTML elements. Optionally, tags can have attributes.

Example of a start tag: `<p>`

Example of an end tag: `</p>`

#### HTML Attributes

Attributes have a `name` and `value` and are specified in the element’s start tag.

Example of an element’s attributes: `<img src="" alt="">`

<a name="html-syntax"></a>
### 3.3 Syntax

- HTML tag names and attribute values must be in lowercase
- Use double quotes (`""`) around attribute values
- Omit the `type` attribute when including style sheets and scripts
- Use a new line for every [block-level](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements) element

<a name="html-document-type-definition"></a>
### 3.4 Document Type Definition (DTD):

Include the HTML5 doctype:

```html
<!doctype html>
```

> Including the doctype in a document ensures that the browser makes a best-effort attempt at following the relevant specifications. – [W3C](http://www.w3.org/TR/html5/syntax.html#the-doctype)

<a name="html-language"></a>
### 3.5 Language

Specify the language [code](http://www.loc.gov/standards/iso639-2/php/code_list.php) for your HTML document:

```html
<html lang="en">
```

> Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth. – [W3C](http://www.w3.org/TR/html5/semantics.html#the-html-element)

<a name="html-character-encoding"></a>
### 3.6 Character Encoding

Define the HTML document’s character set as [utf-8](http://www.utf-8.com):

```html
<meta charset="utf-8">
```

> Unicode is a universal character set, ie. a standard that defines, in one place, all the characters needed for writing the majority of living languages in use on computers. It aims to be, and to a large extent already is, a superset of all other character sets that have been encoded. – [W3C](http://www.w3.org/International/articles/definitions-characters)

<a name="html-internet-explorer-compatibility-mode"></a>
### 3.7 Internet Explorer Compatibility Mode

Ensure that IE uses the latest engine:

```html
<meta http-equiv="x-ua-compatible" content="ie=edge">
```

> The idea behind compatibility mode is to allow web sites and applications that are not designed to modern standards to continue to work while upgrades can be made, allowing end users to upgrade to the latest browser version. Designating 'IE=edge' is the best practice because it ensures Internet Explorer uses the latest engine. The most current Internet Explorer version includes the latest security updates as well as feature support. The current version is also the fastest version. – [modern.IE](https://www.modern.ie/en-us/performance/how-to-use-x-ua-compatible)

<a name="html-attribute-order"></a>
### 3.8 Attribute Order

In order to improve the general readability of code, it is recommended to place tag attributes in the following order:

- `class`
- `type`
- `id`, `name`
- `placeholder`, `value`, `maxlength`, 'checked`, `selected`, `disabled`, `required`
- `for`, `href`, `src`, `srcset`
- `action`, `method`, `href`, `target`
- `width`, `height`
- `title`, `alt`
- `data-*`
- `aria-*`, `role`

This is an example of the recommended attribute order for an **image**:

```html
<img src="…" width="…" height="…" title="…" alt="…">
```

This is an example of the recommended attribute order for a **form control**:

```html
<input class="…" type="…" name="…" required>
```

This is an example of the recommended attribute order for an **anchor**:

```html
<a class="…" href="…" target="…" title="…" data-attribute="…">
```

This is an example of the recommended attribute order for a **div**:

```html
<div class="…" id="…" aria-controls="…" role="…">
```

<a name="html-boolean-attributes"></a>
### 3.9 Boolean Attributes

> The presence of a boolean attribute on an element represents the true value, and the absence of the attribute represents the false value. – [WHATWG](https://html.spec.whatwg.org/#boolean-attributes)

In HTML5, the following variations for setting a boolean attribute to **true** are valid:

```
autofocus
autofocus=""
autofocus="autofocus"
```

However, the preference is to _not add a value_. For example:

```
<input type="text" autofocus>
```

<a name="html-semantics"></a>
### 3.10 Semantics

Use the appropriate element when marking up your content to give it meaning on a web page. Semantic code describes the value of the content on a page, independent of it’s style.

```
<!-- ✗ -->
<div class="button">Submit</div>

<!-- ✓ -->
<button>Submit</button>
```

Have a look at the [HTML5 Sectioning Element Flowchart](http://html5doctor.com/resources/#flowchart) if you get stuck.

Avoid adding superflous parent elements when writing HTML – reduce markup wherever possible.

```
<!-- ✗ -->
<span class="logo">
    <img src="…">
</span>

<!-- ✓ -->
<img class="logo" src="…">
```

<a name="html-using-wai-aria"></a>
### 3.11 Using WAI-ARIA in HTML

The main goal of the ARIA specification is to improve the overall accessibility of websites.

> WAI-ARIA, the Accessible Rich Internet Applications Suite, defines a way to make Web content and Web applications more accessible to people with disabilities. It especially helps with dynamic content and advanced user interface controls developed with Ajax, HTML, JavaScript, and related technologies. – [WAI-ARIA Overview](http://www.w3.org/WAI/intro/aria)

As per the W3C draft, [using WAI-ARIA in HTML](http://www.w3.org/TR/aria-in-html), rather use native HTML elements wherever possible as it will have the semantics and required behaviour built-in.

<a name="html-validation"></a>
### 3.12 Validation

Use tools like the [W3C Markup Validation Service](http://validator.w3.org) or the [Nu Markup Checker](http://validator.w3.org/nu) to validate your markup.

Reasons for validating:

- Useful as a debugging tool (modern browsers do a good job of fixing “tag soup”)
- Helps to future-proof your code by adhering to [Web Standards](https://www.w3.org/standards)
- Improves maintainability over time by agreeing to a global code style
- Teaches best practices to newcomers and raises awareness of accessbility

Continue reading about [why you should validate](https://validator.w3.org/docs/why.html).

<a name="css"></a>
## 4. CSS

<a name="css-general"></a>
### 4.1 General

> Every time you write inline styles in your markup, a front-end developer somewhere dies – whether it’s in a style tag or directly in the markup. Don’t do it. – [TMWtech](http://tech.tmw.co.uk/code/TMW-frontend-guidelines/)

This guide assumes that [Sass](http://sass-lang.com) will be used as the preprocessor to compile your CSS. The majority of the rules in this guide also apply to vanilla CSS, unless otherwise stated.

The features in Sass that we use are:

- Variables
- Nesting
- Partials
- Mixins

<a name="css-terminology"></a>
### 4.2 Terminology

A rule set (also called “rule”) consists of a selector followed by a declaration block:

```
[selector] {
    [property]: [value];
}
```

> A selector is a chain of one or more sequences of simple selectors separated by combinators. One pseudo-element may be appended to the last sequence of simple selectors in a selector. – [W3C](https://www.w3.org/TR/2011/REC-css3-selectors-20110929/#selector-syntax)

For example:

```
.foo {
    background-color: red;
    color: white;
}
```

> A simple selector is either a type selector, universal selector, attribute selector, class selector, ID selector, or pseudo-class. – [W3C](https://www.w3.org/TR/2011/REC-css3-selectors-20110929/#selector-syntax)

#### Type

```
h1 {

}
```

#### Universal

```
* {

}
```

#### Attribute

```
a[rel="external"] {

}
```

#### Class

```
.hero {

}
```

#### ID

```
#top {

}
```

#### Pseudo

```
button:focus {

}
```

> Combinators are: whitespace, "greater-than sign" (U+003E, >), "plus sign" (U+002B, +) and "tilde" (U+007E, ~). – [W3C](https://www.w3.org/TR/2011/REC-css3-selectors-20110929/#selector-syntax)

For example:

#### Descendant combinator

```
nav a {

}
```

#### Child combinator

```
ul > li {

}
```

#### Adjacent sibling

```
p + h2 {

}
```

#### General sibling

```
div ~ hr {

}
```

<a name="css-syntax"></a>
### 4.3 Syntax

<a name="css-commenting"></a>
### 4.4 Commenting

<a name="css-naming-conventions"></a>
### 4.5 Naming Conventions

<a name="css-declaration-order"></a>
### 4.6 Declaration Order

<a name="css-selectors"></a>
### 4.7 Selectors

<a name="sass"></a>
## 5. Sass

<a name="javascript"></a>
## 6. JavaScript

<a name="linting"></a>
## 7. Linting

<a name="references"></a>
## 8. References

- [Dive Into HTML5](http://diveintohtml5.info)
- [HTML5 Doctor](http://html5doctor.com)
- [Mozilla Developer Network](https://developer.mozilla.org)
- [World Wide Web Consortium (W3C)](http://www.w3.org)

<a name="inspiration-and-credits"></a>
## 9. Inspiration & Credits

- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.xml)
- [Code Guide by Mark Otto](http://codeguide.co)
- [Idiomatic CSS by Nicolas Gallagher](https://github.com/necolas/idiomatic-css)
- [CSS Guidelines by Harry Roberts](http://cssguidelin.es/)
- [TMW Unlimited Front-End Dev guidelines](http://tech.tmw.co.uk/code/TMW-frontend-guidelines)
- [Front end standards by Mark Brown](http://www.yellowshoe.com.au/standards/)
- [Sass Guidelines](https://sass-guidelin.es)
