# Front-end Code Standards

## CSS

### Multiline CSS
CSS should always be multiline, single line should not be used. All selectors and properties should be on their own line.

```
/* Correct */
.selector {
	display: block;
	width: 250px;
}

/* Correct */
.selector-1,
.selector-2 {
	display: block;
	width: 250px;
}

/* Incorrect */
.selector-1, .selector-2 {
	display: block;
	width: 250px;
}

/* Incorrect */
.selector-1,
.selector-2 {
	display: block; width: 250px;
}
```

### Selectors
* Use lowercase and hyphens to separate words when naming selectors. Don't use camelCase and underscores.
* Use readable selectors that describe what elements they style. You should always strive for reusable css through out the project.

```
/* Correct */
.comment-form {
	property: value;
}

/* Incorrect */
.commentForm {
	property: value;
}

/* Incorrect */
.cmt-lg {
	property: value;
}
```

### Properties and Values
* All properties and values should be lowercase, except font names.
* Use one selector per line in multi-selector rulesets.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include a single space after the colon of a declaration.
* Use lowercase and shorthand hex values: #fff instead of #FFFFFF.
* Use double quotes over single: `content: ""`.
* Avoid specifiying a unit if value is zero: `0` instead of `0px`.
* Separate each ruleset by a blank line.
* Width should also be declared before height.

```
/* Correct */
.selector {
	width: 300px;
	height: 500px;
	margin: 10px 15px;
	background: #fff;
	color: #333;
}

/* Incorrect */
.selector {
	background: white;
	color: #DDDDDD;
	height: 500px;
	margin-top: 10px;
	margin-right: 15px;
	margin-bottom: 10px;
	margin-left: 15px;
	width: 300px;
}
```

#### Declaration Order
Declarations should be ordered where structurally important properties (positioning and box-model) are declared prior to all others. Use the below format when structuring all declarations.

```
.selector {
	/* Positioning */
	position: absolute;
	z-index: 10;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;

	/* Display & Box Model */
	display: inline-block;
	overflow: hidden;
	box-sizing: border-box;
	width: 100px;
	height: 100px;
	padding: 10px;
	border: 10px solid #333;
	margin: 10px;

	/* Other */
	background: #000;
	color: #fff
	font-family: sans-serif;
	font-size: 1.4em;
	text-align: right;
}
```

Prefixed vendor-specific properties pairs should appear directly before the generic property they refer to. <a href="http://www.alistapart.com/comments/prefix-or-posthack//#9">Why?</a>

```
/* Correct */
.selector-1 {
	-moz-border-radius: 5px;
	-webkit-border-radius: 5px;
	border-radius: 5px;
}

/* Incorrect */
.selector-1 {
	border-radius: 5px;
	-moz-border-radius: 5px;
	-webkit-border-radius: 5px;
}
```

### Comments & Groups
Well commented code is extremely important. Taking the time to describe components, how they work, and their limitations will go a long way with other members on the team.

* Place comments on a new line above their subject.
* Avoid end of line comments.
* Keep line-length to a sensible maximum, e.g., 80 columns.
* Make use of comments to break CSS code into discrete sections.

```
/* Correct */
.selector {
	property: value;
}

/* Correct */
.selector {
	white-space: pre; /* CSS 2 */
	white-space: pre-wrap; /* CSS 2.1 */
	white-space: pre-line; /* CSS 3 */
	word-wrap: break-word; /* IE */
}

.selector { /* Incorrect */
	property: value;
}
```

Complete example of using comments.

```
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/**
 * Short description using Doxygen-style comment format
 *
 * Long description first sentence starts here and continues on this line for a
 * while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * @todo This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 */

/* Basic comment */
```

### Font Size and Line Height
* Unit-less line-height is preferred because it does not inherit a percentage value of its parent element and instead is based on a multiplier of the font-size.
* We use em for all font-sizes. A percentage is set on the body to start off at 10px (Ex: 1.2em inheriting from only body would be 12px). **This could change soon**

### Font Use & Abuse
Before embedding a custom font it is important that you check the license and check if web embedding is allowed. I strongly believe that if a font does not allow web embedding then we will not be embedding it at all. If the font is embeddable then using a proper bulletproof @font-face is required.

```
/* Correct */
@font-face {
	font-family: 'MyWebFont';
	src: url('webfont.eot'); /* IE9 Compat Modes */
	src: url('webfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
    	url('webfont.woff') format('woff'), /* Modern Browsers */
    	url('webfont.ttf')  format('truetype'), /* Safari, Android, iOS */
    	url('webfont.svg#svgFontName') format('svg'); /* Legacy iOS */
}
```

If you are looking for a custom font to embed then check out <a href="http://www.fontsquirrel.com/">http://www.fontsquirrel.com/</a> and <a href="http://www.google.com/webfonts">http://www.google.com/webfonts</a>.

### Feature Sniff
Don't sniff for a browser when you should be sniffing for features. The days of detecting IE to disregard new techniques are (kinda) over. With IE9 (and to an extent IE8) the browser has a lot of modern HTML5 and CSS3 abilities. This means you need to be using Modernizr to sniff browser features.

@todo: add examples and more info on feature sniffing.

## HTML

### Doctype
HTML5 Doctype is always to be used. It is simple, clear and throws IE6/7 into standards mode.

```
<!DOCTYPE html>
```

### SEO
@todo: Move this section to another guide and complete it.

### Tables for Tabular Data Only
Tables should only be used for the presentation of tabular data. The only exception is of course when composing HTML email, due to tables being almost the only thing supported by most clients.

