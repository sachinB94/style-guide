# ES5 Style Guide

*Something I came up with - Nothing fancy*
*(Will keep on adding more)*


## Table of Contents

  1. [Variables](#variables)
  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Functions](#functions)
  1. [Naming Conventions](#naming-conventions)
  1. [Comparison Operators & Equality](#comparison-operators--equality)
  1. [Blocks](#blocks)
  1. [Comments](#comments)
  1. [Whitespace](#whitespace)
  1. [Semicolons](#semicolons)
  1. [License](#license)

## 1. Variables

  - Declare all the variables and constants before using them. Preferably at the top of their scope

    ```javascript
    // bad
    function() {
      console.log('hello');

      var foo = 1;

      console.log('It\'s foo ', foo);
    }

    // good
    function() {
      var foo = 1;

      console.log('hello');

      console.log('It\'s foo ', foo);
    }
    ```

  - Always use 'var' for variable declaration. Avoid polluting the global namespace

    ```javascript
    // bad
    foo = 'abc';

    // good
    var foo = 'abc';
    ```

  - Always use one 'var' declaration for each variable.

    ```javascript
    // bad
    var foo = 1,
      bar = 2;

    // good
    var foo = 1;
    var bar = 2;
    ```

  - Avoid comma first syntax

    ```javascript
    // bad
    var foo = [
      name: 'abc'
    , addr: 'xyz'
    , ph: 9876543210
    ];

    // good
    var foo = [
      name: 'abc',
      addr: 'xyz',
      ph: 9876543210
    ];
    ```

**[⬆ back to top](#table-of-contents)**


## Objects

  - Use the literal syntax for object creation.

    ```javascript
    // bad
    var foo = new Object();

    // good
    var foo = {};
    ```

  - Use dot notation to access properties of an object
    
    ```javascript
    // bad
    foo['bar'] = 'xyz';

    // good
    foo.bar = 'xyz';
    ```
  - Use subscript notation [] to access properties with a variable
    
    ```javascript
    var prop = 'bar';

    console.log(foo[prop]);
    ```

**[⬆ back to top](#table-of-contents)**


## Arrays

  - Use the literal syntax for array creation.

    ```javascript
    // bad
    var foo = new Array();

    // good
    var foo = [];
    ```

  - Use Array#push instead of direct assignment to add items to an array.

    ```javascript
    var foo = [];

    // bad
    foo[foo.length] = 1;

    // good
    foo.push(1);
    ```

**[⬆ back to top](#table-of-contents)**


## Strings

  - Use single quotes `''` for strings.

    ```javascript
    // bad
    var foo = "abc";

    // good
    var foo = 'abc';
    ```

  - Strings longer than 100 characters should be written across multiple lines using string concatenation.

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```

**[⬆ back to top](#table-of-contents)**


## Functions

  - Function expressions:

    ```javascript
    // anonymous function expression
    var foo = function() {
      return true;
    };

    // named function expression
    var foo = function foo() {
      return true;
    };

    // immediately-invoked function expression (IIFE)
    (function() {
      console.log('You can\'t stop me');
    })();
    ```

**[⬆ back to top](#table-of-contents)**


## Naming Conventions

  - Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - Use camelCase when naming objects, functions, variables, and instances.

    ```javascript
    // bad
    var ThisIsObject = {};
    var this_is_also_a_object = {};

    // good
    var thisIsObject = {};
    var thisIsAlsoAObject = {};
    ```

  - Use PascalCase when naming constructors or classes.

    ```javascript
    // bad
    function user(name) {
      this.name = name;
    }

    var bad = new user('nope');

    // good
    function User(name) {
      this.name = name;
    }

    var good = new User('yup');
    ```

  - Use UPPERCASE when naming constants.

    ```javascript
    // bad
    var thisIsAConstant = 'abc';
    var this_is_also_a_constant = 'xyz';

    // good
    var THIS_IS_A_CONSTANT = 'abc';
    ```

  - Use a leading underscore `_` when naming private properties.

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';

    // good
    this._firstName = 'Panda';
    ```

  - When saving a reference to `this` use `_this`.

    ```javascript
    // bad
    function() {
      var self = this;
      return function() {
        console.log(self);
      };
    }

    // good
    function() {
      var _this = this;
      return function() {
        console.log(_this);
      };
    }
    ```

  - If your file exports a single class, your filename should be exactly the name of the class.
    ```javascript
    // file contents
    class CheckBox {
      // ...
    }
    module.exports = CheckBox;

    // in some other file
    // bad
    var CheckBox = require('./checkBox');

    // bad
    var CheckBox = require('./check_box');

    // good
    var CheckBox = require('./CheckBox');
    ```

**[⬆ back to top](#table-of-contents)**


## Comparison Operators & Equality

  - Use `===` and `!==` over `==` and `!=`.
  - Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    + **Objects** evaluate to **true**
    + **Undefined** evaluates to **false**
    + **Null** evaluates to **false**
    + **Booleans** evaluate to **the value of the boolean**
    + **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - Use shortcuts.

    ```javascript
    // bad
    if (name !== '') {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Blocks

  - Use braces with all the blocks (even single line `if` statements).

    ```javascript
    // bad
    if (test)
      return false;

    // bad
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function() { return false; }

    // bad
    function()
    {
      return false;
    }

    // good
    function() {
      return false;
    }
    ```

  - If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your
    `if` block's closing brace.

    ```javascript
    // bad
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Comments

  - Use `//` for all comments whether multi-line or single-line comments. Also, leave a single line before a comment.

    ```javascript
    // bad
    var active = true;  // is current tab

    // good
    // is current tab
    var active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }
    ```

  - Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME -- need to figure this out` or `TODO -- need to implement`.

  - Use `// FIXME:` to annotate problems.

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

  - Use `// TODO:` to annotate solutions to problems.

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Whitespace

  - Use soft tabs set to 2 spaces.

    ```javascript
    // bad
    function() {
    ∙∙∙∙var name;
    }

    // bad
    function() {
    ∙var name;
    }

    // good
    function() {
    ∙∙var name;
    }
    ```

  - Place 1 space before the leading brace.

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });
    ```

  - Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space before the argument list in function calls and declarations.

    ```javascript
    // bad
    if(isJedi) {
      fight ();
    }

    // good
    if (isJedi) {
      fight();
    }

    // bad
    function fight () {
      console.log ('Swooosh!');
    }

    // good
    function fight() {
      console.log('Swooosh!');
    }
    ```

  - Set off operators with spaces.

    ```javascript
    // bad
    var x=y+5;

    // good
    var x = y + 5;
    ```

  - End files with a single newline character.

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);
    ```

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);↵
    ↵
    ```

    ```javascript
    // good
    (function(global) {
      // ...stuff...
    })(this);↵
    ```

  - Leave a blank line after blocks and before the next statement

    ```javascript
    // bad
    if (foo) {
      return bar;
    }
    return baz;

    // good
    if (foo) {
      return bar;
    }

    return baz;

    // bad
    var obj = {
      foo: function() {
      },
      bar: function() {
      }
    };
    return obj;

    // good
    var obj = {
      foo: function() {
      },

      bar: function() {
      }
    };

    return obj;
    ```

**[⬆ back to top](#table-of-contents)**


## Semicolons

  - **Yup.**

    ```javascript
    // bad
    (function() {
      var name = 'Skywalker'
      return name
    })()

    // good
    (function() {
      var name = 'Skywalker';
      return name;
    })();

    ```

**[⬆ back to top](#table-of-contents)**



## License

(The MIT License)

Copyright (c) Sachin Bansal

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**
