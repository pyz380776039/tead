# Tead - Lighting the way to simpler testing

[![Travis Build Status](https://travis-ci.org/okwolf/tead.svg?branch=master)](https://travis-ci.org/okwolf/tead) [![Windows Build Status](https://ci.appveyor.com/api/projects/status/github/okwolf/tead?svg=true)](https://ci.appveyor.com/project/okwolf/tead/branch/master) [![Coverage Status](https://coveralls.io/repos/github/okwolf/tead/badge.svg?branch=master)](https://coveralls.io/github/okwolf/tead?branch=master) [![npm version](https://img.shields.io/npm/v/tead.svg?style=flat)](https://www.npmjs.com/package/tead)

In a world full of complex test-runners, Tead dares to keep it simple. Tests are defined as plain JavaScript objects. The only test assertion supported is a basic form of deep equals. Mocks/fakes/spies will never be provided. Asynchronous tests are not possible. These are all very intentional key features.

The boilerplate and global nastiness of functions such as `describe/beforeEach/beforeAll/afterEach/afterAll/test/it/assert/expect/...` are gone. Your linter is so happy, it no longer cares whether you use semicolons or not. Callback functions with `done` arguments that you're responsible for calling - history. Once you learn the simple convention for test values, you will notice they are all signal and no noise. Standard-issue watch mode is built-in. Support for your ES6 modules comes attached to its frontal lobe.

Tead is compatible with `Node.js >=6`.

If you are interested in using a functional style of building applications from pure functions free of side effects, Tead will aid you in your noble quest. There is only one possible kind of function that can be written in this utopian world, and but a single way to test it. Each test merely calls one of these pure functions with an input value and compares the actual result with the expected output for equality. Writing tests changes from being a chore to a joy, and suddenly tests are written first instead of as an afterthought. Such coverage. So much rejoicing.

The name is from an obscure word for torch.

## Getting Started

Let's get started by writing a test for a hypothetical function that adds two numbers. First create a `sum.js` file:

```js
export default (a, b) => a + b;
```

Then create a file named `sum.test.js` and add some tests:

```js
import sum from "./sum";

export default {
  "sum can add": {
    zeros: [sum(0, 0), 0],
    "positive numbers": [sum(1, 2), 3],
    "negative numbers": [sum(-1, -2), -3],
    "mixed sign numbers": [sum(1, -2), -1]
  }
};
```

Object keys are used to group and describe tests. Array values represent test expectations. The order of the elements in the expectation is `[actual, expected]` and differences will be reported as test failures.

Finally, run `npx tead` and Tead will print this message:

```console
$ npx tead
 PASS  sum.test.js
  sum can add
    ✓ zeros
    ✓ positive numbers
    ✓ negative numbers
    ✓ mixed sign numbers

4 passing
```

**You have successfully written your first test using Tead!**

I believed in you all along ✋

## Installation Options

### Global

```console
npm i -g tead
```

Then you may run tests in any project folder with:

```console
tead
```

### NPX

No install required, just run from any project folder:

```console
npx tead
```

### Local

Install with npm / Yarn:

```console
npm i -D tead
```

Then add tead as the test script in your `package.json`:

```json
"scripts": {
  "test": "tead"
}
```

Now you may run with:

```console
npm test
```

## Usage

### Command Line

Here are the available command line arguments:

| Argument     | Usage                                                                                                                                                      | Default                                                 |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| testPattern  | The regex pattern Tead uses to detect test files. Defaults to files ending with `test.js` or `spec.js` not in `node_modules`.                              | <code>^((?!node_modules).)*(test&#124;spec)\.js$</code> |
| watch        | Watch files for changes and rerun tests. Output is limited to only failing tests and overall passing/failing counts.                                       |                                                         |
| watchPattern | The regex pattern Tead uses when in watch mode to match which file changes should rereun tests. Defaults to files ending with `.js` not in `node_modules`. | <code>^((?!node_modules).)*\.js$</code>                 |

Each argument is passed in the form `--argument=value`. Here is an example using all available arguments:

```console
npx tead --testPattern=folder.*\.test\.js --watch --watchPattern=folder.*\.test\.js
```

### API

Tead offers a programmatic way to integrate running with existing JavaScript code.

You may bring in the `tead` API function using `import` if you have support for ES6 syntax:

```js
import tead from "tead";

tead(options);
```

Or using `require`:

```js
const tead = require("tead");

tead(options);
```

The `options` object has the same properties and values as the arguments supported by the command line version.

## License

Tead is MIT licensed. See [LICENSE](LICENSE.md).
