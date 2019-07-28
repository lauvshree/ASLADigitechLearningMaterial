### Testing:

Testing is an important and integral part of any software development project. Testing ensures that the sofware works in a manner it is intended to work. Testing also help avoid bugs in the code. It tests for issues in the code and facilitates fixing then and there before the completed code is deployed in production. 

<img src="testing_flowchart.png"/>

The objective of using Testing tools is to automate the tests instead of doing them manually or in addition to manual testing, thereby saving a lot of time doing redundant tasks. These testing tools are nothing but code that tests code. 

#### Why is testing important?
1. Get an error if you break the code
2. Save time
3. Think about possible bugs and issues
4. Integrate into build workflow so that most issues are dealt with before the code is deployed.
5. Breakup complex dependencies into smaller testable units of code which will help in isolating the issues. 
6. Improve the code to cover all the corner cases and handle all the exceptions.

#### Different kind of tests
1. Unit tests which tests an isolated unit of the code.
2. Integration test which tests code which interdependent.
3. E2E (End to End test) which tests the full flow of the software being developed.

#### Jest
To run tests we need test runners, assertion libraries and browser simulators.
Jest is a library which offers all in one package along with puppeteer and has been recetly updated and is robust. It is a very popular tool and is used extensively in Java script testing.


1. To test your project with jest, `npm install --save-dev jest` in your project root folder.

2. Also for browser test `npm install --save-dev puppeteer`.

3. In `package.json`, under scripts make `test` point to `jest`. 

4. Run `npm test` from the project root folder now and it should look for all test files and run them. But we don't have any test files yet. All js files whose names end with `test.js` or `spec.js`  will be picked up by jest for testing. Let's start creating our first test file.

#### Sample unit test
We first require the module or js file we want to test into a constant using object destructuring. 
While including test cases, 
1. Create test cases for valid arguments (Preferably more than one)
2. Create test cases for invalid arguments
3. 
In `package.json` adding `--watch` option to jest will make the test run automatically when there is a code change.
To test the interaction that actually happens through the browser, we also need a browser simulator. 


