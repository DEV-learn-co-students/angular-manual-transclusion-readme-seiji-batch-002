# Manual and isolate transclusion

## Overview

Now that we know what transclusion does, we can look into more advanced methods of implementing it. Let's take a look how to transclude our content manually.

## Objectives

- Use the transclude function inside the link function

## transclude()

We can also use the fifth function provided in our `link` function - `transclude`. This function returns our transcluded content as an actual DOM element. This allows us to manually append our elements into our directives instead.

We might want to use this when we want to transform the transcluded elements depending on attributes. For instance, we could remove a `<button>` if the attribute disabled is present.

```js
function ourDirective() {
  return {
    transclude: true,
    template: [
      '<div class="ourDirective">',
        'The content of our directive is: <span></span>',
      '</div>'
    ].join(''),
    link: function (scope, element, attrs, ctrl, transclude) {
        // transclude() = DOM elements
    }
  };
}

angular
  .module('app', [])
  .directive('ourDirective', ourDirective);
```

Now that we've got the transcluded elements as actual DOM elements and also our whole directive element (the `element` variable), we can insert our transcluded content wherever we want. If we want to put it into the span, we can do this:

```js
function ourDirective() {
  return {
    transclude: true,
    template: [
      '<div class="ourDirective">',
        'The content of our directive is: <span></span>',
      '</div>'
    ].join(''),
    link: function (scope, element, attrs, ctrl, transclude) {
        element.find('span').after(transclude());
    }
  };
}

angular
  .module('app', [])
  .directive('ourDirective', ourDirective);
```

Awesome! This puts our transcluded content inside the `<span />`.
