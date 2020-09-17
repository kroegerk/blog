---
eleventyNavigation:
  key: Python Compared to JavaScript
  parent: Python
layout: topic-layout.njk
---

This compares the most commonly used features of Python and JavaScript.
Lesser used features are omitted.

## Overview

| Topic                   | Python                                                                                                                                 | JavaScript                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| standard                | {% aTargetBlank "https://docs.python.org/3/", "Python 3 documentation" %}                                                              | {% aTargetBlank "https://www.ecma-international.org/publications/standards/Ecma-262.htm", "ECMAScript" %} |
| evaluation              | dynamic                                                                                                                                | dynamic                                                                                                   |
| performance             | slow                                                                                                                                   | fast                                                                                                      |
| style guide             | {% aTargetBlank "https://www.python.org/dev/peps/pep-0008/", "PEP 8" %}, {% aTargetBlank "https://pypi.org/project/black/", "Black" %} | {% aTargetBlank "https://prettier.io/", "Prettier" %}                                                     |
| most common indentation | 4 spaces                                                                                                                               | 2 spaces                                                                                                  |
| type coercion           | must be explicit                                                                                                                       | implicit                                                                                                  |

Once source of performance benchmarks can be found at
{% aTargetBlank
"https://benchmarksgame-team.pages.debian.net/benchmarksgame/which-programs-are-fastest.html",
"The Computer Language Benchmarks Game" %}.

## Pros and Cons

### JavaScript

pros:

- performance
- ability to run in web browsers (clients) and from command-line (servers)
- great support for asynchronous code
- more compact syntax for functional programming (ex. functools vs. `reduce`)
- can use TypeScript, a superset of JavaScript, to add type checking

cons:

- still in transition from require to import syntax in Node.js
- type coercions can result in surprising results if not familiar with them

### Python

pros:

- targeted at scripting and rapid application development
- quantity and maturity of libraries for machine learning
- multiple number types
- some syntax is easier for beginners
  - ex. `and` vs. `&&`.
  - ex. `print` vs. `console.log`
  - fewer parentheses and no curly braces or semicolons
- can add functions implemented in C/C++ or any language callable from C

cons:

- poor performance
- magic methods (a.k.a. "dunder" for double underscore) such as `__init__`
  (see list in "Python Magic Methods" section)
- operator overloading (supported by magic methods)
- lots of documentation and examples are still for V2 instead of V3
- anonymous functions are limited to a single expression
- no built-in support for asynchronous code
  until the asyncio module was added in Python 3.4
  (some features require Python 3.7+)
- ternary operator is not supported; for example:

  ```python
  name = len(sys.argv) > 1 ? sys.argv[1] : 'World' # not supported
  name = sys.argv[1] || 'World' # doesn't work
  name = sys.argv[1] if len(sys.argv) > 1 else 'World' # works
  ```

## Getting Help

In Python, enter the `python` command to start the REPL and enter `help`.
To get help on a particular library, import it and pass the name to help.
For example:

```python
import re
help(re)
```

In JavaScript, perform web searches that begin with "MDN"
(for the Mozilla Developer Network) followed by a JavaScript search term.
For example, "mdn regexp".

## Comments

| Type        | JavaScript | Python |
| ----------- | ---------- | ------ |
| single-line | //         | #      |
| multi-line  | /\* \*/    | none   |

## Types

| Type                 | JavaScript                                           | Python                                             |
| -------------------- | ---------------------------------------------------- | -------------------------------------------------- |
| boolean              | `true`, `false`                                      | `True`, `False`                                    |
| number               | default is double precision float; also `BigInt`     | `int`, `float`, `complex`                          |
| character            | use string type                                      | use string type                                    |
| string               | `'text'` or `"text"`                                 | same                                               |
| multi-line string    | `` `text` ``                                         | `"""text"""` or `'''text'''`                       |
| string interpolation | `` `prefix${expr}suffix` ``                          | `f'prefix{expr}suffix'`                            |
| array                | `Array`, `[v1, v2, ...]`                             | see list, tuple, and range                         |
| list                 | see `Array`                                          | `[v1, v2, ...]`; mutable and homogeneous           |
| tuple                | no equivalent                                        | `(v1, v2, ...)`; immutable and heterogeneous       |
| range                | no equivalent                                        | range range(start, stop[, step])                   |
| key/value pairs      | Object in the form `{k1: v1, k2: v2, ...}` and `Map` | dictionary in the form `{'k1': v1, 'k2': v2, ...}` |
| set                  | `new Set()`                                          | `{v1, v2, ...}` or `set(v1, v2, ...)`              |
| function             | see "Function" section below                         | see "Function" section below                       |
| class                | `class Name { ... }`                                 | `class Name:`                                      |
| no value             | `undefined` or `null`                                | `None`                                             |

In Python, the following values are treated as false when used
in a boolean context: False, None, 0, '', and empty sequences.

In JavaScript, the following values are treated as false when used
in a boolean context: false, 0, '', undefined, null.

Python has sequences whereas JavaScript has arrays.
There are three kinds of sequences: list, tuple, and range.
A list is a mutable sequence of values that have the same type.
A tuple is an immutable sequence of values that have varying types.
A range is an immutable sequence of numbers that can be used for looping.

