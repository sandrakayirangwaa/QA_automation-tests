Part A: Test Structure
describe() 
Purpose: describe() is used to group related test cases together. It helps organize tests into logical sections, making them easier to read and maintain.
Syntax: describe(‘Test case name’ () => { });
Example: describe(‘Login tests’, () => { 
it(‘should log in successfully’, () =>{
cy.visit(‘https://example.com/login’);
}); 
});
Real-world use case: in an e-commerce website, you can use describe() to group all cart tests together, such as adding products, removing products and updating quantities.

it()
Purpose: it() defines a single test case. 
Syntax: it(‘should perform a specific action’, () => { });
Example: it(‘should display the homepage’, () =>{
cy.visit(‘https://example.com’);
cy.title().should(‘contain’, ‘Example’); 
});
Real-world use case: Testing whether a user can successfully log in with valid credentials.

before()
Purpose: before() is used for setup tasks that only need to happen one time.
Syntax: before(() => { });
Example: describe(‘user tests’, () => { 
before(() => {
cy.visit(‘https://example.com/login’);
});
it(‘should load the login page’, () => {
cy.contains(‘Login’);
});
});
Real-world use case: Logging into an application once before running several tests that require an authenticated user.

beforeEach()
Purpose: beforeEach() runs before every test case inside a describe() block. It ensures each test starts with the same setup. 
Syntax: beforeEach(() => { });
Example: describe(‘Dashboard tests’, () => {
beforeEach(() => {
cy.visit(‘https://example.com/dashboard’);
});
it(‘should display the dashboard’, () => {
cy.contains(‘Dashboard’);
it(‘should display the profile menu’, () => {
cy.contains(‘Profile’);
});
});
Real-world use case: opening the application’s homepage before every test starts.

after()
Purpose: after() runs after all tests in a describe() block. It is used for cleanup.
Syntax: after(() => { });
Example: describe(‘Logout Tests’ , () => {
after(() => {
cy.log(‘All tests completed’);
});
it(‘should log out successfully’, () => {
cy.visit(‘https://example.com’);
});
});
Real-world use case: Deleting test data or logging out after all tests have completed.

afterEach()
Purpose: it is used for cleanup after each individual test.
Syntax: afterEach(() => { });
Example: describe(‘Search Tests’, () => {
afterEach(() => {
cy.log(‘Test completed’);
});
it(‘should search for a product’ () => {
cy.visit(‘https://example.com);
cy.get(‘input).type(‘Book’);
});
}):
Real-world use case: resetting an application after each test so that one test does not affect the next.

Part B: Assertions
expect()
It is used to make assertions about JavaScript values such as variables, arrays, objects or strings.

When to use it
 Testing JavaScript variables
 Comparing values
 Checking objects or arrays

Examples
 Comparison of numbers
 Checking a string
 Checking an array

should()
This is a cypress assertion that automatically retries until the expected condition is met or the timeout expires.

When to use it
 Verifying page URLs
 Validating element visibility
 Confirming text is displayed.

Examples
 Check element visibility
 Verify input value
 Verify URL


Part C: Basic Cypress Commands
 
Action
Command
Example 
Visit a page
cy.visit()
cy.visit(‘https://example.cypress.io’)

Type into a textbox
cy.type()
cy.get(‘#name’).type(‘John Doe’)

Click a button
cy.click()
cy.get(‘#submit’).click()

Clear a field
cy.clear()
cy.get(‘#password’).click()

Check a checkbox
cy.check()
cy.get(‘#agree’).click()

Uncheck a checkbox
cy.uncheck()
cy.get(‘#agree’).click()

Select from a dropdown
cy.select()
cy.get(‘#country’).click()

Scroll to an element
cy.scrollIntoView()
cy.get(‘#footer’).click()

Upload a file
cy.selectFile()
cy.get(‘input[type=file]’).selectFile(‘cypress/fixtures/sample.pdf’)

Hover over an element
cy.trigger(‘mouseover’)
cy.get(‘.menu’).trigger(‘mouseover’)

Right click
cy.rightclick()
cy.get(‘.box’).rightclick()

Double click
cy.dbclick()
cy.get(‘.button’).dbclick()

Press keyboard keys
cy.type()
cy.get(‘#search’’).type(‘{delete})


Part D: Locators
cy.get()
Finds elements using a CSS selector.

Example: cy.get(‘username’).type(‘John’);

cy.contains()
Finds an element containing a specific text.

Example: cy.contains(‘Login’).click();

.find()
Finds child elements within another element.

Example: cy.get(‘.menu’).find(‘li’);

.children()
Gets only the direct children of an element.

Example: cy.get(‘#list’).children();

.parent()
Gets the immediate parent element.

Example: cy.get(‘.item’).parent();

.closest()
Gets the nearest ancestor matching a selector.

Example: cy.get(‘.price’).closest(‘.product’);

.eq()
Selects an element by index.

Example: cy.get(‘tr’).eq(2);

.first()
Get the first element.

Example: cy.get(‘li’).first();
.last()
Get the last element.

Example: cy.get(‘li’).last();

.within()
Limits commands to a specific section.

Example: cy.get(‘form’).within(() => {
cy.get(‘#email’).type(‘john@example.com);
});

Why are IDs preferred?
IDs are unique on a webpage, making testing faster and more reliable. 
What are CSS selectors?
CSS selectors identify HTML elements using tags, IDs, classes or attributes.
What are data attributes (data-cy, data-testid)?
These are custom HTML attributes created specifically for testing.
Why are long CSS selectors discouraged?
Because they can easily break when the UI changes and are difficult to read.

PART E: Assertions Practice
Be.visible
cy.get(‘#login’).should(‘be.visible’);
Exist
cy.get(‘#username’).should(‘exist’);
Contain
cy.get(‘h1’).should(‘contain’,’Welcome’);
Have.text
cy.get(‘#message’).should(‘have.text’.’Success’);

Have.value
cy.get(‘#email’)
.type(‘sandra@gmail.com’)
.should(‘have.value’, ‘sandra@gmail.com’);

Have.length
cy.get(‘li).should(‘have.length’,5);

Be.enabled
cy.get(‘#submit’).should(‘be.enabled’);

Be.disabled
cy.get(‘#submit’).should(‘be.disabled’);

Be.checked
cy.get(‘#agree).check().should(‘be.checked’);

Have.attr
cy.get(‘img’).should(‘have.attr’, ‘src’);


PART F: Working with elements
Buttons
cy.get(‘#submit’).click();

Text fields
cy.get(‘#name’).type(‘sandra’);

Password fields
cy.get(‘#password’).type(‘sandra123’);

Checkboxes
cy.get(‘#agree’).check();
cy.get(‘#agree’).uncheck();

Radio buttons
cy.get(‘#male’).check();

Dropdowns
cy.get(‘#country’).select(‘Kenya’);

Text areas
cy.get(‘#comments’).type(‘this is my comment’);

Links
cy.contains(‘ABout’).click();

Images
cy.get(‘img’).should(‘be.visible’).and(‘have.attr’, ‘src’);


PART G: Waiting
Automatic waiting
Cypress automatically waits for elements to appear before interacting with them.

Retry-ability 
If an assertion fails, Cypress automatically retries until it passes or the timeout is reached.

cy.wait()
Pauses test execution for a specified time or waits for an API request
Waiting for API request
Example:
cy.intercept(‘GET’ ‘/users’).as(‘getUsers’);
cy.visit(‘/users’);
cy.wait(‘@getUsers’);
Waiting for page loading
Example:
cy.visist(‘https://example.cypress.io’);
cy.get(‘h1’),should(‘be.visible’);


Why is cy.wait(5000) considered bad practice?
This is because it makes tests slower and may fail if the page loads slower.
A better alternative is to wait for an element or API request.

PART H: FORMS
describe('Form Test', () => {
beforeEach(() => {
cy.visit('https://demoqa.com/automation-practice-form');
});
it('fills the form', () => {
cy.get('#firstName').type('Sandra');
cy.get('#lastName').type('Keza');
cy.get('#userEmail').type('sandrakeza@gmail.com');
cy.get('input[type="radio"]').first().check({force:true});
cy.get('#dateOfBirthInput').click();
cy.get('.react-datepicker__day--015').click();
cy.get('#hobbies-checkbox-1').check({force:true});
cy.get('#submit').click({force:true});
cy.contains('Thanks for submitting the form').should('be.visible');
});
});

PART I: TABLES
Count rows
cy.get('table tbody tr').type('have.length', 5);
Count columns
cy.get('table thead th').type('have.length', 3);
Read data from a row
cy.get('table tbody tr').eq(1).should(‘contain’, ‘sandra’);
Click a button inside a row
cy.get('table tbody tr').eq(2).find(‘contain’).click();
Verify table contents
cy.get('table').should(‘contain’, ‘book’);

PART J: BROWSER INTERACTIONS
Browser Back
cy.go(‘Back’);

Browser Forward
cy.go(‘forward’);

Reload
cy.reload()

Open a new tab (how Cypress handles this)
Cypress does not support multiple browser tabs. Instead remove the target attribute.
cy.get('a').invoke(‘removeAttr’, ‘target’).click();

Browser alerts
cy.on('window:alert’, (text) => {
expect(text).to.equal(‘Success’);
}); 

Confirmation dialogs
cy.on('window:confirm’, () => true);

Prompt dialogs
Cypress cannot directly automate browser prompts
Window.prompt is often used

PART K: KEYBOARD ACTIONS
Enter
cy.get(‘#search’).type(‘Laptop{enter}’);

Tab
cy.get(‘#firstName’).type(‘Sandra’);

Escape
cy.get(‘body’).type(‘{esc}’);

Arrow Up
cy.get(‘input’).type(‘{uparrow}’);

Arrow Down
cy.get(‘input’).type(‘{downarrow}’);

Arrow Left
cy.get(‘input’).type(‘{leftarrow}’);

Arrow Right
cy.get(‘input’).type(‘{rightarrow}’);

Delete
cy.get(‘#name’).type(‘{del}’);

Backspace
cy.get(‘#name’).type(‘{backspace}’);


PART L: SCROLLING
Scroll to the bottom of a page
cy.scrollTo(‘bottom’);

Scroll to the top
cy.scrollTo(‘top’);

Scroll to a specific element
cy.get(‘#footer’).scrollIntoView();

Verify the element becomes visible
cy.get(‘#footer’).scrollIntoView().should(‘be.visible’);


PART M: FILE UPLOAD
Why Cypress cannot upload files by default
Earlier versions of CYpress did not include built-in file upload support, so users relied on plugins such as cypress-file-upload. Recent versions now include the built-in selectFile() command.

The plugin or built-in approach commonly used
Built-in Method
cy.get(‘input[type=file]’).selectFile(‘cypress/fixtures/sample.pdf’);

Upload a sample image or PDF
cy.get(‘input[type=file]’).selectFile(‘cypress/fixtures/photo.jpg’);


REFLECTION
During this assignment, I learned the basic concepts of Cypress and how it is used for automated web testing. The easiest concept for me to understand was using cy.visit() because it simply opens a webpage before running the rest of the test. I also found cy.get() straightforward since it allows me to locate elements using CSS selectors.
The most challenging part was understanding how Cypress waits for elements automatically and learning how to select the correct element when multiple similar elements exist on a page. I had to practice using selectors and assertions to make my tests more reliable.
I also learned that Cypress executes commands asynchronously, which is different from regular JavaScript. This required some adjustment in the way I wrote my tests. Running the tests in the Cypress Test Runner and seeing each step execute helped me understand how Cypress works.
In the future, I would like to learn more about creating reusable custom commands, handling API testing with Cypress, and integrating Cypress into CI/CD pipelines using GitHub Actions. I am also interested in learning how to organize larger test suites using the Page Object Model and how to generate detailed test reports for automation projects. Overall, this assignment gave me a strong foundation in Cypress automation testing and increased my confidence in writing simple automated tests.
