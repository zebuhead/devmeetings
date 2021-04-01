# Unit Testing
Unit testing is a way of testing code. A "unit" is the smallest piece of code
that can be isolated - in javascript and php this is a function or 
method. 

Unit testing is used in test driven development, as part of the QA process, or during code refactoring.

Unit Test Examples
---
Javascript using Jest 
```javascript
test('two plus two is four', () => {
  expect(2 + 2).toBe(4);
});
```
PHP using PHPUnit:
```php
final class EmptyTest extends TestCase
{
    public function testTwoPlusTwoIsFour(): void
    {
        $this->assertEquals(4, 2+2);
    }
}
```


Test Driven Development
----------------
In test driven development, unit tests are written before any other code is written.
Test are usually written by the developer that writes the code. The idea is that the 
programmer can keep tweaking or refactoring the code, but still know that it functions correctly.

QA Process
---
Tests can written during the QA process to verify that the code functions as intended.
The tests can also be used as a way to provide documentation by describing what the code should
be doing.

Jest
===
Jest is a javascript testing framework. It's one of the most popular testing frameworks for javascript.

Installing Jest
---
Jest can be installed using npm. 
Start by setting up a new npm project. Create a new directory. Use the terminal to 
to navigate to the directory. In the terminal type
```shell
npm init
```

This should ask you a series of questions about your project. 
You can press enter on `project name`, `version`, `description`, and `entry point` questions 
to use the default values (or you can change them if you want). On the `test command` question type `jest`
```shell
test command: jest
``` 
Any remaining questions can also be skipped.

Once the project is created run 
```shell
npm install --save-dev jest
```

Your directory should now contain a `node_modules` directory, a `package.json` file, and a `package-lock.json` file

Creating Your First Test
---
In Jest, a single test is a call to the `test()` function. The `test()` function takes 2 parameters - the test description as a string and a callback function. 
(The documentation uses "arrow" functions for the callback) 

The conditions that are being tested are in the callback. The callback in it's simplest form contains `expect(x).toBe(value)`. 

In your project directory create a new file with the name `main.test.js`. (This file name is arbitrary and could be anything)

For the first test add the following to `main.test.js`. 
```javascript
test('two plus two is four', () => {
  expect(2 + 2).toBe(4);
});
```

Save the file and run the command
```shell
npm run test
```


After a few seconds you should see something like:

```shell
 PASS  ./main.test.js
  ✓ two plus two is four (2 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.962 s, estimated 1 s
Ran all test suites.
```

If you are using VS Code, instead of using the terminal, you may be able to open the `package.json` file and click `Debug` right above

```json
  "scripts": {
    "test": "jest"
  },
```

Writing more realistic tests
---
In the project directory create a new file named `main.js` (Like the `main.test.js` file, this name is arbitrary).
Create a function in the new file. 
```javascript
function toCelsius(fahrenheit) {
  return (5/9) * (fahrenheit-32);
}
```
The function will need to be exported using `module.export` so that the test file has access to the function. 
In `main.js` add the line `module.exports = {toCelsius}` at the bottom. The file should now contain:
```javascript
function toCelsius(fahrenheit) {
  return (5/9) * (fahrenheit-32);
}
 
module.exports = {toCelsius};
```

The function will need to be imported into `main.test.js`. Add `const mod = require('./main');` to the top of the file.
An object was exported in `main.js`. That means that the function will need to be accessed through the object (we named it `mod` when we imported it). 


Now create a test to verify that 32F is equal to 0C in `main.test.js`.
```javascript
test("32 F is 0 C", () => {
    expect(mod.toCelsius(32)).toBe(0);
});   
```
Run the test now to verify that everything is working correctly. 

**Create another test to verify that 212F is equal to 100C.**

Another Example
---

Create a new function in main.js
```javascript
function getUrlParameter(name, location) {
    name = name.replace(/[\[]/, '\\[').replace(/[\]]/, '\\]');
    var regex = new RegExp('[\\?&]' + name + '=([^&#]*)');
    var results = regex.exec(location);
    return results === null ? '' : results[1].replace(/\+/g, ' ');
};
```
Make sure to add the function to the exported module. 
```javascript
module.exports = {toCelsius, getUrlParameter};
```

Add 2 more tests to `main.test.js`
```javascript
test("can get name from url", () => {
    expect(mod.getUrlParameter("name", "example.com?name=John&email=john%40example.com")).toBe("John");
});

test("can get email from url", () => {
    expect(mod.getUrlParameter("email", "example.com?name=John&email=john%40example.com")).toBe("john@example.com");
});
```










 
 





  