A named tuple gives a name to a tuple type and
supports accessing elements in instances by name.
For example:

```python
from collections import namedtuple
# Internally, this generate a class named Person.
Dog = namedtuple('Dog', 'name breed')
dog = Dog('Comet', 'Whippet')
print(dog.name) # Comet
print(dog[1]) # Whippet
print(len(dog)) # 2
```

JavaScript object keys must be strings.
Python dict keys can e any immutable type.

## Naming Conventions

| Kind                        | JavaScript   | Python         |
| --------------------------- | ------------ | -------------- |
| constant                    | UNDER_SCORES | same           |
| variable                    | camelCase    | under_scores   |
| function                    | camelCase    | under_scores   |
| class                       | CamelCase    | same           |
| method                      | camelCase    | under_scores   |
| public instance properties  | camelCase    | under_scores   |
| private instance properties | camelCase    | \_under_scores |

Python uses a naming convention (all uppercase) to identify constants,
but they can still be modified.
JavaScript and Python class names

## Printing

| Operation                | JavaScript                                                                               | Python                                                |
| ------------------------ | ---------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| print values             | `console.log(v1, v2, ...);`                                                              | `print(v1, v2, ..)`                                   |
| print error              | `console.error(message);`                                                                | `import sys`<br>`print(v1, v2, ..., file=sys.stderr)` |
| print with interpolation | `console.log(`Hello, ${name}, today is ${dayOfWeek}.`);`                                 | print(f'Hello, {name}, today is {dayOfWeek}.')        |
| print without newline    | in Node<br>`const process = require('process');`<br>`process.stdout.write(v1, v2, ...);` | `print(v1, v2, ..., end='')`                          |

## Variables and Assignment

JavaScript variables should be declared
using either the `const` or `let` keyword.
Python variables are not declared and
are created when a value is assigned to them.

| Topic                | JavaScript                      | Python           |
| -------------------- | ------------------------------- | ---------------- |
| constant declaration | `const NAME = value;`           | `NAME = value`   |
| variable declaration | `let name = value;`             | `name = value`   |
| multiple assignment  | const [a, b] = [1, 2]           | a, b = 1, 2      |
| spread of array/list | `const [v1, v2, ...] = array;`  | `v1, v2 = array` |
| spread of object     | `const {k1, k2, ...} = object;` | not supported    |
| addition             | `name += expr`                  | same             |
| subtraction          | `name -= expr`                  | same             |
| multiplication       | `name \*= expr`                 | same             |
| division             | `name /= expr`                  | same             |
| exponentiation       | `name \*\*= expr`               | same             |
| mod (remainder)      | `name %= expr`                  | same             |
| logical and          | `name &&= expr`                 | not supported    |
| logical or           | `name \|\|= expr`               | not supported    |
| logical xor          | `name ^= expr`                  | not supported    |
| bitwise and          | `name &= expr`                  | same             |
| bitwise or           | `name \|= expr`                 | same             |
| bitwise xor          | `name ^= expr`                  | same             |
| signed bit shift     | `<<=` (left), `>>=` (right)     | same             |
| unsigned bit shift   | `<<<=` (left), `>>>=` (right)   | not supported    |

## Comparison

| Topic                 | JavaScript                              | Python   |
| --------------------- | --------------------------------------- | -------- |
| equal for non-objects | `==` (with coercion) or `===` (without) | `==`     |
| equal of objects      | `===`                                   | `is`     |
| not equal of objects  | `!==`                                   | `is not` |
| not equal             | `!=` (with coercion) or `!==` (without) | `!=`     |
| less than             | `<`                                     | same     |
| less than or equal    | `<=`                                    | same     |
| greater than          | `>`                                     | same     |
| greater than or equal | `>=`                                    | same     |

## Conditional Logic

In the JavaScript syntax below, `sOrB` is short for "statement or block".
It can be a single statement or a set of statements surrounded by curly braces.

A Python `if` statement can contain any number of `elif` parts.

| Topic   | JavaScript                                          | Python                                            |
| ------- | --------------------------------------------------- | ------------------------------------------------- |
| if      | `if (cond) sOrB`                                    | `if cond: block`                                  |
| if/else | `if (cond) sOrB1 else sOrB2`                        | `if cond: block1 else: block2`                    |
| if/else | `if (cond1) sOrB1 else if (cond2) sOrB2 else sOrB3` | `if cond: block1 elif cond2: block2 else: block3` |
| ternary | `cond ? trueValue : falseValue`                     | `trueValue if cond else falseValue`               |

## Iteration

Python "dictionaries" (or dicts) are used to store key/value pairs.
In JavaScript this is done with plain objects
or the `Map` class (described later).

| Topic                            | JavaScript                                                           | Python                                   |
| -------------------------------- | -------------------------------------------------------------------- | ---------------------------------------- |
| classic                          | `for (let var = initial; cond; statements)`                          | `for var in range(start, stop[, step]):` |
| over collection                  | `for (const value of iterable)`                                      | `for value in sequence:`                 |
| over object/dict keys            | `for (const key of Object.keys(obj))`<br>or `for (const key in obj)` | `for key in dict.keys():`                |
| over object/dict values          | `for (const value of Object.values(obj))`                            | `for value in dict.values():`            |
| over object/dict keys and values | `for (const [key, value] of Object.entries(obj))`                    | `for key, value in dict.items():`        |
| top-tested                       | `while (cond)`                                                       | `while cond:`                            |
| bottom-tested                    | `do { ... } while (cond);`                                           | `while True: ... if !cond: break`        |
| break out of closes loop         | `break`                                                              | same                                     |
| continue to next iteration       | `continue`                                                           | same                                     |

