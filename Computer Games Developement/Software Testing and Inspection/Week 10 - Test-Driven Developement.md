## Final Assignment
**Deadline**: Sunday Week 12 (29/11/26, 11:59)
**Worth**: 50%
**Assignment**: TDD + Data Flow Testing
**Submission**: Report + Two Java Files

**Data Flow Testing**
DFT is a type of structural testing focused on selecting test paths through program a program based on definition and use of variables.

Definition clear paths: 

## Principles
You should always write tests before you write code. Then you write code to pass this test and you continue to do this until the code achieves expectations and passes all your test cases. It should be a failing test where you do the following: 

**`Write test -> Test fails -> Edit Code to Pass the Test`**

A useful quote from Kent Beck is "Even if I do not know how to code I should know how to test for what I expect".

![[Week_10_Test_Driven_Developement_ Cycle_2.png|wrap-left|506]]
## The TDD Cycle
1. Write/Rewrite test.
2. Test fails.
3. Write enough code to pass the tests.
4. Some tests fail.
5. Write enough code to pass the tests.
6. Refactor/Clean code.

## Continuous Integration
- Continuous Integration (CI) is the merging of all developers code shared on mainline several times per day.
- Continuous Regression Testing is when you test immediately after approach
- Perform some level of statistic analysis
Often CI goes alongside Continuous Deployment (CD) which is automated deployment of the working build

**Seamless Pipeline**
TDD, CI and CD allow you to create a pipeline that is maximally bullet proof and secures the product that is at the end of development.

## TDD 
**PROS**
- Promotes thinking before implementation instead of instinctive or impulsive coding.
- Allows to concentrate on small chunks of code, less need for huge scope comprehension.
- Testing AND refactoring are at the core of this method and aid in software quality and stability.
- Developers take testing seriously and cannot forget to do so. It is a part of the pipeline.
**CONS**
- Some people do not care for testing, they care about output. Outcomes. Patches can be made.
- Everyone needs to be on board. A lack of cohesion leads to a total loss of cohesion.
- It is not sufficient as the only testing of the system. It can lead to a false sense of confidence.
- Becomes very complicated especially if the systems include external dependencies such as databases.

# Code Kata
A kata is an exercise in karate where one repeats a sequence of movements many times, making improvements each time. We can apply this to our code. One place you can do this is [**Cyber Dojo**](https://cyber-dojo.org/creator/home)

**Refactoring**
A nice practice, however for the final assignment it will probably not be necessary.

