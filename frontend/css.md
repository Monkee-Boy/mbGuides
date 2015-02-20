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
