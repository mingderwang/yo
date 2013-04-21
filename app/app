/*
  <div first-directive></div>
    <div directive-with-attrs dir-value="yo"></div>
    <div directive-with-interpolated-attrs dir-value="yo, {{someValue}}"></div>
    <div directive-with-isolate-scope dir-attr-value="Yo!" dir-incoming-value="someValue" dir-incoming-function="someFunc" dir-incoming-interpolation="Hi {{someOtherValue}}"></div>
    <div class="css-directive"></div>
    <div class="css-directive-with-value: Something"></div>
    <sixth-directive></sixth-directive>
    <div seventh-directive></div>

  */
angular.module("directives", [])
  .directive("firstDirective", function() {
    return function(scope, element) {
      element.text("Basic");
    };
  })
  .directive("directiveWithAttrs", function() {
    return function(scope, element, attrs) {
      element.text(attrs.dirValue);
    };
  })
  .directive("directiveWithInterpolatedAttrs", function() {
    return function(scope, element, attrs) {
      attrs.$observe("dirValue", function(newVal) {
        element.text(newVal);
      });
    };
  })
  .directive("directiveWithIsolateScope", function() {
    return {
      scope: {
        content: "=dirIncomingValue",
        thisFunc: "&dirIncomingFunction"
      },
      template:"{{content}} <button ng-click=\"thisFunc()('foo!')\">Click me to reset someValue</button>"
    };
  })
  .directive("cssDirective", function() {
    return {
      restrict: "C",
      link: function(scope, element) {
        element.text("CSS-Basic");
      }
    };
  })
  .directive("cssDirectiveWithValue", function() {
    return {
      restrict: "C",
      link: function(scope, element, attrs) {
        element.text(attrs.cssDirectiveWithValue);
      }
    };
  })
  .directive("elementDirective", function() {
    return {
      restrict: "E",
      link: function(scope, element, attrs) {
        element.text("Element Level!  Woot!");
      }
    };
  })
  .service("myService", function() {
    this.value = "IM IN UR SERVCS!";
  })
  .directive("directiveInjectedWithService", function(myService) {
    return {
      link: function(scope, element, attrs) {
        element.text(myService.value);
      }
    };
  })
  .controller("fooController", function($scope, $element, $attrs) {
    this.foo = function(source) {
      $element.append("I've been foo'ed by " + source + "!");
    };
  })
  .directive("directiveWithController", function() {
    return {
      controller: function($scope, $element, $attrs) {
        this.foo = function() {
          $element.append("I've been foo'ed!");
        };
      }
    };
  })
  .directive("directiveRequiringController", function() {
    return {
      require:"^directiveWithController",
      template: "<button ng-click=\"clickMe()\">Foo that crazy controller</button>",
      scope: true,
      link: function(scope, element, attrs, controller) {
        scope.clickMe = function() {
          controller.foo(attrs.source);
        };
      }
    };
  })
  .directive("directiveWithCompile", function(myService) {
    return {
      compile: function(tEl, tAttr) {
        tEl.text("IM IN UR COMPILE!!!");
        return function(scope, element, attrs) {
          tEl.append("Now I'm in your Linking Function, though!");
        };
      }
    };
  })
  .directive("directiveWithModifiedCloning", function(myService) {
    return {
      compile: function(tEl, tAttr) {
        var i = 1;
        tEl.text("IM IN UR COMPILE!!!");
        return function(scope, element, attrs) {
          tEl.text("I've been cloned " + (i++) + " times!");
        };
      }
    };
  })
  .directive("directiveWithPreLink", function(myService) {
    return {
      template:"<div first-directive>Thing1</div><div first-directive>Thing2</div>",
      compile: function(tEl, tAttr) {
        return {
          pre: function(scope, el, attrs) {
            el.children().eq(1).append("Bleah!");
          },
          post: function(scope, el, attrs) {
            
          }
        };
      }
    };
  })
  .directive("directiveWithPostLink", function(myService) {
    return {
      template:"<div first-directive>Thing1</div><div first-directive>Thing2</div>",
      compile: function(tEl, tAttr) {
        return {
          pre: function(scope, el, attrs) {
            
          },
          post: function(scope, el, attrs) {
            el.children().eq(1).append("Bleah!");
          }
        };
      }
    };
  });