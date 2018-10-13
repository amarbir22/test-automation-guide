# Test Automation Practice Guide
Welcome, all test evangelists!! In the word of constantly evolving test practices and tools, we hope this document acts as a fundamental guide, which helps you write some awesome :sparkling_heart: tests; which are beautiful, yet effective and hopefully easier to maintain by the next Joe :neckbeard:, who comes across your tests.

This guide is __NOT__ intended as set of rules you need to follow. But, a roadmap towards writing better tests for your team that suits you needs. 

_To contribute to this document, please create a PR and explain why the change is required._

## Planning
Planning is the most crucial part when starting a new project. There is nothing such as 'too much planning'. It is imperative that you spend time selecting the right tools, design patter and test framework.

### Selecting the right tools
One of the most critical aspects of starting a new project is to pick the right tools for the job. In terms of test automation, one should align their tools with the development team. Here are some of the key points to keep in mind:

* __Try to stay in same technology stack__ as the application. If the application is a front-end UI NodeJS App, it's favorable to select a NodeJS based test framework such as Protractor, WebDriverIO etc. This helps development team colaborate and help test team.
* __Favor a more popular and engaging tool__. Community driven tools usually have enough documentation to help you with your configuration problems and special use cases. You can gauge a tool's engagement by checking the tool GitHub page for stars, last commit date, releases etc. Also, its noteworthy to check the open-issues and PRs on GitHub.

### POCs
After selecting the right tool that suit your needs you can go ahead and create your own or find existing boilerplates, examples etc. on GitHub. Here are some steps you can follow:

1.	__Search on GitHub for existing implementations__. It is good idea to fork and evaluate it. Contact the owner if required for more help. 
2.	__Create your abstraction layer around the tool that try to solve your special use cases__. Follow the recommendation and best practices of the tool, which usually can be found on their website/GitHub page under "Developer's Guide" or "API reference"
3.	__Clone existing boilerplates and examples from GitHub__ and use them to evaluate and utilize as your own custom implementation of the tool. If you plan to use someone's boilerplate as is or in part, then __don’t forget to credit them in your readme file__.

## Architecture
After, completing an exhaustive selection and evaluation of the tool or test framework we can start forming the tool according to our need and use cases.

Remember, that automation tests are not just only for you. But, the next Joe who comes along to perform the regression.

### Design Pattern
Now, you are ready to start developing your framework around the tool (or an existing framework). For a UI test automation framework, one of the most used and loved design pattern is Page Object Model which provides a level of granularity to your tests. 

Page Object Model provides an abstraction layer based on the pages of your UI application. Simply put, each page would have its model. The model maybe be represented by a class (if you have chosen a Java or Typescript based framework). Or it might be a Javascript file (for NodeJS based frameworks).

* A model representing your UI application page usually contains UI elements (__selectors -CSS please :pray:__!  [Learn More]() and functions for business logic. That’s it!! It's a simple design pattern, try not to over engineer it. Refer to Gifting as an example.
* Apply SOLID principles if possible. Create a basePage to represent lower level common elements and functions. For an example refer to ProtractorModel Link for Typescript/Java.

### Test Organization
Test organization help write readable and maintainable tests. Poorly written tests not only are unreliably for positively finding defects. But, they add overhead on test teams to constantly fix the tests. Constant maintenance of these poor tests can drag down a test team, which may ultimately ignore/comment-out these tests. This negatively affects the test bottom line of finding defects.  

Here are some absolute key points:
*	__Test must be independent__. It must NOT depend on other tests to set the application state or pre-reqs. [Learn More](http://essentials.xebia.com/independent-tests/)
*	__Test should encapsulate high level business functionally__ such as form fillings etc. in an Abstraction layer such as a Page Model or common functions. [Learn More]()
*	__Test must not interfere with other test cases__. For example, if there is a test 'X' which creates a "User Joe", then under no circumstances you should have test Y should refer to the "User Joe". Doing so creates __high coupling -which is BAD__.
* __Test should create and delete its own data__. It by be performed by triggering a Hook such as before Test and after Test etc. If you cannot delete data, you must tag this data with prefix such as MY_APP_AUTO_GEN_FNAME_joe etc. so it would be easier to perform housekeeping by the Database team in future. Provide the prefix information in your readme file.
*	__Test must be focus on a specific goal__, functionality and acceptance criteria. __A test should not be longer than 60 lines__, if it is then you need to rethink about your test objective. You must break it down! Longer tests are harder it is to read them. But, also it is __very hard to maintain__ them by the next Joe. Refer to Gifting for a good example.
*	Create helper functions that may be imported in your test case to solve special use cases or for setting application state. It is important to name them appropriately. __Naming a function "reusableTestFunction" is NOT helping anyone__ understand or fixing your tests! On other hand, ``` fillUserPersonalInformation({"firstname": "joe", "lastname": "jones"})``` is a good method name. It shows the reader its purpose, and handles data elegantly. In Javascript, its a good idea to pass objects rather than hard arguments; as you can add more arguments anytime, without any breaking changes upstream or to the function calls.
*	__Favor quality over quantity__. Don’t test same thing in 10 different tests. For example, if you have asserted against a `<h1>` tag text on a page in a test, you don’t need to test the same `<h1>` tag in a different test.
*	__Avoid Unnecessary field validation and assertions__. It may look tempting to assert against a text inside a `<p>` tag. But, doing so not __only makes user test more prone to failure on dynamic content changes__ but also it provides very little functional test value. Ideally you should just check for text being not empty. But, it is O.K sometimes to test `<h>` tags for content, but there is a line that you need to draw in terms of content validation. If it is absolutely critical to test bunch of texts, __you may add these expected texts in a file (or a page models)__ or somewhere from where it can be easily managed and changed, if tests fails on an indented content change.

#### Selectors
In the current UI scene, __CSS selector is the recommended__ way to go. Not only CSS selectors are much more readable then xpath, they are also more resilient on different browsers. Most modern Javascript based UI test automation framework such as Protractor, NightwatchJS, WebDriverIO have css as default selector strategy. [Learn More](https://www.w3schools.com/cssref/css_selectors.asp)

Here are some key points to remember:
*	Shorter is better
*	A Dynamic Selector is better then many selectors

#### Load Page Strategy
A load page strategy is one of the most import aspect for a UI test framework. A good load page strategy will save you from a lot of synchronization issues that you may encounter later in your tests. [Learn More]()

Here are some key points you need to keep in mind:
1.	Load Page method should receive a partial path for the page and not the whole url. This helps you decouple your tests from a hardcoded environment. The base url should be stored somewhere global where it can be set from an environment variable.
2.	Load Page method can have a second argument for an element that will be present on the page after loading. Load Page must for this element to be visible before returning. This help solves synchronization issues when next command is called before the page has completely loaded.
3.	For making a resilient load page method, you can add smart retry mechanism and add waits for ajax and Javascript to finish executing.

## Continious Integeration
Place Holder [Learn More]()

### Code Pipeline
Place Holder [Learn More]()
### Containerization
Place Holder [Learn More]()


## Must read whitepapers
1.	[How to create killer automated functional tests - by Nikolay Advolodkin](https://techbeacon.com/how-create-killer-automated-functional-tests)
2.	[How to create an effective test automation strategy - by Albert Starreveld](https://medium.com/@abstarreveld/considerations-for-an-effective-test-automation-strategy-a5bd027b3fa3)
