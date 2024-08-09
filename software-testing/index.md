# Software Testing

## Behavior Driven Testing

* BDD is a mindset, philosophy on how to better explain do TDD.
* TDD can go wrong by focusing on coverage and tests that are hard to read.
* BDD gives an extra layer that takes the angle of the end user, not you, the creator, and explains on the high level how a feature or scenario should go.
    * **BDD is the layer or "What to test (a flow/feature/scenario)"**
    * Underneath there is the code on "how to test" this flow/feature/scenario, this is an implementation detail that can change over time.
    * **Any good test should rather say what it tests, than how, just like when writing code**.
* A good TDD approach would actually look like BDD, tools like gherkin and SpecFlow are not a must, you can technically write just clearer tests that follow this philosophy.
* Remember, BDD was to help avoid misunderstandings about TDD. So they are not mutually exclusive and rather complementary.
* Tests that are about "how to test" you are structured are easier to maintain, if the implementation changed of the design, the test still indicates what it intends to test.
* BDD is a flavour to TDD one could argue.

## Resources

* [Guide to BDD](https://youtu.be/gXh0iUt4TXA?si=RBTym3p1--dGUG6i)
* [TDD vs BDD](https://youtu.be/Bq_oz7nCNUA?si=IKeSQgOEhMQXGJT8)