# CSS ![Current Status](https://img.shields.io/badge/status-DRAFT-green.svg)

> All code in any code-base should look like a single person typed it, no matter how many people contributed.

* Don't optimize your code for the sake of optimizing; it should always be readable and understandable.
* Stylesheets should always be maintainable.
* Keep code transparent, sane, and readable at all times.
* Think scalable and modular. Don't get overly specific.
* **This is the agreed upon style and it should be strictly enforced.**

---

## File organization

All CSS and SASS files live together. On a typical project inside of `./css` will be your compiled and minified CSS files along with a SASS directory. The `./css/sass` directory should contain your primary .scss file along with any imports. If the project has a large number of SASS files then group together; for example `./css/sass/components/` which might house `_accordions.scss`, `_slider`, and `_callouts`.

```
./css
├── ./sass
│   ├── styles.scss
│   ├── _grid.scss
│   ├── _typography.scss
│   └── _forms.scss
├── app.css
└── app.min.css
```

Break out all SASS into import files for ease of use. Your main `./styles.scss` should mostly hold imports. Put an effort into grouping rulesets and use common sense.

---

## Formatting

* Use soft-tabs with a two space indent. Spaces are the only way to guarantee code renders the same in any person's environment.
* There should not be end-of-line whitespace.
* Never mix tabs and spaces.
* An .editorconfig should always be used to maintain these conventions.

---

## Comments

Well documented code can save the day. As with every language, this holds true for CSS as well. Other members of the team should not have to guess as to the purpose of non-obvious code. Taking a moment to describe how it work

* Comments should be on a new line above their subject.
* Make liberal use of comments to break CSS code into sections.
* Use sentence case comments and consistent indentation.

```
/* Short description using comment format. */
.selector {
  property: value;
}

/*
  Long description using comment format. Pellentesque habitant morbi
  tristique senectus et netus et malesuada fames ac turpis egestas.
  Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor
  sit amet, ante.
*/
.selector {
  property: value;
}

.selector { /* Do not do this. */
  property: value;
}
```

---

## Rulesets

* Single line CSS should never be used. All selectors and properties should be on their own line.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration. Do not tab to align colons.
* Include a single space after the colon of a declaration.
* Use lowercase and shorthand hex values, e.g., `#aaa`.
* Always use double quotes, e.g., `content: ""`.
* Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* Where allowed, avoid specifying units for zero-values, e.g., `margin: 0;`.
* Include a space after each comma in comma-separated property or function values.
* Include a semi-colon at the end of the last declaration in a declaration block.
* Place the closing brace of a ruleset in the same column as the first character of the ruleset.
* Separate each ruleset by a blank line.
* All properties and values should be lowercase, except font names.

```
/* Correct */
.selector {
  display: block;
  width: 250px;
}

/* Correct */
.selector-1, .selector-2 {
  display: block;
  width: 250px;
}

/* Incorrect */
.selector-1,
.selector-2 {
  display: block;
  width: 250px;
}

/* Incorrect */
.selector-1,
.selector-2 {
  display: block; width: 250px;
}

/* Really Incorrect */
.selector-1, .selector-2 { display: block; width: 250px; }
```

---

## Selectors
* Use lowercase and hyphens to separate words when naming selectors. Do not use camelCase or underscores.
* Use readable selectors that describe what elements they style. You should always strive for reusable css through out the project.
* Never reference js- prefixed class names from CSS files. js- are used exclusively from JavaScript files.

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
.cmt-frm {
  property: value;
}
```

---

## Declaration Order

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
  color: #fff;
  font-family: sans-serif;
  font-size: 16px;
  text-align: right;
}
```

---

## Preprocessors

At Monkee-Boy we use SASS as our preprocessor.

* Limit nesting to 2 levels deep. Reassess any nesting more than 3 levels deep. If you cannot help it, step back and rethink your overall strategy (either the specificity needed, or the layout of the nesting). This prevents overly-specific CSS selectors.
* Avoid large numbers of nested rules. Break them up when readability starts to be affected. Avoid nesting that spreads over more than 20 lines.
* Always place `@extend` statements on the first lines of a declaration block.
* Where possible, group `@include` statements at the top of a declaration block, after any `@extend` statements.
* Prefix all custom functions with `mb-`. This helps to avoid any potential to confuse your function with a native CSS function, or to clash with functions from libraries.
* Always make use of [Monkee-Boy/_mixins.scss](https://github.com/Monkee-Boy/_mixins.scss).

```
.selector-1 {
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);
    width: mb-grid-unit(1);
    // other declarations
}

.nested-0 {
  property: value;

  .nested-1 {
    property: value;

    .nested-2 {
      property: value;

      /* STOP NESTING */
    }
  }
}
```

---

### Font Use & Abuse
Before embedding a web font it is important to check the license and how it will affect performance. Only embed the weights you need and avoid using more than two web fonts.

[Monkee-Boy/_mixins.scss](https://github.com/Monkee-Boy/_mixins.scss/blob/master/_mixins.scss#L248) contains a great @font-face mixin to use when embedding fonts.

```
@include font-face(icomoon, /fonts/icomoon);

@mixin font-face($font-family, $file-path, $font-weight: normal, $font-style: normal) {
  @font-face {
    font-family: $font-family;
    font-weight: $font-weight;
    font-style: $font-style;
    src: url('#{$file-path}.eot');
    src: url('#{$file-path}.eot?#iefix') format('embedded-opentype'),
      url('#{$file-path}.woff') format('woff'),
      url('#{$file-path}.ttf') format('truetype'),
      url('#{$file-path}.svg##{$font-family}') format('svg');
  }
}
```

If you are looking for a custom font to embed then check out <a href="http://www.fontsquirrel.com/">http://www.fontsquirrel.com/</a> and <a href="http://www.google.com/webfonts">http://www.google.com/webfonts</a>.

---

#### Thanks
* [necolas/idiomatic-css](https://github.com/necolas/idiomatic-css)
* [CSS Guidelines](http://cssguidelin.es/)
* [github.com/styleguide/css](https://github.com/styleguide/css)
