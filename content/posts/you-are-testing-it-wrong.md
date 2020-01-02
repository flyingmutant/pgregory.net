+++
title = "You are testing it wrong"
description = "Preaching of a property-based testing church adept"
date = 2019-07-25T23:35:05+03:00
draft = true
+++

# You are testing it wrong

1. Traditional testing is useless
   - where do we get test cases from?
     - we check ourselves
   - what do we gain after running a test?
     - first time: it does something (appropriate)
     - next time: it still does the same thing (~0 information)
2. QA, quality assurance
   - being assured that the program does what (and how) is expected
   - developer: feelsgoodman
   - company: $$$
3. Ways to achieve quality assurance
   - strong static typing
   - code review
   - continuous integration
   - ...
   - testing
     - first-hand quality assurance
     - all other ways are secondary
4. Testing
   - modular (e.g. unit-testing)
   - integration
   - regression
   - acceptance
   - ...
   - almost always: example-based testing
     - each test case is an example of the expected behavior
5. Quality assurance with testing
   - want:
     - confidence that the program does what (and how) is expected
       - global property
   - can:
     - check the behavior of the program in a specific case
       - local property
   - result:
     - example-based testing does not give us quality assurance
       - yes, even with 100% test coverage
6. Aside: test coverage
   - useless as a metric
     - does not have any meaningful interpretation
   - useful as an indicator
     - "what is covered by our tests?" -- exact interpretation
7. Quality assurance with testing (pt. 2)
   - want:
     - the height of the part is 1+-0.1mm
   - can:
     - measure the height at the point
   - solution:
     - measure the height at a lot of random points, and extrapolate our confidence
       - it works
8. Property-based testing
   1. State the desired properties
      - the things that the clients of the software expect
      - can be hard!
   2. For each property, Write a test generator which checks it
   3. ...
   4. Profit!
9. Common kinds of properties
   - stateless vs stateful
   - subtypes:
     - simple invariant
       - "sorting sorts"
       - "rebate coupon is not summed with other discounts"
     - relationship
       - encode/decode
       - `+ - * /`
     - conformance to the model
       - database works like `map[string]string`
10. Practice of property-based testing
    - use a good library
      - python: hypothesis
      - go: rapid
    - why?
      - high quality of test case generation
        - intentionally non-uniform distribution
      - automatic minimization of failed test cases
11. Conclusion
    - any tests are better than no tests
    - integration tests are better than unit-tests
    - there is nothing better than property-based tests
      - it can be hard to come up with good properties
      - but it is fun!
    - for good property-based tests you need good libraries
      - python: hypothesis
      - go: rapid
