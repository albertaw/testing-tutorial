Unit testing with Mocha
===============================

Install mocha globally 

```bash
npm install --global mocha
```

Install locally

```bash
npm install --save-dev mocha
```

Create a folder named test to hold your test files.

Install Chai to use their expect assertions
npm install chai --save-dev

Example use:
expect(actual_value).matcher(expected_value)

```js
//book.test.js
const expect = require('chai').expect;

describe('Book', function() {
	it('get book properties', function() {
		const book = {
			isbn: '1234',
			title: 'Oliver Twist',
			author: 'Charles Dickens'
		};

		expect(book.isbn).to.equal('1234');
		expect(book).to.have.deep.property('title');
	});
});
```

To run tests:

```bash
Mocha
```



Testing an API with Axios
===============================

Install chai, axios and mocha

```javascript
const axios = require('axios');
const expect = require('chai').expect;

describe('Books', function() {
	it('GET books', async function() {
		let response;
	    try {
	      response = await axios.get('http://localhost:3000/api/books');
	    } catch (error) {
	      console.log(error);
	    } finally {
	      const count = response.data.length;

	      expect(count).to.equal(2);
	    }
	});
});
```


Acceptance testing with Cypress
===============================

Install cypress

```bash
npm install cypress --save-dev
```

Open cypress

```bash
npx cypress open
```

Add tests to `cypress/integration` folder. Uses Mocha and Chai.

Example test:

```javascript
describe('Creating a post', function() {

	it('creates a post successfully', function() {
		cy.server();
		cy.route('POST', '/api/posts').as('createPost');
		//go to the web page
		cy.visit('http://localhost:3000/');
		//click the new post button
		cy.contains('New Post').click();
		//enter a username and text
		cy.get('input[name=author]').type('Author');
		cy.get('textarea').type('test post');
		//click submit
		cy.contains('submit').click();
		cy.wait('@createPost', {timeout: 10000});
		//should see the post on the page
		cy.get('.card-text').first().should('have.text', 'test post');
	});
});
```

Testing Android apps with Espresso
=====================================

Add the following to dependencies inside app `build.gradle` file:

```
androidTestImplementation 'androidx.test.espresso:espresso-core:3.1.0'
androidTestImplementation 'androidx.test:runner:1.1.0'
androidTestImplementation 'androidx.test:rules:1.1.0'
```

Add the following to the default config inside the `build.gradle` file:

```
testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
```

Add test to androidTest directory.

API:

```java
onView(ViewMatcher).perform(ViewAction).check(ViewAssertion);
```

Example test:

```java

@LargeTest
public class HelloWorldEspressoTest {

    @Rule
    public ActivityTestRule<MainActivity> activityRule =
            new ActivityTestRule<>(MainActivity.class);

    @Test
    public void listGoesOverTheFold() {
        onView(withText("Hello world!")).check(matches(isDisplayed()));
    }
}
```

Resources
===============================

- [Mocha test framework](https://mochajs.org/)
- [Chai assertion library](https://www.chaijs.com/)
- [Axios - promise based HTTP client](https://github.com/axios/axios)
- [Cypress end-to-end testing framework](https://www.cypress.io/)
- [Espresso Android UI testing framework](https://developer.android.com/training/testing/espresso)

