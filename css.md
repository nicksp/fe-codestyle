# CSS / Sass Style Guide

*Opinionated CSS and Sass code style.* Influenced primarily by Yandex's work on [BEM](https://en.bem.info/method/) and Johnathon Snook's [SMACSS](https://smacss.com/).

## Table of Contents

  1. [Philosophy](#philosophy)
  1. [Terminology](#terminology)
  1. [Resources](#resources)

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

## Resources

- [BEM - Technology for creating web applications](https://en.bem.info/). Official pages.
- [MindBEMding – getting your head ’round BEM syntax](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/). Introduction to BEM.
- [BEMIT: Taking the BEM Naming Convention a Step Further](http://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/). Some useful additions to existing BEM convension.
- [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/). What is a meaningful class name?
- [OOCSS + Sass = The best way to CSS](http://ianstormtaylor.com/oocss-plus-sass-is-the-best-way-to-css/). Some examples of building on existing objects using `@extend` in Sass.
- [Hacks for dealing with specificity](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/). Some more technical details around specificity.

**[⬆ back to TOC](#table-of-contents)**