Table headers should always be presented using `<th>` elements. Column headings should always be wrapped in `<thead>` and the table body should always be wrapped in `<tbody>`. If used the table footer should be wrapped in `<tfoot>`.

```
<!-- Correct -->
<table cellpadding="0" cellspacing="0" border="0">
	<thead>
		<tr>
			<th>Column One</th>
			<th>Column Two</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Cell Item</td>
			<td>Cell Item</td>
		</tr>
	</tbody>
</table>

<!-- Incorrect -->
<table>
	<tr>
		<td>Column One</td>
		<td>Column Two</td>
	</tr>
	<tr>
		<td>Cell Item</td>
		<td>Cell Item</td>
	</tr>
</table>
```

### Tags & Attributes
All tags and attributes must be written in lowercase. All attribute values also need to be lowercase when the text is only to be interpreted by machines.

```
<!-- Correct -->
<img src="dog.jpg" alt="Fido enjoying the dog park.">

<!-- Incorrect -->
<img SRC="dog.jpg" ALT="Fido enjoying the dog park.">
```

### Quotes
All attributes must have a value and must use double-quotes. This is according to the W3C.

```
<!-- Correct -->
<input type="text" name="email" disabled="disabled">

<!-- Incorrect -->
<input type=text name=email disabled>
```

### Feature Sniff
Don't sniff for a browser when you should be sniffing for features. The days of detecting IE to disregard new techniques are (kinda) over. With IE9 (and to an extent IE8) the browser has a lot of modern HTML5 and CSS3 abilities. This means you need to be using Modernizr to sniff browser features.

## Javascript

### jQuery
Know when to use it and when to use vanilla JavaScript.

### Whitespacing & Formatting
Consistent formatting makes code more readable and allows the code to be easily modified with find and replace commands.

In general, the use of whitespace should follow English reading conventions. There will be one space after each comma and colon (and semi-colon) but no spaces immediately inside the right and left sides of parenthesis. Braces should always appear on the same line as their preceding argument.

#### Character Spacing
```
// Correct
if (blah === "foo") {
	foo("bar");
}

// Incorrect
if(blah==="foo"){
	foo("bar");
}
```

#### Same Line Braces
```
// Correct
if (foo) {
	bar();
}

// Incorrect
if (foo)
{
	bar();
}
```

### Comments
* Long comments should use `/* ... */`
* Single line comments should always be on their own line and be above the line they reference, there should be an extra end line above it.

```
var foo = "bar";

// Lets do a loop
for (var i = 0; i < 10; i++) { ... }
```

### Blocks
Braces should be used on all if, else, else if conditionals including single line statements.

```
// Correct
if (blah === "foo") {
	// Do something
	// Do something else
} else {
	// Do something instead
}

// Correct
if (blah === "foo") {
	// Do something
}

// Incorrect
if (blah === "foo")
	// Do something

// Incorrect
if (blah === "foo") {
	// Do something
	// Do something else
} else
	// Do something instead
```

### Strict Equality Operator
The use of the strict quality operator === does not run type coercion and therefore strictly evaluates the difference between two objects.

For more information: <a href="http://bonsaiden.github.com/JavaScript-Garden/#types.equality">Javascript Garden</a>

### Avoid Comparing true and false
Direct comparison to the values of true and false is unnecessary, it just results in extra code.

```
// Correct
if (foo)
	// Do something

// Correct
if (!foo)
	// Do something

// Incorrect
if (foo === true)
	// Do something
```

### Camel Case Variables
The camelCasing of variables is accepted as the standard in most environments and should always be used.

## Accessibility

### Semantic Markup
You should always be writing valid semantic markup. Headings should be hierarchically created from `<h1>` onwards. Paragraphs should always be in `<p>` tags. The result will be clean and easy to follow code. This is also one of the simplest SEO fixes you can do.

### Microformats
Microformats are a way of making contact information machine readable. hCard classes are used to define the type of content contained within elements. These can be extracted by the browser or search engine crawler (Google makes heavy use of these as well as Bing). Mobile Safari on iOS devices do something similar for finding phone numbers and adding as a contact, etc.

```
<span class="vcard">
	<span class="adr">
	    <span class="type hidden">Work</span>
	    <span class="street-address">1234 Main St</span>
	    <span class="locality">Wichita Falls</span>,
	    <abbr class="region" title="Texas">TX</abbr>&nbsp;
	    <span class="postal-code">76301</span>
	    <span class="country-name">USA</span>
	</span><br />
	<span class="tel"><span class="type hidden">Work</span>P: <span class="value">940-555-1234</span></span><br />
        <span class="tel"><span class="type hidden">Fax</span> F: <span class="value">940-555-5678</span></span><br />
	<span class="email">jdoe@yourcompany.com</span><br />
</span>
```

For more information: <a href="http://microformats.org/wiki/hcard">http://microformats.org/wiki/hcard</a>

### Alt & Title Tags
The `<img>` tag requires alt text to validate as well as meet accessibility guidelines. The text in the alt attribute should be descriptive of what the image shows or is trying to achieve. That is if the image is not critical. If the image is a trivial icon then leave the alt attribute empty, but still present. A screenreader will then ignore it instead of having to read out "icon" 20 times.

```
<!-- Correct -->
<img src="dog.jpg" alt="Fido enjoying the dog park!">

<!-- Incorrect -->
<img src="bullet.png" alt="bullet">

<!-- Correct -->
<img src="bullet.png" alt="">
```
