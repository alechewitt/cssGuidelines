# cssGuidelines
#Utilities
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

## u-utilityName
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


#Components
Syntax: `<componentName>[--modifierName]`

Component driven development offers several benefits when reading and writing HTML and CSS:
* It helps to distinguish between the classes for the root of the component, descendant elements, and modifications.
* It keeps the specificity of selectors low.
* It helps to decouple presentation semantics from document semantics.

You can think of components as custom elements that enclose specific semantics, styling, and behaviour.

## ComponentName
The component's name must be written in camel case.
```
.myComponent { /* … */ }
<article class="myComponent">
  …
</article>
```

## componentName--modifierName
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
