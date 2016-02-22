# HTML5 Style Guide

A set of best practices and guidelines for writing HTML. It aims at improving collaboration, code quality, and enabling supporting infrastructure.

## Table of Contents

  1. [General Formatting Rules](#general-formatting-rules)
  1. [HTML Formatting Rules](#html-formatting-rules)
  1. [Boolean Attributes](#boolean-attributes)
  1. [Lean Markup](#lean-markup)
  1. [Forms](#forms)
  1. [Tables](#tables)

## General Formatting Rules

- **Use soft-tabs** with a 2 space indent. Spaces are the only way to guarantee code renders the same in any person’s environment.
- **Use only lowercase.** All code has to be lowercase. This applies to HTML element names, attributes, attribute values (unless text/CDATA), CSS selectors, properties, and property values (with the exception of strings).

  ```html
  <!-- Not recommended -->
  <A HREF="/">Home</A>

  <!-- Recommended -->
  <img src="logo.png" alt="Logo">
  ```

- **Remove trailing white spaces.** Trailing white spaces are unnecessary and can complicate diffs.

  ```html
  <!-- Not recommended -->
  <p>Text line with trailing whitespace</p>_

  <!-- Recommended -->
  <p>Yes please.</p>
  ```
- **Use UTF-8 (without BOM).** Make sure your editor uses UTF-8 as character encoding, without a byte order mark. Specify the encoding in HTML templates and documents via `<meta charset="utf-8">`. Do not specify the encoding of style sheets as these assume UTF-8.
- **Omit the protocol from embedded resources.** Omit the protocol portion (http:, https:) from URLs pointing to images and other media files, style sheets, and scripts.

  ```html
  <!-- Not recommended -->
  <script src="http://www.site.com/script.js"></script>

  <!-- Recommended -->
  <script src="//www.site.com/script.js"></script>
  ```

**[⬆ back to TOC](#table-of-contents)**

## HTML Formatting Rules

- **Use HTML5** document type. HTML5 syntax is preferred for all HTML documents:

  ```html
  <!DOCTYPE html>
  ```
- **Strive to write valid HTML where possible**. Use tools such as the [W3C Nu Html Checker](https://validator.w3.org/nu/) to test.

  ```html
  <!-- Not recommended -->
  <title>Test</title>
  <article>This is a test.

  <!-- Recommended -->
  <!DOCTYPE html>
  <meta charset="utf-8">
  <title>Test</title>
  <article>This is a test.</article>
  ```
- **Keep use of entity references to minimum.** There is no need to use entity references like `&mdash;` `&rdquo;` or `&#x263a;` assuming the same encoding (UTF-8) is used for files and editors as well as among teams. The only exceptions apply to characters with special meaning in HTML (like `<` and `&`) as well as control or “invisible” characters (like no-break spaces).

  ```html
  <!-- Not recommended -->
  The symbol for the copyright is &ldquo;&copy;&rdquo;.

  <!-- Recommended -->
  The symbol for the copyright is “©”.
  ```
- **Use a new line** for every block, list, or table element, and indent every such child element. Also, indent them if they are child elements of a block, list, or table element.
- **Separate structure from presentation and from behavior.** Strictly keep structure (markup), presentation (styling), and behavior (scripting) apart, and try to keep the interaction between the three to an absolute minimum.
- **Omit `type` attributes for style sheets and scripts.** Do not use type attributes for style sheets (unless not using CSS) and scripts (unless not using JavaScript).

  ```html
  <!-- Not recommended -->
  <script src="//www.site.com/script.js" type="text/javascript"></script>

  <!-- Recommended -->
  <script src="//www.site.com/script.js"></script>
  ```
- Paragraphs of text should always be placed in a `<p>` tag. **Never use multiple `<br>` tags.**
- Items in list form should always be wrapped with `<ul>`, `<ol>`, or `<dl>`. Never use a set of `<div>` or `<p>`.
- Every form input that has text attached should utilize a `<label>` tag. **Especially radio or checkbox elements.**
- Even though quotes around attributes is optional, **always put quotes around attributes** (preferably **double quotation marks**) for readability and consistency.

  ```html
  <!-- Not recommended -->
  <a class='button button-secondary'>Button</a>

  <!-- Recommended -->
  <a class="button button-secondary">Correct Button</a>
  ```
- **Avoid writing closing tag comments**, like `<!-- /.element -->`. This just adds to page load time. Plus, most editors have indentation guides and open-close tag highlighting.
- **Avoid trailing slashes in self-closing elements.** For example, `<br>`, `<hr>`, `<img>`, and `<input>`.
- **Don’t set `tabindex` manually** — rely on the browser to set the order for you.

**[⬆ back to TOC](#table-of-contents)**

## Boolean Attributes

Many attributes don’t require a value to be set, like `disabled`, `checked`, `selected`, `autofocus` or `required` so don’t set them.

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

**[⬆ back to TOC](#table-of-contents)**

## Lean Markup

Whenever possible, avoid excessive parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML. For example:

```html
<!-- Not so great -->
<span class="avatar">
  <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```

**[⬆ back to TOC](#table-of-contents)**

## Forms

- Wrap radio and checkbox inputs and their text in `<label>`s. No need for `for` attributes here — the wrapping automatically associates the two.
- Form buttons should always include an explicit `type`. Use primary buttons for the `type="submit"` button and regular buttons for `type="button"`.
- The primary form button must come first in the DOM, especially for forms with multiple submit buttons. The visual order should be preserved with `float: right;` on each button.

**[⬆ back to TOC](#table-of-contents)**

## Tables

Make use of `<thead>`, `<tfoot>`, `<tbody>`, and `<th>` tags (and `scope` attribute) when appropriate. (Note: `<tfoot>` goes above `<tbody>` for speed reasons. You want the browser to load the footer before a table full of data.)

```html
<table summary="A list of orders">
  <thead>
    <tr>
      <th scope="col">Table header 1</th>
      <th scope="col">Table header 2</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Table footer 1</td>
      <td>Table footer 2</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Table body 1</td>
      <td>Table body 2</td>
    </tr>
  </tbody>
</table>
```

**[⬆ back to TOC](#table-of-contents)**
