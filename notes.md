Intro
-----

I'll start by introducing the categories of testing commonly used in web dev
This chart is how I think about testing code: there's a continuum of low level to high level tests.

Low level tests tend to be very fast, simple and decoupled. The benefit of this is that you can thoroughly check specific behaviour. They can also help with debugging, maintenance and refactoring.

High level tests tend to be very similar to production system, more integrated with other services and closer to real user interactions. The benefit of these is they can provide a lot of confidence that your system works correctly.

Unit
----

Unit tests are the lowest level in this scale. They normally make use of mocks and stubs to isolate code from other systems and services. This is fairly easy with platforms that use depedency injection, such as Angular, but more tricky in node, because of the way modules are loaded.

Extensive use of mocks and stubs also ties your tests to a particular implementation, which makes refactoring more difficult.

- Gulp
    - Streams
    - Tasks
    - Watching
- Mocha
    - Methods
    - Assertions
    - Only/skip
    - Async stuff
- Client side
    - Karma
    - PhantomJS
- Server side
- Mocking stuff
    - Sinon
    - Nock

Code coverage is a really useful tool, and luckily there's a really awesome Javascript library called Istanbul. Code coverage can give you a good indication of missing areas in your test coverage, and it's really helpful for adding tests to an existing project.

- Code coverage
    - Istanbul


Integration
-----------

Probably the most ill-defined type of tests are integration tests. Integration tests are technically any test which integrates different parts of a system, but the term is often used to mean tests which integrate the whole system. I'm going to use the term to mean tests which test the integration of specific components with the system.

For example we may wish to have tests which run against a real database, i.e. test that data is saved and retrieved from the database correctly. These kind of tests help guard against changes to other services, and check our assumptions of those services.

Another useful integration test is to check routing works correctly, by mocking an express server and checking that URLs map correctly to routes. The real value in this case is to handle regressions which might be caused as new routes are added.

- Routing
    - Supertest
- Database
    - SQLLite
    - Test dependencies
    - Fixtures

System / Acceptance
-------------------

As I mentioned before, integration tests are often used as tests of the whole system, these are sometimes known as system tests. We may wish to test HTTP requests and responses on a real server, or even test client side behaviour on a real browser.

Another variety here is acceptance testing (or user acceptance testing also known as behavioural testing), where tests are written to follow user journeys through a site. This is typically run on a real server and a real browser (via Selenium). These tests work really well with agile, allowing you to validate stories as part of your tests. These kind of tests give you a good confidence that key parts of your system do exactly what they should, but they take a long time to write.

- Protractor / Selenium

Smoke
-----

Finally at the very end of the spectrum we have smoke tests, these are typically almost identical to acceptance tests, except they run on a live server. The purpose of these tests is to verify that the server and its services are running correctly, usually after a deploy. There some obvious limitations with these tests, since we don't want to affect any real user data, we either need to revert any changes that are made, or make sure the changes happen in a development only profile. More importantly these tests should be lightweight because the aim is to find problems as fast as possible post-deploy.


Testing strategy
----------------

So how do you choose which tests to write?
You have to choose the right tests for the project. Low level tests make your project more maintainable but they can't insure that the system works all together.
High level tests validate your project against a spec, which is really useful for clients and managers, but they can't test all the details.
