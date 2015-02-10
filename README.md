# CSS Guidelines


# General

## Polymer
* Use Polymer layout attirbutes to align elements: https://www.polymer-project.org/docs/polymer/layout-attrs.html
* Use simple Polymer components such as <paper-ripple> for effects
* Discuss usage of more complex Polymer components.

## LESS vs CSS
* Colour functions (eg. darken on hover) should be written in LESS
* Variables will be written in LESS
* The (slightly wooly) guiding principle is to keep things readable: sometimes pure CSS is better for this sometimes LESS is.

## Images
* TODO: Nuke image files.
* TODO: Client branding images should sit on Amazon not in source code.
* Icons can be images because creating icon font is unnecesary work at this stage and it's not the HTML component of the application that causes performance issues.
 

# Structure

## Utilities
Utility classes are low-level structural and positional traits. Utilities can be applied directly to any element; multiple utilities can be used together; and utilities can be used alongside component classes.
Utilities exist because certain CSS properties and patterns are used frequently. For example: floats, containing floats, vertical alignment, text truncation. Relying on utilities can help to reduce repetition and provide consistent implementations. They also act as a philosophical alternative to functional (i.e. non-polyfill) mixins.
```
<div class="u-clearfix">
  <p class="u-textTruncate">{$text}</p>
  <img class="u-pullLeft" src="{$src}" alt="">
  <img class="u-pullLeft" src="{$src}" alt="">
  <img class="u-pullLeft" src="{$src}" alt="">
</div>
```

### u-utilityName
Syntax: `u-<utilityName>`


Utilities must use a camel case name, prefixed with a u namespace. What follows is an example of how various utilities can be used to create a simple structure within a component.

```
<div class="u-clearfix">
  <a class="u-pullLeft" href="{$url}">
    <img class="u-block" src="{$src}" alt="">
  </a>
  <p class="u-sizeFill u-textBreak">
    …
  </p>
</div>
```


## Components
Syntax: `<componentName>[--modifierName]`


Always look to abstract components.


A name like .homepage-nav limits its use. Instead think about writing styles in such a way that they can be reused in other parts of the app. Instead of .homepage-nav, try .nav or .nav-bar. Ask yourself if this component could be reused in another context (chances are it could!). But don't create single use components, ask yourself: is it a reusable component or a specific change? If a specific change, could it be dealt with as a utility?


Components should belong to their own less file. For example, all general button definitions belong in buttons.less.


Component driven development offers several benefits when reading and writing HTML and CSS:
* It helps to distinguish between the classes for the root of the component, descendant elements, and modifications.
* It keeps the specificity of selectors low.
* It helps to decouple presentation semantics from document semantics.


You can think of components as custom elements that enclose specific semantics, styling, and behaviour. We prefer components over page level styles

### ComponentName
The component's name must be written in camel case.
```
.myComponent { /* … */ }
<article class="myComponent">
  …
</article>
```

### componentName--modifierName
A component modifier is a class that modifies the presentation of the base component in some form. Modifier names must be written in camel case and be separated from the component name by two hyphens. The class should be included in the HTML in addition to the base component class.

```
/* Core button */
.btn { /* … */ }
```

```
/* Default button style */
.btn--default { /* … */ }
<button class="btn btn--primary">…</button>
```


## Nesting

Don't nest components. Ever.

Nesting reduces the legibility of css. Instead, be specific in your use of class names, component, modifers and utilities. 

**Wrong:**

```css
.list-btn {
  .list-btn-inner {
    .btn {
      background: red;
    }
    .btn:hover {
      .opacity(.4);
    }
  }
}
```

**Right:**

```CSS
.list-btn .btn-inner {
  background: red;
}
.list-btn .btn-inner:hover {
  .opacity(.4);
}
```

## Style Scoping
Pages should largely be reusing the general component level styles defined above. Page level name-spaces however can be helpful for overriding generic components in very specific contexts. Examples of dealing with page level overrides are shown below 

** WRONG - should use specific modifiers **
```
.home-page {
  .nav {
    margin-top: 10px;
  }
}
```
** RIGHT - two options **
```
.nav-homePage {
	margin-top: 10px;
}
class=“nav nav-homePage”

OR

u-marginTopSmall {
	margin-top: 10px;
}

class=“nav u-marginTopSmall”
```
Which solution is preferred? [Will - I think I prefer the modifier approach to the utility approach as I think different pages will have slightly different spacing requirements which would require an inordinate number of utilities to meet]

# Variables

Syntax: `<property>-<value>`

Variable names in our CSS are also strictly structured. This syntax provides strong associations between property, use, and component.

## Colors
Use RGB and RGBA color units. When implementing styles only use the color variables provided by constants.less and themes.less. Themed colours should be abstracted:

**Wrong**
`color-maroon: RGBA(52,121,34,1)`
**Right**
`color-brand-primary: RGBA(52,121,34,1)`


## Z-Index Scale

Use the z-index scale defined in z-index.less.

`@zIndex-1 - @zIndex-9` are provided. Nothing should be higher then `@zIndex-9`.

## Typography

Use type variables defined in typography.less.

Raw font weights should be avoided. Instead, use the appropriate font mixin: `.font-sansI7, .font-sansN7, etc.`

The suffix defines the weight and style:

```CSS
N = normal
I = italic
4 = normal font-weight
7 = bold font-weight
```

Refer to type.less for type size, letter-spacing, and line height. Raw sizes, spaces, and line heights should be avoided outside of type.less.


```CSS
ex:

@fontSize-micro
@fontSize-smallest
@fontSize-smaller
@fontSize-small
@fontSize-base
@fontSize-large
@fontSize-larger
@fontSize-largest
@fontSize-jumbo
```

# Formatting


## Commenting
* Titles `//== Buttons`
* Subtitles `//## Contains component and modifier button stylings`
* Comments `// Explaining hover effect darkening`


## Spacing

CSS rules should be comma seperated but live on new lines. This probably shouldn't happen anyways as components and modifiers should be used for overlapping styles.

**Right:**
```css
.content,
.content-edit {
  â€¦
}
```

**Wrong:**
```css
.content, .content-edit {
  â€¦
}
```

Within sections, CSS blocks should be seperated by a single blank line. Sections should be seperated by a double line space followed by a section title.

**Right:**
```css
.content {
  â€¦
}

.content-edit {
  â€¦
}
```

**Wrong:**
```css
.content {
  â€¦
}
.content-edit {
  â€¦
}
```

## Quotes

Quotes are optional in CSS and LESS. We use double quotes as it is visually clearer that the string is not a selector or a style property.

**Right:**
```css
background-image: url("/img/you.jpg");
font-family: "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial;
```

**Wrong:**
```css
background-image: url(/img/you.jpg);
font-family: Helvetica Neue Light, Helvetica Neue, Helvetica, Arial;
```