## Functions

In JavaScript, functions can be defined in two ways.

```js
// Named function
function myFn(args) {
  body;
}

// Anonymous function (a.k.a. arrow function)
const myFn = args => {
  body;
};
```

If an anonymous function has exactly one named argument,
the parentheses around it are optional.
If an anonymous function simply returns the value of a single expression,
The curly braces around the body and the `return` keyword are optional.

In Python, functions can be defined in two ways.

```python
# Named function
def myFn:
  body

# Lambda function
lambda args: expression
```

Python lambda functions can only return the value of a single expression.
They cannot contain additional statements.

Python named functions can have a docstring as their first line.
This is used by tools that generate documentation from code.
It is typically delimited by triple quotes.
For guidelines on the content of docstrings, see the
{% aTargetBlank
  "https://docs.python.org/3/tutorial/controlflow.html#documentation-strings",
  "Python Tutorial" %} and
{% aTargetBlank
  "https://www.python.org/dev/peps/pep-0008/#documentation-strings",
  "PEP-8 documentation strings" %}.

In Python:

- Function parameters with a default value must follows those without one.
- Function parameters that do not begin with `*` or `**` are positional.
- Function parameters can be specified positionally or by name,
  but positional ones must be specified before named ones.
- The `partial` function (shown in the table below)
  can only be used on functions, not methods of a class.

| Operation                                                           | JavaScript                                                   | Python                                                                                                           |
| ------------------------------------------------------------------- | ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| define named                                                        | `function fnName(params) { definition }`                     | `def fnName(params):`                                                                                            |
| define anonymous                                                    | `const fnName = (params) => definition`                      | `lambda params: expression`                                                                                      |
| define anonymous w/ single parameter                                | `const fnName = param => {...}`                              | same as above                                                                                                    |
| define anonymous w/ single expression                               | `const fnName = (params) => expr`                            | same as above                                                                                                    |
| use variable arguments                                              | `function fnName(p1, p2, ...rest) {...}`                     | `def fnName(p1, p2, *rest):`<br>`rest` is set to a tuple                                                         |
| specify default argument values                                     | `function fnName(p1=v1, p2=v2) {...}`                        | `def fnName(p1=v1, p2=v2):`                                                                                      |
| use named/keyword arguments                                         | `function fnName({p1, p2}) {...}` - pass an object           | same as above<br>any parameter with a default value can be specified by name<br>call with `fnName(p1=v2, p2=v2)` |
| gather arguments as key/value pairs                                 | not supported                                                | `def fnName(**args):`<br>call with `fnName(p1=v2, p2=v2)`<br>or `fnName(**dict)`                                 |
| return a value                                                      | `return value;`                                              | `return value`                                                                                                   |
| default return value when no `return`                               | `undefined`                                                  | `None`                                                                                                           | value` |
| call                                                                | `fnName(args)`                                               | same                                                                                                             |
| get required parameter count                                        | `fnName.length`                                              | `from inspect import getfullargspec`<br>`len(getfullargspec(fn).args)`                                           |
| passing fewer arguments than positional parameters                  | remaining are assigned `undefined`                           | results in an error                                                                                              |
| passing more arguments than positional parameters with no gathering | all arguments are available in `arguments` array-like object | results in an error                                                                                              |
| get name                                                            | `fnName.name`                                                | `fnName.__name__`                                                                                                |
| get implementation code                                             | `fnName.toString()`                                          | `from inspect import getsource`<br>`getsource(fn)`                                                               |
| create partial                                                      | `const newFn = fnName.bind(thisArg, arg1, arg2, ...)`        | `from functools import partial`<br>`newFn = partial(fn, arg1, arg2, ...)`                                        |
| call                                                                | `fnName.call(thisArg, arg1, arg2, ...)`                      | `method(obj, arg1, arg2, ...)`                                                                                   |
| apply                                                               | `fnName.apply(thisArg, argArray)`                            | `method(obj, *argList)`                                                                                          |
| spreading arguments                                                 | fnName(...arr)                                               | fnName(\*seq)                                                                                                    |

## Classes

| Topic                             | JavaScript                                 | Python                                                      |
| --------------------------------- | ------------------------------------------ | ----------------------------------------------------------- |
| defining                          | `class Name { ... }`                       | `class Name:`                                               |
| inheritance                       | `class Sub extends Super { ... }`          | `class Sub(Super1, Super2, ...)`                            |
| constructor                       | `constructor(params) { ... }`              | `def \_\_init\_\_(self, params):`                           |
| instance property declaration     | not declared; set in constructor on `this` | not declared; set in \_\_init\_\_ on `self`                 |
| instance property reference       | `this.propName`                            | `self.propName`                                             |
| class/static property declaration | `static propName = value;`                 | `propName = value;`                                         |
| class/static property reference   | `CName.propName`                           | `CName.propName` or `instance.propName`                     |
| instance method                   | `name(params) { ... }`                     | `def fnName(self, params):`                                 |
| class/static method declaration   | `static methodName(params) { ... }`        | `@staticmethod`<br>`def methodName(params):`                |
| class/static method call          | `CName.methodName(params)`                 | `CName.methodName(params)` or `instance.methodName(params)` |
| instantiate (create instance)     | `const instance = new CName(args);`        | `instance = CName(args)`                                    |

JavaScript does not support multiple inheritance, but Python does.
In addition to the `@staticmethod` decorator, Python also supports the
`@classmethod` decorator. The difference is that methods defined with
the latter are passed the class as the first argument.

Here is an example of a JavaScript class:

```js
class Statistics {
  constructor(...numbers) {
    this.numbers = numbers;
    this.min = Math.min(...this.numbers);
    this.max = Math.max(...this.numbers);
    this.sum = this.numbers.reduce((acc, n) => acc + n, 0);
  }

