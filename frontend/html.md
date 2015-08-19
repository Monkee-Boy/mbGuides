# HTML ![Current Status](https://img.shields.io/badge/status-DRAFT-green.svg)

> All code in any code-base should look like a single person typed it, no matter how many people contributed.

* Always think structure when writing HTML. Ignore styles and focus on each piece of content; what it is, how it should be structured in the dom, and is it still readable if CSS doesn't load.
* The goal is semantic, SEO, and accessible friendly HTML.
* Reference **Front End - CSS** for how to name classes.
* Reference **Front End - Accessibility** for more on SEO, microformats, schemas, etc.
* **This is the agreed upon style and it should be strictly enforced.**

---

## Doctype

One doctype to rule them all. A proper doctype helps you avoid quirks mode by triggering standards mode.

```
<!DOCTYPE html>
```

---

## Formatting

* Paragraphs of text should always be placed in a `<p>` tag. Never use multiple `<br>` tags.
* Items in list form should always be in `<ul>`, `<ol>`, or `<dl>`.
* Every form input that has text attached should utilize a `<label>` tag. Especially radio or checkbox elements.
* Even though quotes around attributes is optional, always put quotes around attributes for readability.
* Avoid trailing slashes in self-closing elements. For example, `<br>`, `<hr>`, `<img>`, and `<input>`.
* Don't set tabindex manually, rely on the browser to set the order.
* All JavaScript should load after content and styles.
* Do NOT minify your HTML.

---

## Tags & Attributes
All tags and attributes must be written in lowercase. All attribute values also need to be lowercase when the text is only to be interpreted by machines.

```
<!-- Correct -->
<img src="dog.jpg" alt="Fido enjoying the dog park.">

<!-- Incorrect -->
<img SRC="dog.jpg" ALT="Fido enjoying the dog park.">
```

---

## Boolean attributes

Many attributes don't require a value to be set, like disabled or checked, so don't set them.

```
<!-- Correct -->
<input type="text" name="email" disabled>

<!-- Incorrect -->
<input type="text" name="email" disabled="disabled">

<!-- Incorrect -->
<input type=text name=email disabled=disabled>
```

---

## Alt & Title Tags
All `<img>` and `<a href="">` tags should have proper alt or title tags. The text should be descriptive of the image or anchor. If the image is non-critical then an empty `alt=""` is allowed. If you have a list with an icon for each item you would leave the `alt` empty instead of forcing a screenreader to read "bullet" a dozen times.

```
<!-- Correct -->
<img src="dog.jpg" alt="Fido enjoying the dog park!">

<!-- Correct -->
<img src="bullet.png" alt="">

<!-- Correct -->
<a href="/explore/" title="Explore beautiful Austin, Texas">Explore</a>

<!-- Incorrect -->
<img src="bullet.png" alt="bullet">

<!-- Extremely Incorrect -->
<img src="bullet.png">
```

---

## Forms

* Wrap radio and checkbox inputs and their text in `<label>`s. No need for `for` attributes here, the wrapping automatically associates the two.
* Form buttons should always include an explicit type. Use primary buttons for the `type="submit"` button and regular buttons for `type="button"`.

---

## Tables

Tables should only be used for the presentation of tabular data. The only exception is of course when coding email templates.

Table headers should always be presented using `<th>` elements. Column headings should always be wrapped in `<thead>` and the table body should always be wrapped in `<tbody>`. If used the table footer should be wrapped in `<tfoot>`. Remember `<tfoot>` goes above `<tbody>` for speed reasons. You want the browser to load the footer before a table full of data.

```
<!-- Correct -->
<table cellpadding="0" cellspacing="0" border="0">
  <thead>
    <tr>
      <th scope="col">Column One</th>
      <th scope="col">Column Two</th>
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

---

---

## Comments

HTML comments should be added on a case-by-case basis. They are primarily used to let the developer know where a certain block of code ends. Comments are not necessary on more-explicit tags, such as <header> or <nav>, but are useful when dealing with <div> tags with different class or id attributes.

```
<!-- Correct -->
<header>
  <div class="content-pane">
    <div class="row">
      <div class="column">
        <p>Sample text</p>
        
      </div>

      <div class="column">
        <p>Sample text</p>

      </div>
    </div> <!-- /.row -->
  </div> <!-- /.content-pane -->
</header>

<!-- Incorrect -->
<header>
  <div class="content-pane">
    <div class="row">
      <div class="column">
        <p>Sample text</p>

      </div>

      <div class="column">
        <p>Sample text</p>

      </div>
    </div> <!-- /.row -->
  </div> <!-- /.content-pane -->
</header>
```

---

## Thanks

* [github.com/styleguide/templates](https://github.com/styleguide/templates)
