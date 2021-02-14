# [Refactoring from good to great](https://www.youtube.com/watch?v=L1G--mPscQM)

1) Temporal variables to private methods
  * Reduces the number of methods
  * We can reuse them
  * Easier to read
  * Hides implementation details
2) Feature envy (a class inspects other classes). Tell don't ask
  * Move logic to the object
  * Behaviour closer to the data
3) Data clump (passing a lot of parameters)
  * Better to pass a minimum number parameters as possible
4) Invert control. Instead of passing params we pass the data clump
  * Reduces coupling
  * Easiert to change
5) Parameter coupling. Passing and inspecting objects in methods increases coupling, less parameters is better.
6) Behaviour magnet. Now that we have the appropriate classes, we have a place to put behaviour.
7) Refactor and improve performance of the classes we have probably with native behaviour
8) Extract behavior into private methods
9) Collection as first class citisens so we have a place to put collection behaviour
10) We do not have all data in objects (null data). Pej: a Job may not have a contact name. We have to check it all over the place. NullContact (Null-Object pattern). NullContact (name and phone). No need for conditions or obfuscation.
11) Adapter pattern. A user managing payments (Depending on Braintree). Depend upon abstractions. If I want to change the payment provider I have to change a lot of places. Extract it to a PaymentGateway and make the user depend on that abstraction. Easy to mock and test.

When to refactor:
- All the time. Refactor on green. On code review
- God objects (like user, the main class of the business journey)
- High churn files, a file that changes all the time. Do not waste a lot of effort on files that don't change often
- Bug

Check out for number of lines, there are better ways of measuring complexity

References:
- [Clean Code](https://www.goodreads.com/book/show/3735293-clean-code)
- [GOOS](https://www.goodreads.com/book/show/4268826-growing-object-oriented-software-guided-by-tests)