# How to style your block with CSS

## Table of contents

-   [Atomic CSS Framework](#atomic-css-framework)
-   [Aphrodite](#aphrodite)
-   [joinClasses()](#joinclasses)
-   [Inline Styling](#inline-styling)

## Atomic CSS Framework

Atomic is a mobile-first CSS library based on Tachyons for use on Element based Volusion storefronts.

### Individual Stylesheets

-   [box-sizing](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/box-sizing.css)
-   [coordinates](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/coordinates.css)
-   [display](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/display.css)
-   [flexbox](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/flexbox.css)
-   [height](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/height.css)
-   [images](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/images.css)
-   [lists](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/lists.css)
-   [max-width](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/max-width.css)
-   [normalize](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/normalize.css)
-   [overflow](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/overflow.css)
-   [position](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/position.css)
-   [skins](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/skins.css)
-   [spacing](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/spacing.css)
-   [text-align](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/text-align.css)
-   [text-decoration](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/text-decoration.css)
-   [utilities](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/utilities.css)
-   [vertical-align](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/vertical-align.css)
-   [width](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/width.css)
-   [z-index](https://github.com/volusion/element-atomic-css/blob/master/dist/styles/z-index.css)

## Aphrodite

When the Atomic classes just aren't enough to meet your needs, you'll want to write custom styling with Aphrodite. You can view more information on styling your block with Aphrodite [here](../style-a-block-with-aphrodite/README.md).

## `joinClasses()`

`joinClasses` is a helper function that is provided by the SDK and can be found in your block props. It is meant to join your classes together into a single string and contains some extra logic to ensure your class list is clean and free of unintended classes and whitespace.

#### It will:

-   Accept an infinite number of arguments and join them all together with a single space between each one.
-   Remove any unnecessary whitespace that might be caused before, between, or after your final classes.
-   Remove any invalid classes that might be output by bad logic (removes undefined, null, false, and additional whitespace), which is the biggest reason to use it over string literals.

#### How to use it:

```jsx
<div
    className={joinClasses(
        'flex items-center w-100',
        css(
            classes.yourCustomAphroditeClassA,
            classes.yourCustomAphroditeClassB
        ),
        isRequirementMet && 'w-50' // isRequirementMet === false in this example
    )}
/>
```

Output:

```jsx
<div class="flex items-center w-100 dynamic_aphrodite_class"></div>
```

## Inline Styling

Sometimes inline styling is the best option for what you're trying to accomplish, but we recommend against using it when you can. Since you cannot use certain types of CSS with inline styling (ie. media queries) you end up creating yet another place that CSS needs to be tracked in your code. In the end, inline styling is fully supported, so do what works best.
