# ui-sortable directive [![Build Status](https://travis-ci.org/angular-ui/ui-sortable.png)](https://travis-ci.org/angular-ui/ui-sortable)

This directive allows you to sort array with drag & drop.

## Requirements

- JQuery
- JQueryUI
- AngularJS 1.0.x

**Note for AngularJS 1.2 users:** Use the separate branch `angular1.2`.

## Usage

Load the script file: sortable.js in your application:

```html
<script type="text/javascript" src="modules/directives/sortable/src/sortable.js"></script>
```

Add the sortable module as a dependency to your application module:

```js
var myAppModule = angular.module('MyApp', ['ui.sortable'])
```

Apply the directive to your form elements:

```html
<ul ui-sortable ng-model="items">
  <li ng-repeat="item in items">{{ item }}</li>
</ul>
```

**Note:** `ng-model` is required, so that the directive knows which model to update.

### Options

All the jQueryUI Sortable options can be passed through the directive.


```js
myAppModule.controller('MyController', function($scope) {
  $scope.items = ["One", "Two", "Three"];

  $scope.sortableOptions = {
    update: function(e, ui) { ... },
    axis: 'x'
  };
});
```

```html
<ul ui-sortable="sortableOptions" ng-model="items">
  <li ng-repeat="item in items">{{ item }}</li>
</ul>
```

#### Canceling

Inside the `update` callback, you can check the item that is dragged and cancel the sorting.

```js
$scope.sortableOptions = {
  update: function(e, ui) {
    if (ui.item.scope().item == "can't be moved") {
      ui.item.parent().sortable('cancel');
    }
  }
};
```

**Note:** `update` occurs before any model/scope changes but after the DOM position has been updated.
So `ui.item.scope` and the directive's `ng-model`, are equal to the scope before the drag start.

## Reporting Issues

The following pen's are provided as a good starting point to demonstrate issues, proposals and use cases.
Feel free to edit any of them for your needs (don't forget to also update the libraries used to your version).

- [Simple Demo](http://codepen.io/thgreasi/pen/BlFLp)
- [Connected Lists](http://codepen.io/thgreasi/pen/apwsb)