  add(number) {
    this.numbers.push(number);
    this.sum += number;
    if (number < this.min) {
      this.min = number;
    } else if (number > this.max) {
      this.max = number;
    }
  }

  mean() {
    return this.sum / this.numbers.length;
  }

  report() {
    console.log('min =', this.min);
    console.log('max =', this.max);
    console.log('mean =', this.mean());
  }
}

const stats = new Statistics(1, 2, 3, 4);
stats.report();
stats.add(5);
stats.report();
```

Here is the same class implemented in Python:

```python
from functools import reduce

class Statistics:
    def __init__(self, *numbers):
        self.numbers = list(numbers)
        self.min = min(*self.numbers)
        self.max = max(*self.numbers)
        self.sum = reduce(lambda acc, n: acc + n, self.numbers, 0)

    def add(self, number):
        self.numbers.append(number)
        self.sum += number
        if number < self.min:
            self.min = number
        elif number > self.max:
            self.max = number

    def mean(self):
        return self.sum / len(self.numbers)

    def report(self):
        print('min =', self.min)
        print('max =', self.max)
        print('mean =', self.mean())

stats = Statistics(1, 2, 3, 4)
stats.report()
stats.add(5)
stats.report()
```

Note how in Python the first parameter in all instance methods must be `self`.

## Asynchronous Functions

In Python 3.4+, asynchronous functions are supported by the asyncio library.

| Topic                    | JavaScript                                 | Python                      |
| ------------------------ | ------------------------------------------ | --------------------------- |
| async named function     | `async function fnName(params) { ... }`    | `async def fnName(params):` |
| async anonymous function | `const fnName = async (params) => { ... }` | not supported               |
| async call with await    | `const result = await name(args);`         | `result = await name(args)` |
| async call with then     | `name(args).then(result => { ... });`      | n/a                         |

In JavaScript, async functions return a Promise.
Here is an example of running tasks that
take a simulated amount of time to complete.
The first takes 3 seconds, the second takes 2, and the third takes 1.
Each tasks outputs its "starting" message immediately.
The "ending" messages appear in reverse order
due to their differing sleep durations.

```js
const sleep = async ms => new Promise(resolve => setTimeout(resolve, ms));

async function doIt(name, sleepMs) {
  console.log('starting', name);
  await sleep(sleepMs);
  console.log('ending', name);
}

async function main() {
  const task1 = doIt('alpha', 3000);
  const task2 = doIt('beta', 2000);
  const task3 = doIt('gamma', 1000);
  await Promise.all([task1, task2, task3]);
  console.log('finished');
}

main();
```

The output is:

```text
starting alpha
starting beta
starting gamma
ending gamma
ending beta
ending alpha
finished
```

In Python 3.4, the `asyncio` library was added.
It can be used to create coroutines which are similar to JavaScript Promises.
See {% aTargetBlank "https://docs.python.org/3.8/library/asyncio.html", "asyncio docs" %}
Python doesn't seem to have to equivalent of
the JavaScript Promise methods `then` and `catch`.

Here is an implementation of the previous JavaScript example in Python.
It produces the same output.

```python
import asyncio

async def doIt(name, sleepMs):
    print('starting', name)
    await asyncio.sleep(sleepMs / 1000)
    print('ending', name)

async def main():
    task1 = asyncio.create_task(doIt('alpha', 3000))
    task2 = asyncio.create_task(doIt('beta', 2000))
    task3 = asyncio.create_task(doIt('gamma', 1000))
    await asyncio.gather(task1, task2, task2)
    print('finished')

