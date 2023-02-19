[//]: # TODO Add the correct images to the post

# Adding Test to your project

#webdev #beginners #tutorial #testing

## Why test

Making tests ensures that your application works as expected, lets you prove that it does what is supposed to do. For this there are several kind of test we can use:

**_Manual Testing_**: In this kind of tests we use the application as the end user will and see what happens when we do certain things.

- _Advantages_

  - Lets you follow the flow a normal user will use
  - Don't have to write more code for your application

- _Disadvantages_
  - They take long time to run
  - Can "forget" to run some tests
  - May not be checking for edge cases

**_Automated Tests_**: In this kind of tests we write some code that will ensure that our application does what is expected.

- _Advantages_

  - Runs fast
  - You can not "forget" to run some test
  - You define all of the edge cases

- _Disadvantages_
  - You need to write more code in your application
  - A bad designed test will not ensure your code quality

## Kinds of test

Now that we've seen how we can test (either manually or automated), let's see what are the most common types of tests we will encounter

- Functionality tests: With this kind of tests we ensure that the business logic of each of our components work properly.

- Integration tests: With this kind of tests we ensure that the different components of our application works together properly.

- End to end tests: With this kind of tests we go through the process of what a user will do when using the application

As more things go in place the longer the test takes to run, and the more things that it have to check.

## Creating the tests

For our example, since we are using TypeScript in the project we created in the last post, we are going to be using a tool that is called [JEST](<(https://jestjs.io/)>)

### Installing JEST

To install JEST you need to type on the console

```cmd
$ npm install -D jest ts-jest @types/jest @jest/globals
$ npx ts-jest config:init
```
This will add all of the required libraries for jest to work and will create the jest configuration file that wil look something like

```javascript
/** @type {import('ts-jest).JestConfigWithTsJest}  */
module.exports = {
	preset: 'ts-jest',
	testEnvironment: 'node',
};
```

Finally we need to add the test script to our *package.json* file

```json
{
    ...
    "scripts": {
        ...
        "test": "jest"
        ...
    }
    ...
}
```

Now we are ready to start making our test, for that we will create a new file called ```sum.test.ts``` inside this file we will make a test that will check that a sum function works properly

Inside the file we will write the following:

```typescript
import { describe, it, expect } from "@jest/globals"
function sumNumbers(num1: number, num2: number): number {
	return num1 + num2
}

describe("Testing that we can add two numbers", () => {
	it("Should return the sum of the two numbers",() =>{
		const total = sumNumbers(1, 1)
		expect(total).toBe(2)
 	})
})
```

For us to be able to run the test we just need to run the following command on our terminal

```cmd
$ npm run test
```

Now lest run a failing test to see how it looks

```typescript
import { describe, it, expect } from "@jest/globals"
function sumNumbers( num1: number, num2: number): number {
    return num1 + num2
}

describe("Testing that we can add two numbers", () => {
    it("Should return the sum of the two numbers", () => {
        const total = sumNumbers(1, 1)
        expect(total).toBe(2)
    })

    it("Should send error when not the correct sum", () => {
        const total = sumNumbers(1, 1)
        expect(total).toBe(3)
    })
})
```

Again, run the test and we will see an error.
Now that we know that our tests are working propperly, lets refactor.
First lest create a directory inside our *src* folder called *helpers* and inside lets create a file called *sumNumbers.ts* and that file should have the following contents:

```typescript
function sumNumbers(num1: number, num2: number): number {
    return num1 + num2
}
```

Finally in our *sum.test.ts" file we need to delete the function and import it from the new file we have just created

```typescript
import { describe, it, expect } from "@jest/globals"
import sumNumbers from "../src/helpers/sumNumbers"

describe("Testing that we can add two numbers", () => {
    it("Shoud return the sum of the two numbers", () => {
        const total = sumNumbers(1, 1)
        expect(total).toBe(2)
    })

    it("Should send error when not the correct sum", () => {
        const total = sumNumbers(1, 1)
        expect(total).toBe(3)
    })
})
```

If we have done everything right, we should see that the first test should be successfull and that the second test should show us the same error as before.
Finally lets remove the failing test and  we are done.

## Conclusions

In today's post we were learned about testing and begin to write functionality tests using a library called **JEST**

## Next steps

Excelent, we have just enabled a testing library in our project.

After this we will need to:

- Add eslint and prettier
- Add the routes to work the logic of our application

All of these topics I will cover them in future posts































