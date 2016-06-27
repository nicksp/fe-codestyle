# CSS / Sass Style Guide

This document outlines opinionated CSS and Sass code style guide. Influenced primarily by Yandex's work on [BEM](https://en.bem.info/method/) and Johnathon Snook's [SMACSS](https://smacss.com/).

## Table of Contents

  1. [General Formatting Rules](#general-formatting-rules)
  1. [Philosophy](#philosophy)
  1. [Terminology](#terminology)
  1. [BEM 101](#bem-101)
  1. [CSS Formatting Rules](#css-formatting-rules)
  1. [Theming](#theming)
  1. [Sass Specifics](#sass-specifics)
  1. [Resources](#resources)

## General Formatting Rules

- **Use soft tabs** with a 2 space indent. Spaces are the only way to guarantee code renders the same in any person’s environment and improve readability. Always be consistent in your use of whitespace.

  ***Pro tip:*** use an [EditorConfig](http://editorconfig.org/) file (or equivalent) to help maintain the basic whitespace conventions that have been agreed for your code-base. For an example, see [the one in my Redux boilerplate](https://github.com/nicksp/redux-webpack-es6-boilerplate/blob/extended/.editorconfig).

- Add **new line** at end of files.

- **Use only lowercase.** All code has to be lowercase. This applies to CSS selectors, properties, and property values (with the exception of strings).

    ```css
    /* Not recommended */
    color: #E5E5E5;

    /* Recommended */
    color: #e5e5e5;
    ```

- **Remove trailing white spaces.** Trailing white spaces are unnecessary and can complicate diffs.

  ```css
  /* Not recommended */
  .rule {
    color: #1aa;_
  }

  /* Recommended */
  .rule {
    color: #1aa;
  }
  ```
- **Use UTF-8 (without BOM).** Make sure your editor uses UTF-8 as character encoding, without a byte order mark. Do not specify the encoding of style sheets explicitly as these assume UTF-8.
- **Omit the protocol from embedded resources.** Omit the protocol portion (http:, https:) from URLs pointing to images and other media files.

  ```css
  /* Not recommended */
  .example {
    background: url(http://www.site.com/images/example.png);
  }

  /* Recommended */
  .example {
    background: url(//www.site.com/images/example.png);
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Philosophy

In any CSS I write, the goal is to provide code that is:

1. **Abstracted.** Component names shouldn't be derived from the content they contain. Class names should convey structural meaning.
1. **Reusable.** Components should be generic enough to be reused throughout the site. They should make no assumptions what page/view they will be used on. Problems solved in one area should be easily applied elsewhere.
1. **Mixable.** Components should be able to join together to create larger blocks.
1. **Powered by variables.** Nearly all design elements — colors, fonts, spacings, shadows — should be defined using the pre-existing variables.

By achieving these goals our code becomes:

1. **Scalable.** Reusing patterns means new elements can be created faster and with minimal additional CSS.
1. **Consistent.** Not only will developers be able to read each other's code more easily we'll have a better end-user experience across the product.
1. **Smaller and [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself)er.** Since we're constantly reusing low-level objects to build larger ones, often with Sass' <code>@extend</code> functionality, we cut down on CSS bloat. Less code leads to fewer bugs.

**[⬆ back to TOC](#table-of-contents)**

## Terminology

### Writing Good Classes

In order to write HTML and CSS classes that provide meaning for developers I'm using the [BEM](https://en.bem.info/method/key-concepts/) syntax. BEM stands for Block, Element, Modifier and is becoming a popular approach to building CSS and HTML that describes an object's internal relationships.

```html
<ul class="menu menu--top">
  <li class="menu__item">
    menu item
  </li>
  <li class="menu__item">
    menu item
  </li>
  </li>
  <li class="menu__item">
    menu item
  </li>
</ul>
```

In the example above:

- **Block** is represented by <code>menu</code> and is the parent class of the object.
- **Elements** are children of the object. They are named by joining the parent class name and a child class with a double underscore. In this case <code>menu__item</code>.
- **Modifiers** are variations on the default. In this case we have a <code>menu--top</code>. This provides the position for the menu.

Though somewhat verbose, this syntax makes it easy to determine the child/parent relationships between bits of code, especially when different objects are mixed together. It can be tricky naming elements so some judgment is required. This becomes easier with practice.

**[⬆ back to TOC](#table-of-contents)**

## BEM 101

- Benefits:
  * code sharing
  * living style guide
  * scalability
  * faster development
  * eliminating specificity problems (because BEM provides unique class names for most styles, you'd depend only on the order of rules)
  * no more cascades (every BEM CSS class is unique and self-sufficient, doesn't depend on tags or IDs, so we need only a single class name selector to style our BEN entities. In some cases we might need two class names in a selector, when a block modifier affects individual elements, i.e.: *.text-input_disabled .text-input __label {}*)

### Block

A block is an independent entity with its own meaning that represents a piece of interface on a page.

**Examples**
  * Heading
  * Button
  * Menu

To define a block, you'd give it a unique name and specify its semantics. Several instances of the same block definition might be presented on a page.

### Element

An element is an integral part of a block, tied to it semantically and functionally. It has no meaning outside of the block it belongs to. Not all blocks have elements.

**Examples**
  * Menu items of a menu block
  * Form elements (different kind of inputs for example)

### Modifier

Modifiers are states/flags set on blocks or elements. They might be of two types:

  * boolean: `visible`
  * key-value pairs: `size: large`

### DOM

BEM uses CSS class names to denote blocks, elements and modifiers. One DOM node may host several blocks. A node may be an element within one block and a container for another block at the same time. Such scenario is called a "BEM mixin".

### Naming Conventions

- Keep the names of blocks, elements and modifiers short and semantic.
- Use only latin letters, dashes and digits (*words-are-dash-separated*).

Element containers within a block get CSS classes consisting of their block class, two underscores and the element's name:

```css
.text-input__label
.text-input__text-field
```

**Note:** BEM entity can not be represented as an element of another element and the following string representation will be invalid:

```css
.block__elem-1__sub-elem-2
```

Modifiers belong to a block or an element. Their CSS class is the class name of their parent block, one underscore and a modifier name:

```css
.text-input_disabled
.select__option_selected
```

Some modifiers are key-value pairs with more than one possible value. Use another underscore to separate the values:

```css
.heading_level_alpha
```

Modifier classes are used together with the block and element class, like so:

```html
<div class="heading heading_level_alpha">BEM</div>
```

**Note:** Also there is no such BEM entity as a modifier and an element modifier simultaneously so the following string representation will be invalid:

```css
.block_block-mod-name_block-mod-val__elem-name_elem-mod-name_elem-mod-val
```

**[⬆ back to TOC](#table-of-contents)**

## CSS Formatting Rules

- In order to keep specificity low, which I do, **stop using [IDs](http://cssguidelin.es/#ids-in-css) and [cascades](https://en.bem.info/method/solved-problems/#how-to-start-reusing-code-without-letting-components-influence-each-other) in CSS**.
- **Strive to write valid CSS where possible.** Use tools such as the [W3C CSS Validator](http://jigsaw.w3.org/css-validator/) to test.
- Never reference `js-` prefixed class names from CSS files. `js-` are used exclusively from JS files.

  Use the `is-` prefix for state rules that are shared between CSS and JS.
- **Attribute selectors should be used alone**, just like classes. Example: `[type="text"]` vs `input[type="text"]`
- **Use [shorthand properties](https://www.w3.org/TR/CSS21/about.html#shorthand) where possible.** Using shorthand properties is useful for code efficiency and understandability.

  ```css
  /* Not recommended */
  border-top-style: none;
  font-family: georgia, serif;
  font-size: 100%;
  line-height: 1;
  padding-bottom: 2em;
  padding-left: 1em;
  padding-right: 1em;
  padding-top: 0;

  /* Recommended */
  border-top: 0;
  font: 100%/1, georgia, serif;
  padding: 0 1em 2em;
  ```
- Avoid specifying units for zero-values.

  ```css
  margin: 0;
  padding: 0;
  ```
- **Omit leading “0”s in values.** Do not use put 0s in front of values or lengths between -1 and 1.

  ```css
  opacity: .3;
  ```
- **Use 3 character hexadecimal notation where possible.** For color values that permit it, 3 character hexadecimal notation is shorter and more succinct.

  ```css
  /* Not recommended */
  color: #aabbcc;

  /* Recommended */
  color: #abc;
  ```
- **Avoid user agent detection** as well as **CSS “hacks”** — try a different approach first.

- **Use a semicolon after every declaration.** End every declaration with a semicolon for consistency and extensibility reasons.

  ```css
  /* Not recommended */
  .test {
    display: block;
    height: 100px
  }

  /* Recommended */
  .test {
    display: block;
    height: 100px;
  }
  ```

- Use **one level of indentation** for each declaration.

- **Use a space after a property name’s colon.** Always use a single space between property and value (but no space between property and colon) for consistency reasons.

  ```css
  /* Not recommended */
  h3 {
    font-weight :bold;
  }

  /* Recommended */
  h3 {
    font-weight: bold;
  }
  ```

- Include a **single space before the opening brace** of a ruleset.

  ```css
  /* Not recommended: missing space */
  .class{
    margin-top: 1em;
  }

  /* Not recommended: unnecessary line break */
  .class
  {
    margin-top: 1em;
  }

  /* Recommended */
  .class {
    margin-top: 1em;
  }
  ```

- Separate each ruleset by a **blank line**. Include **one declaration per line**, and **one discrete selector per line**.

  ```css
  /* Not recommended */
  html {
    background: #fff;
  }
  a:focus, a:active {
    position: relative; top: 1px;
  }

  /* Recommended */
  .selector-1 {
    background: #fff;
  }

  h1,
  h2,
  h3 {
    font-weight: normal;
    line-height: 1.2;
  }
  ```

- **Declaration order.** If declarations are to be consistently ordered, it should be in accordance with a single, simple principle.

  Smaller teams may prefer to group related properties (e.g. positioning and box-model) together.

  ```css
  .selector {
    /* Positioning */
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    /* Display & Box Model */
    display: block;
    float: right;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;

    /* Typography */
    font: normal 13px "Helvetica Neue", sans-serif;
    line-height: 1.5;
    color: #333;
    text-align: center;

    /* Visual */
    background: #000;
    border: 1px solid #e5e5e5;
    border-radius: 3px;

    /* Other */
    opacity: 1;

    /* Pseudo Classes */
    &:active {
        background: blue;
    }

    &:last-child {
      border-top: 1px solid blue;
    }

    /* Pseudo Elements */
    &::before {
      content: 'CSS Rules!';
    }

    /* Child Elements */
    span {
      font-weight: bold;
    }
  }
  ```

  Larger teams may prefer the simplicity and ease-of-maintenance that comes with alphabetical ordering.

- **Use double quotation marks for attribute selectors and property values.** Double (`""`) over single (`''`). Do not use quotation marks in URI values (`url()`).

  ```css
  /* Not recommended */
  @import url('//www.site.com/app.css');

  html {
    font-family: 'open sans';
  }

  /* Recommended */
  @import url(//www.site.com/app.css);

  input[type="checkbox"]

  html {
    font-family: "open sans";
  }
  ```

- **Media query placement.** Place media queries as close to their relevant rule sets whenever possible. Don't bundle them all in a separate stylesheet or at the end of the document. Doing so only makes it easier for folks to miss them in the future. Here's a typical setup.

  ```css
  .element { }

  @media (min-width: 480px) {
    .element { }
  }
  ```

- Ensure your code is descriptive and well commented. When writing comments, it is best to following a format that makes making changes easy, without having to clutter your code.

  ```css
  /* ==========================================================================
     Section comment block
     ========================================================================== */

  .b-header {
    height: 100%;
    font-size: 1em;
  }

  /* Basic comment */

  .b-header-plate {}

  // OR another format

  // My Component
  // ============
  //
  // Notes:
  //
  // 1. This is a direct comment about why we're using display: block
  // 2. Absolutely positioned relative to the parent .c-my-component

  .c-my-component {
    position: relative; // 2
    display: block; // 1

    .some-child {
      position: absolute; // 2
    }
  }


  // My Component: Inner
  // -------------------
  //
  // Notes:
  //
  // 1. We see the number 1 again! But this note only counts for the code below and ignore the 1 above

  .c-my-component__inner {
    display: block; // 1
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Theming

When creating theme styles try to stick to these rules:

- Create a `themes.scss` in the `/scss` directory
- Create a `/theme` directory, in which you will create directories like: `/components`, `/templates`, and any other directories you deem necessary.

So your newly created files and directories should look like the follow (existing files excluded):

```css
/scss
    themes.scss
    /themes
        /components
        /templates
```

Any theme styles you write should go in their appropriate directory in `/themes`. For example, if a `product-list` component is themed, it would belong in `/scss/themes/components/_product-list.scss`.

Any SCSS files created in the `/themes` directory should be formatted as follows

```css
.x-theme-class-name {
  .c-component-class-name {
    // ...
  }
}
```

The `.x-theme-class-name` is basically a global state that we are expecting to be applied on either the HTML, body, or other top level container.

**[⬆ back to TOC](#table-of-contents)**

## Sass Specifics

- Use the `.scss` syntax, never the original `.sass` syntax.
- **Nesting.** As a rule of thumb, avoid unnecessary nesting in `SCSS`. Just because you can nest, doesn't mean you always should. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested. At most, aim for three (3) levels deep.

  ```css
  .page-container {
    .content {
      .card {
        // STOP HERE
      }
    }
  }
  ```

- **Variables.** Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$_my-variable`).
- **Mixins.** Mixins should be used to DRY up your code, add clarity, or abstract complexity -- in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.
- **Global vs. Local Variables/Mixins** Any `$variable` that is used in more than one file should be placed in the `/variables.scss` file. Others should be placed at the top of the file in which they're used. Any `@mixin` that is used in more than one file should be placed in the `/utilities` folder.
- **Extend.** `@extend` directives [should be](http://csswizardry.com/2014/11/when-to-use-extend-when-to-use-a-mixin/) [avoided](http://csswizardry.com/2014/01/extending-silent-classes-in-sass/) because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts).
- **Filename naming convention** The file naming convention should be identical to the class naming convention as described above, but with the following difference:
    - Sass files (technical scss files) should be a Sass partial (prepended with a underscore `_`)
    - Sass files are named after it's root class name
        - the filename can be named after the grouping of elements (Example `ul`, `ol` and `li` can be grouped together in `_list.scss`)
        - in case of a component, the base component will be the filename (i.e. `color-picker` makes `_color-picker.scss`)
- **Operators.** For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.

  ```css
  /* Not recommended */
  .element {
    margin: 10px 0 @variable*2 10px;
  }

  /* Recommended */
  .element {
    margin: 10px 0 (@variable * 2) 10px;
  }
  ```

- **Including (S)CSS files.** Use explicit lists of imports to control the cascade, specificity, and more.

  ```css
  // Imports
  @import "base";
  @import "component";
  @import "another-component";

  // Rules
  .rule { ... }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Resources

- [BEM - Technology for creating web applications](https://en.bem.info/). Official pages.
- [MindBEMding – getting your head ’round BEM syntax](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax). Introduction to BEM.
- [BEMIT: Taking the BEM Naming Convention a Step Further](http://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further). Some useful additions to existing BEM convension.
- [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/). What is a meaningful class name?
- [OOCSS + Sass = The best way to CSS](http://ianstormtaylor.com/oocss-plus-sass-is-the-best-way-to-css/). Some examples of building on existing objects using `@extend` in Sass.
- [CSS: the cascade, specificity, and inheritance](http://nicolasgallagher.com/css-cascade-specificity-inheritance/). Some basic knowledge on important CSS terminology.
- [Hacks for dealing with specificity](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity). Some more technical details around specificity.

**[⬆ back to TOC](#table-of-contents)**