asyncio.run(main())
```

## Modules

| Topic          | JavaScript                                 | Python                               |
| -------------- | ------------------------------------------ | ------------------------------------ |
| defining       | content of file                            | content of file                      |
| export         | `export name = value;`                     | everything is automatically exported |
| default export | `export default name = value;`             | not supported                        |
| import default | `import name from 'path';`                 | not supported                        |
| import named   | `import {name1, name2} from 'path';`       | from moduleName import name1, name2  |
| import both    | `import name, {name1, name2} from 'path';` | n/a                                  |
| where to find  | npm                                        | pip                                  |

## Boolean Operations

| Operation   | JavaScript   | Python      |
| ----------- | ------------ | ----------- |
| and         | `b1 && b2`   | `b1 and b2` |
| or          | `b1 \|\| b2` | `b1 or b2`  |
| not         | `!b`         | `not b`     |
| bitwise and | `b1 & b2`    | same        |
| bitwise or  | `b1 \| b2`   | same        |
| bitwise not | `~b`         | same        |
| bitwise xor | `b1 ^ b2`    | `b1 & b2`   |

## Numeric Operations

| Operation                                     | JavaScript                         | Python               |
| --------------------------------------------- | ---------------------------------- | -------------------- |
| basic                                         | `+`, `-`, `\*`, `/`                | same                 |
| exponentiation                                | `*\*`                              | same                 |
| increment                                     | `++n1` (pre) or `n1++` (post)      | `v += 1`             |
| decrement                                     | `--n1` (pre) or `n1--` (post)      | `v -= 1`             |
| mod (remainder)                               | `%`                                | same                 |
| convert to string                             | `n.toString()`                     | `str(n)`             |
| convert to string with fixed decimals (ex. 2) | `n.toFixed(2)`                     | `"{:.2f}".format(n)` |
| convert to hex                                | `n.toString(16)`                   | `hex(n)`             |
| convert from hex                              | `parseInt(hexString, 16)`          | `int(hexString, 16)` |
| constants                                     | see Math and Number global objects | see math module      |
| functions                                     | see Math and Number global objects | see math module      |

## String Operations

| Operation           | JavaScript                                      | Python                                      |
| ------------------- | ----------------------------------------------- | ------------------------------------------- |
| literal single line | `'text'` or `"text"`                            | same                                        |
| literal multi-line  | `` `text` ``                                    | `"""text"""` or `'''text'''`                |
| length              | `s.length`                                      | `len(s)`                                    |
| concatenate         | `s1 + n1`                                       | `s1 + str(n1)` or `s1 str(n1)`              |
| lowercase           | `s.toLowerCase()`                               | `s.lower()`                                 |
| uppercase           | `s.toUpperCase()`                               | `s.upper()`                                 |
| substring           | `s1.substring(start[, end])`                    | `s[start:end]` or `s[start:]` or `s[:end]`  |
| slice               | like `substring`, but supports negative indexes | same as above                               |
| split               | `s.split(delimiter)` returns array              | `s.split(delimiter)` returns list           |
| starts with         | `s.startsWith(sub)` returns boolean             | `s.startswith(sub)` returns boolean         |
| ends with           | `s.endsWith(sub)` returns boolean               | `s.endswith(sub)` returns boolean           |
| contains            | `s.includes(sub)` returns boolean               | `sub in s` returns boolean                  |
| index of            | `s.indexOf(sub)` returns number                 | `s.index(sub[, start[, end]])` returns int  |
| last index of       | `s.lastIndexOf(sub)` returns number             | `s.rindex(sub[, start[, end]])` returns int |
| compare             | `s.localeCompare(sub)` returns -1, 0, or 1      | not supported                               |
| replace first       | `s.replace(oldSub, newSub)`                     | `s.replace(old, new, 1)`                    |
| replace all         | `s.replaceAll(oldSub, newSub)`                  | `s.replace(old, new)`                       |
| trim start          | `s.trimStart()`                                 | `s.lstrip()`                                |
| trim end            | `s.trimEnd()`                                   | `s.rstrip()`                                |
| trim both           | `s.trim()`                                      | `s.strip()`                                 |
| repeat n times      | `s.repeat(n)`                                   | `s * n` or `n * s`                          |

## Sequences

JavaScript stores sequences of values in arrays.

Python has three sequence types which are list, tuple, and range.
Lists are mutable and are typically homogeneous (elements have the same type).
Tuples are immutable and are typically heterogeneous
(elements can have different types).
Ranges are immutable sequences of numbers and are often used in `for` loops.

To create a JavaScript array:

```js
const arr = [element1, element2, ...];
```

To create a Python list, tuple, and range:

```python
myList = [element1, element2, ...]

# Parentheses around a tuple are optional.
myTuple = (element1, element2, ...)

