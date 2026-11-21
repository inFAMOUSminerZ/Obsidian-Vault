## Title page
- Assignment: 3: Test-Driven Development
- Name: Brandon McAuley
- Student ID: 26457288
- Module: CS4004 Software Testing & Inspection
---
## 1. Introduction
### 1.1 Purpose of the report
The purpose of this report is to demonstrate my Test-Driven Development (TDD) in action. Using the TDD method to develop a banking system and testing as you go, demonstrating that testing for failure, editing the code until it passes. 

I am going to try and avoid editing the code to do more than just pass our previous failure. Though editing is acceptable if it is strictly structural and adds no functionality.
### 1.2 Tools and Environment
- **Java version**: Java 25
- **JUnit version**: JUnit Jupiter 5.14.0
- **IDE**: IntelliJ IDEA
### 1.3 Legend
- 🟥: Test designed to pass once the missing feature exists. The test is expected to fail.
- 🟩: Edit made to only pass the fail-case.
- 🟨: Edit made to improve structure, not add functionality.

### 1.4 Cycles
#### 🟥 Test #1 Failure
The first thing I wanted to do is create a bank account system with the 2 Java files outlined in the assignment brief. First what I did was write my first fail-case which creates a `BankAccountManagementSystem_26457288` object called "Bank".

```java
public class TDD_26457288{
    @Test
    public void accountTest(){
        BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();
        Bank.createAccount(67);
    }
}
```

![[Project 3 _Test-Driven_Development_Error1.png|612]]

	It tries to access the `createAccount` method, however this does not exist yet so it fails with the above error. I chose this test case first because this is where any account will be created. It is the first part of the code that is run when we account for things in the future such as balance, withdrawal, etc... Without an account, these things should not be possible.
#### 🟩 Test #1 Success
Next I want to edit the code so that it passes this initial test. To do this all we need to do is create the method it was looking for. Right now the `BankAccountManagementSystem_26457288.java` file is blank, here is what I added to pass the test: 

```java
public class BankAccountManagementSystem_26457288{

    public void createAccount(int Id){

    }
}
```

![[Project_3_Test-Driven_Development_Pass1.png]]

Here I just put some arbitrary int called Id in the parameters so that I could pass through 67 (also arbitrary for now) since this was the least I needed to do to pass the test. 
#### 🟨 Test #1 Refactoring
There are some non-functional edits I wish to make here however, such as the naming for the test method being somewhat vague and and the parameter being Id instead of id: 

```java
public class BankAccountManagementSystem_26457288{

    public void createAccount(int id){

    }
}
```

```java
public class TDD_26457288{
    @Test
    public void methodTest(){
        BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();
        Bank.createAccount(67);
    }
}
```
#### 🟥 Test #2 Failure
Now I have to test for the initial balance on the account. I do not have such a thing so the failing point is a little obvious, I duplicated the previous test and added a double to the create account function, this is how I did it:

```java
@Test
    public void accountTest(){
        BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();
        Bank.createAccount(67, 10.00);
        assertEquals(10.00, Bank.initBalance);
    }
```

![[Project_3_Test-Driven_Development_Error2-1.png]]

You can also see that I expect to get 10.00 from `initBalance` which is our assertion. This comes back as a compile error for two separate reasons. 
1. There is no place for the double to go in `creatAccount`.
2. Once it compiles, the test still fails because the parameters aren't stored, so `initBalance` is `0.0` instead of `10.0`.
#### 🟩 Test #2 Success
To fix these issues I just need to add the following `initBalance` double, however you may see another smart solution. I needed to make sure that the previous test passed for TDD principals to apply, so I overloaded the method `createAccount` so that I can keep my previous solution and create a new one for our current test.

Then I equated the parameters in `createAccount` (`id` and `initBalance`) with the global variables `id` and `initBalance`.

```java
public class BankAccountManagementSystem_26457288{

    int id;
    double initBalance;

    public void createAccount(int id){

    }

    public void  createAccount(int id, double initBalance){
        this.id = id;
        this.initBalance = initBalance;
    }
}
```

![[Project_3_Test-Driven_Development_Success2.png]]
#### 🟥 Test #3 
**Requirement 1.2: the initial balance must be a positive value**
Now I want to set up a test for detecting a negative number is not stored. I set up an `assertThrows` methods which is like saying

```java
@Test
    public void negativeTest(){
        BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();
        assertThrows(IllegalArgumentException.class, () -> Bank.createAccount(67, -100.0));
    }
```

![[Project_3_Test-Driven_Development_Error3.png]]



