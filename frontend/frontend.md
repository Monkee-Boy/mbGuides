# OLD - Used as reference in new guides. Delete soon.




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