myRange = range(start, end, step)
```

| Operation         | JavaScript                                                                            | Python                                                                                    |
| ----------------- | ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| is array/sequence | `Array.isArray(expression)`                                                           | `hasattr(type(obj), '\_\_iter\_\_')`                                                      |
| append            | `arr.push(v1, v2, ...)`                                                               | `seq.append(v)` and<br>`seq.extend(iterable)` to add more than one element                |
| length            | `arr.length`                                                                          | `len(seq)`                                                                                |
| lookup            | `const value = arr[index];`                                                           | `value = seq[index]`                                                                      |
| subset            | `const newArr = arr.slice(startIndex[, endIndex]);`                                   | `newSeq = seq[startIndex:endIndex]`                                                       |
| concatenate       | `const newArr = arr1.concat(arr2, arr3, ...);`                                        | `newSeq = seq1 + seq2`                                                                    |
| find              | `const value = arr.find(predicate);`                                                  | `next(filter(predicate, iterable))`                                                       |
| find index        | `const index = arr.findIndex(predicate);`                                             | see note below this table                                                                 |
| for each          | `arr.forEach(value => { ... });`                                                      | `for item in seq:`                                                                        |
| includes          | `arr.includes(value)` returns boolean                                                 | `value in seq`                                                                            |
| not includes      | `!arr.includes(value)` returns boolean                                                | `value not in seq`                                                                        |
| index of          | `const index = arr.indexOf(value[, fromIndex])`                                       | `seq.index(value[, start[, end]])`                                                        |
| last index of     | `const index = arr.lastIndexOf(value[, fromIndex])`                                   | not builtin; have to reverse list                                                         |
| join              | `arr.join(delimiter)` returns string                                                  | `delimiter.join(iterable)`                                                                |
| map               | `const newArr = arr.map(value => newValue);`                                          | `iterator = map(function, iterable)`                                                      |
| filter            | `const newArr = arr.filter(predicate);`                                               | `iterator = filter(predicate, iterable)`                                                  |
| reduce            | `const value = arr.reduce((acc, value) => { ... });`                                  | `from functools import reduce`<br>`value = reduce(lambda acc, item: ..., seq, initial)`   |
| any/some          | `arr.some(predicate)` returns boolean                                                 | `any(map(predicate, iterable))`                                                           |
| all/every         | `arr.every(predicate)` returns boolean                                                | `all(map(predicate, iterable))`                                                           |
| add to end        | `arr.push(value);`                                                                    | `seq.append(value)`                                                                       |
| remove from end   | `const value = arr.pop();`                                                            | `seq.pop()`                                                                               |
| add to start      | `arr.unshift(value);`                                                                 | `seq.insert(0, item)`                                                                     |
| remove from start | `const value = arr.shift();`                                                          | `del seq[0]`                                                                              |
| remove all        | `arr = [];`                                                                           | `seq.clear()`                                                                             |
| sort              | `arr.sort(comparator);`                                                               | `list.sort(key=fn)` where `fn` returns a value for the key                                |
| change            | `arr.splice(start, delCount, v1, v2, ...);`                                           | combine `del` and `insert` above                                                          |
| slice             | `arr.slice(start, end)`<br>can omit end<br>can use negative indexes to count from end | `seq[start:end]`<br>can omit start and/or end; can use negative indexes to count from end |

JavaScript generators can be used to implement lazy evaluations
where code is not executed until results are needed.
See examples in the "List Comprehensions" section.

Python also supports generator functions and the `yield` keyword.
The Python `filter` and `map` functions are lazy.
To get values from them, pass the result to a function like `list` or `set`.
For example:

```python
numbers = [1, 2, 3]
doubled = list(map(lambda n: n * 2, numbers))
```

The string `join` method takes an iterable over strings.
To join non-string values, use `map`. For example:

```python
'-'.join(map(str, numberList))
```

Python doesn't have a simple, builtin way to find the first item in a list
that matches some criteria. This naive approach is probably the most efficient.

```python
def index(aList, predicate):
  for index in range(0, len(aList) - 1):
      if predicate(aList[index]):
          return index
  return None
```

## Sorting

Suppose we have a sequence of object that represent people and we wish to
sort the sequence on their last name following by their first name.

Here is how this can be done in JavaScript:

```js
const people = [
  {firstName: 'Tami', lastName: 'Volkmann'},
  {firstName: 'Mark', lastName: 'Volkmann'},
  {firstName: 'Brendan', lastName: 'Eich'},
  {firstName: 'Guido', lastName: 'van Rossum'}
];
people.sort((p1, p2) => {
  const compare = p1.lastName.localeCompare(p2.lastName);
  return compare ? compare : p1.firstName.localeCompare(p2.lastName);
});
console.log(people);
```

Here is how this can be done in Python:

```python
people = [
  {'firstName': 'Tami', 'lastName': 'Volkmann'},
  {'firstName': 'Mark', 'lastName': 'Volkmann'},
  {'firstName': 'Brendan', 'lastName': 'Eich'},
  {'firstName': 'Guido', 'lastName': 'van Rossum'}
]

def personKey(person):
  return person.get('lastName').lower() + person.get('firstName').lower()

people.sort(key=personKey)
print(people)
```

## List Comprehensions

Python supports list comprehensions, but JavaScript does not.
Here are some examples.

```py
squares = [n**2 for n in range(5)]
print(squares) # [0, 1, 4, 9, 16]

multipleOf3 = [n for n in range(10) if n % 3 == 0]
print(multipleOf3) # [0, 3, 6, 9]
```

JavaScript generator functions can be used to do the same thing,
but some utility generator functions must be written.

```js
function* range(n) {
  for (i = 0; i < n; i++) yield i;
}

function* map(fn, iter) {
  for (const element of iter) yield fn(element);
}

const squared = map(n => n ** 2, range(5));
console.log([...squared]); // [0, 1, 4, 9, 16 ]

function* filter(predicate, obj) {
  for (const element of obj) {
    if (predicate(element)) yield element;
  }
}

