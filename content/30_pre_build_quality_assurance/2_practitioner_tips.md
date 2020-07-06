+++
title = "Practitioner Tips"
chapter = false
weight = 2
+++

Not every line of code needs to be unit tested, few things to watch out for while Unit Testing:

- Test the lines of code that involve a business logic and services that are at high risk.
- No need to test poco / pojo / data / modal classes.
- Complex multi-threading code can be skipped in unit tests (Cover as part of integration tests)
- No need to test exceptions messages and methods that call other public methods.