const multipleOf3 = filter(n => n % 3 === 0, range(10));
console.log([...multipleOf3]); // [ 0, 3, 6, 9 ]
```

## Key/Value Collections

To store associations between keys and values, Python uses "dictionaries".

| Operation               | Python                         |
| ----------------------- | ------------------------------ |
| create                  | `dict = {}`                    |
| get length              | `len(dict)`                    |
| set value of key        | `dict[key] = value`            |
| get value of key        | `dict[key]` or `dict.get(key)` |
| get all keys            | `dict.keys()` or `list(dict)`  |
| get all values          | `dict.values()`                |
| get all keys and values | `dict.items()`                 |
| test if key present     | `key in dict`                  |
| delete key              | `del dict[key]`                |
| delete all keys         | `dict.clear()`                 |
| iterate over            | `for item in dict.items():`    |

JavaScript uses plain objects or instances of the `Map` class
to store associations between keys and values.
The keys in JavaScript objects must be must be strings, integers, or symbols,
but keys in `Map` instances can be any type.

| Operation               | JavaScript Object                                        | JavaScript Map                                                     |
| ----------------------- | -------------------------------------------------------- | ------------------------------------------------------------------ |
| create                  | `const obj = {};`<br>can include initial key/value pairs | `const map = new Map();`<br>cannot specify initial key/value pairs |
| get length              | `Object.keys(obj).length`                                | `map.size`                                                         |
| set value of key        | `obj.key = value` or `obj[key] = value`                  | `map.set(key, value)`                                              |
| get value of key        | `obj.key` or `obj[key]`                                  | `map.get(key)`                                                     |
| get all keys            | `Object.keys(obj)`                                       | `map.keys()`                                                       |
| get all values          | `Object.values(obj)`                                     | `map.values()`                                                     |
| get all keys and values | `Object.entries(obj)`                                    | `map.entries()`                                                    |
| test if key present     | `key in obj` or `obj.hasOwnProperty(key)`                | `map.has(key)`                                                     |
| delete key              | `delete obj.key` or `delete obj[key]`                    | `map.delete(key)`                                                  |
| delete all keys         | `obj = {}`                                               | `map.clear()`                                                      |
| iterate over            | `for (const prop in obj)`                                | `map.forEach((value, key) => { ... });`                            |

## Sets

Sets are unordered collections with no duplicate values.

| Operation             | JavaScript                                       | Python                                  |
| --------------------- | ------------------------------------------------ | --------------------------------------- |
| create                | `const s = new Set();` - cannot specify elements | `s = {elements}` or `s = set(elements)` |
| length                | `s.size`                                         | `len(s)`                                |
| includes              | `s.has(value)`                                   | `value in s`                            |
| add                   | `s.add(value)`                                   | same                                    |
| remove                | `s.delete(value);`                               | `s.remove(value)`                       |
| remove all            | `s.clear()`                                      | same                                    |
| iterate over          | `s.forEach(value => { ... });`                   | `for value in set:`                     |
| convert to list/array | `a = s.values();`                                | `l = list(s)`                           |

## Regular Expressions

In Python, import the `re` library. It supports the following methods:

- split: Split a string by the occurrences of a pattern.

| Operation                | JavaScript                                                                | Python                                       |
| ------------------------ | ------------------------------------------------------------------------- | -------------------------------------------- |
| create                   | `const re = /pattern/flags` or<br>`const re = new RegExp(pattern, flags)` | `import re`<br>`regex = re.compile(pattern)` |
| test if a string matches | `if (re.test(str))`                                                       | `if regex.search(str):`                      |
| get first match          | `str.match(re)`                                                           | `regex.search(str)`                          |
| get all matches          | `str.matchAll(re)` or `re.exec(str)`                                      | `regex.finditer(str)`                        |
| split string on re       | `str.split(re)`                                                           | `regex.split(str)`                           |

## Error Handling

Python refers to errors as exceptions.

| Operation   | JavaScript                                      | Python                         |
| ----------- | ----------------------------------------------- | ------------------------------ |
| throw error | `throw new Error(message);`                     | `raise ExClass(args)`          |
| catch error | `try { ... } catch (e) { ... } finally { ... }` | `try: ... except ExClass: ...` |

## JSON

| Operation | JavaScript                                 | Python                           |
| --------- | ------------------------------------------ | -------------------------------- |
| create    | `const jsonString = JSON.stringify(expr);` | `jsonString = json.dumps(expr)`  |
| parse     | `const value = JSON.parse(jsonString);`    | `value = json.loads(jsonString)` |

In Python, you must `import json`.
There are many builtin Python exception classes.
The base class of all of them is Error.

## Check for running as main

In Python, use `if __name__ == '__main__':`.
In Node.js, use `if (require.main === module) {`.

## Popular Tools/Libraries/Frameworks

| Topic            | JavaScript                          | Python                                        |
| ---------------- | ----------------------------------- | --------------------------------------------- |
| command-line     | Node.js                             | `python` interpreter                          |
| utilities        | Lodash, Ramda                       | pydash                                        |
| web server       | Express                             | Flask                                         |
| web framework    | React, Vue, Svelte                  | Flask                                         |
| dates and times  | date.fns, Moment.js, Temporal       | datetime (in standard library)                |
| unit tests       | Jest, Mocha, Chai, @testing-library | unittest (in standard library), nose2, pytest |
| end-to-end tests | Cypress                             |                                               |
| math             | mathjs                              | math (in standard library)                    |

## Python Magic Methods

Python magic methods support operator overloading for custom classes.
This is a partial list of the magic methods that a Python class can be implement.

| Method                              | Parameters       | Purpose                                               |
| ----------------------------------- | ---------------- | ----------------------------------------------------- |
| object lifecycle                    |                  |                                                       |
| `__new__`                           | cls, ...         | creates a new object                                  |
| `__init__`                          | self, ...        | initializes a new object                              |
| `__del__`                           | self             | destroys an object                                    |
| string representation               |                  |                                                       |
| `__repr__`                          | self             | returns a string representations useful to developers |
| `__str__`                           | self             | returns a string representation useful to users       |
| comparisons                         |                  |                                                       |
| `__cmp__`                           | self, other      | removed in Python 3                                   |
| `__ne__`                            | self, other      | determines if this object is not equal to another     |
| `__eq__`                            | self, other      | determines if this object is equal to another         |
| `__lt__`                            | self, other      | determines if this object is < another                |
| `__le__`                            | self, other      | determines if this object is <= to another            |
| `__gt__`                            | self, other      | determines if this object is > another                |
| `__ge__`                            | self, other      | determines if this object is >= to another            |
| also see functools.total_ordering() |                  |                                                       |
| list-like operations                |                  |                                                       |
| `__getitem__`                       | self, key        | gets an item from a list by index                     |
| `__setitem__`                       | self, key, value | sets an item in a list by index                       |
| `__delitem__`                       | self, key        | deletes an item from a list by index                  |
| `__iter__`                          | self             | returns an iterator                                   |
| `__contains__`                      | self, item       | determines if a given item is contained               |
| dict operations                     |                  |                                                       |
| `__missing__`                       | self, key        | returns value to use when key is not present          |
| math operations                     |                  |                                                       |
| `__add__`                           | self, other      | adds an object to another                             |
| `__sub__`                           | self, other      | subtracts an object from another                      |
| `__mul__`                           | self, other      | multiplies an object by another                       |
| `__div__`                           | self, other      | divides an object by another                          |
| `__mod__`                           | self, other      | mods an object by another                             |
| pickling (serialization)            |                  |                                                       |
| `__getstate__`                      | self             | pickles an object                                     |
| `__setstate__`                      | self             | unpickles an object                                   |
| other                               |                  |                                                       |
| `__call__`                          | self, ...        | treats an object as a function; can change state      |

## Types

For JavaScript, use the TypeScript compiler.

For Python, use the mypy tool which
performs type checking on Python source files.

Primitive types supported by mypy are:

| Type Name | Meaning                                              |
| --------- | ---------------------------------------------------- |
| `bool`    | Boolean                                              |
| `bytes`   | array of bytes                                       |
| `complex` | complex number with `float` real and imaginary parts |
| `float`   | double precision floating point number               |
| `int`     | unlimited precision integer                          |
| `str`     | string                                               |

Collection types supported by mypy are:

| Type Name            | Meaning                                               |
| -------------------- | ----------------------------------------------------- |
| `Dict[KT, VT]`       | dict with keys of type KT and values of type VT       |
| `List[T]`            | list with elements of type T                          |
| `Sequence[T]`        | any kind of sequence whose elements are all of type T |
| `Set[T]`             | set with elements of type T                           |
| `Tuple[T1, T2, ...]` | tuple whose elements have specified types             |

Other types supported by mypy are:

| Type Name                                           | Meaning                                                                 |
| --------------------------------------------------- | ----------------------------------------------------------------------- |
| `Any`                                               | any value                                                               |
| any class name                                      | instance of the class or subclass                                       |
| `Callable[[P1, P2, ...], RT]`                       | function that takes parameters of types P1, P2, ... and returns type RT |
| `Callable[...], RT]`                                | function that takes any parameters and returns type RT                  |
| `Generator[YieldType, SendType, ReturnType]`        | generator function;<br>`SendType` and `ReturnType` can be `None`        |
| `NamedType('Name', [('name1', T1), ('name2', T2)])` | named tuple                                                             |
| `Optional[T]`                                       | matches `None` or the type T<br> same as `Union[None, T]`               |
| `Type[C]`                                           | matches a class object for class C or a subclass                        |
| `Union[T1, T2, ...]`                                | matches any of the specified types                                      |

Aliases can be defined for long type descriptions.
This is useful when the same type description is used in many places.
For example, `IntToStringMap = Dict[int, str]`.

To add a type hint to a variable or function parameter,
follow its name with a colon, a space, and the type.

To add a return type hint to a function,
follow the argument list right parenthesis with `->` and the type.

For example:

```python
def orderIceCream(flavor: str, scoops: int, add_sprinkles: bool) -> IceCream:
```

mypy cannot perform type checking on function arguments that correspond to
parameters with default values or
parameters that collect variadic arguments in a tuple or dict.

The `python` interpreter ignores type hints,
but they make startup time take slightly longer.
They are useful as documentation even without using mypy.
IDEs can use them to flag type issues.

To install mypy, enter `pip install mypy`.
On a Mac, add the following directory to the `PATH` environment variable:
`/Library/Frameworks/Python.framework/Versions/3.8/bin`.

To run mypy on a source file and all the files it imports,
enter `mypy {filename}.py`.

## VS Code

The VS Code extension "Python" from Microsoft adds
"IntelliSense, linting, debugging, code navigation, code formatting,
Jupyter notebook support, refactoring, variable explorer, test explorer,
snippets, and more".

Other useful VS Code extensions for Python code include
autopep8 and pylint.