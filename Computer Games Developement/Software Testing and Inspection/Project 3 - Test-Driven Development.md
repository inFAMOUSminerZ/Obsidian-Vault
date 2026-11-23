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
- **NOTE**: Directories in screenshots and code may change due to working on this project on multiple devices.
### 1.3 Legend
- 🟥: Test designed to pass once the missing feature exists. The test is expected to fail.
- 🟩: Edit made to only pass the fail-case.
- 🟨: Edit made to improve structure, not add functionality.

---
## 2. Task 1: TDD Implementation
### 2.1 Requirement 1: Account Creation
#### 2.1.1 Iteration 1 (Test #1)
##### 🟥 Test #1 Failure
**Implement a successful account creation operation.**
The first thing I wanted to do is create a bank account system with the 2 Java files outlined in the assignment brief. First what I did was write my first fail-case which creates a `BankAccountManagementSystem_26457288` object called "Bank".

**Test #1**
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

It tries to access the `createAccount` method, however this does not exist yet so it fails with the above error. I chose this test case first because this is where any account will be created. It is the first part of the code that is run when I account for things in the future such as balance, withdrawal, etc... Without an account, these things should not be possible.
##### 🟩 Test #1 Success
Next I want to edit the code so that it passes this initial test. To do this all I need to do is create the method it was looking for. Right now the `BankAccountManagementSystem_26457288.java` file is blank, here is what I added to pass the test: 

```java
public class BankAccountManagementSystem_26457288{

    public void createAccount(int Id){

    }
}
```
![[Project_3_Test-Driven_Development_Pass1.png]]

Here I just put some arbitrary int called Id in the parameters so that I could pass through 67 (also arbitrary for now) since this was the least I needed to do to pass the test. 
##### 🟨 Test #1 Refactoring
There are some non-functional edits I wish to make here however, such as the naming for the test method being somewhat vague and the parameter being Id instead of id: 

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
#### 2.1.2 Iteration 2 (Test #2)
##### 🟥 Test #2 Failure
Now I have to test for the initial balance on the account. I do not have such a thing so the failing point is a little obvious, I duplicated the previous test and added a double to the create account function, this is how I did it:

**Test #2**
```java
	@Test
    public void accountTest(){
        BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();
        Bank.createAccount(67, 10.00);
        assertEquals(10.00, Bank.initBalance);
    }
```
![[Project_3_Test-Driven_Development_Error2-1.png]]

You can also see that I expect to get 10.00 from `initBalance` which is our assertion. This comes back as a compile error and an assertion error for two separate reasons. 
1. There is no place for the double to go in `creatAccount`.
2. Once it compiles, the test still fails because the parameters aren't stored, so `initBalance` is `0.0` instead of `10.0`.
##### 🟩 Test #2 Success
To fix these issues I just need to add the following `initBalance` double. I needed to make sure that the previous test passed for TDD principles to apply, so I overloaded the method `createAccount` so that I can keep my previous solution and create a new one for our current test.

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
#### 2.1.3 Iteration 3 (Test #3)
##### 🟥 Test #3 Failure
**Requirement 1.2: the initial balance must be a positive value**
Now I want to set up a test for checking that a negative initial balance is rejected. I set up an `assertThrows` method which is like saying "there will be an error with the following code", then I say what kind of error `IllegalArgumentException.class` "It will signal a bad input" and finally I provide the code `() -> Bank.createAccount(67, -100.0)`.

**Test #3**
```java
	@Test
    public void negativeTest(){
        BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();
        assertThrows(IllegalArgumentException.class, () -> Bank.createAccount(67, -100.0));
    }
```
![[Project_3_Test-Driven_Development_Error3.png]]

This was actually a little confusing to learn, but it was very useful going forward so it is worth the explanation
1. JUnit runs `Bank.createAccount(67, -100.0)`.
2. The method accepts the balance. No error.
3. JUnit says: "I expected an `IllegalArgumentException` and got nothing".
4. JUnit produces the above error.

I chose this use case because `-100.0` stands for the whole class of negative balances and an exception over a return value, because it signals failure without changing the method's return type. I tried to change the return type but it was beyond messy and unnecessary once I found this.
##### 🟩 Test #3 Success
To succeed the test case and keep all others going is actually quite simple. Unlike the last one where fixing one test broke the previous these are relatively unrelated. I just need to check if the number inputted is negative and if it is reject it. So I wrote a simple check and rejection:

```java
public void createAccount(int id, double initBalance){  
    this.id = id;  
    this.initBalance = initBalance;  
  
    if (initBalance < 0) {  
        throw new IllegalArgumentException("Initial balance cannot be negative.");  
    }  
}
```
![[Project_3_Test-Driven_Development_Success3.png|442]]

#### 2.1.4 Iteration 4 (Test #4)
##### 🟥 Test #4 Failure
Next we want to pass through another double, but this time have it be of a value of 0.0. As the brief says this needs to be a positive numeric number. Here is the test we run:

```java
@Test  
public void zeroInitialBalanceTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    assertThrows(IllegalArgumentException.class, () -> Bank.createAccount(67, 0.0));  
}
```
![[Project_3_Test-Driven_Development_Error4.png]]

Same as before, we just expect that it should throw an `IllegalArgumentException` error when we give a number, it doesn't and so it says nothing was thrown. To fix this we need to get the error to actually get thrown.
##### 🟩 Test #4 Success
To succeed all we had to do was edit the if statement to be `<=` to instead of `<`. This ensures we do not get a balance with 0 at all and the test passes with an exit code 0.

```java
public void createAccount(int id, double initBalance){  
    this.id = id;  
    this.initBalance = initBalance;  
  
    if (initBalance <= 0) {  
        throw new IllegalArgumentException("Initial balance cannot be negative.");  
    }  
}
```
![[Project_3_Test-Driven_Development.png]]

#### 2.1.5 Iteration 5 (Test #5)
##### 🟥 Test #5 Failure
**Requirement 1.3: no duplicate accounts**
Now I needed to create two accounts with the same ID but different values. This should throw an error as the ID already exists and so I must represent that by writing the following:

```java
@Test  
public void duplicateAccountTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    // creates initial account with initBalance of 10.  
    Bank.createAccount(67, 10.0);  
    // creates another account with the same id and a different initial balance.  
    assertThrows(IllegalArgumentException.class, () -> Bank.createAccount(67, 20.0));  
}
```
![[Project_3_Test-Driven_Development_Error5.png]]

This is where I decided to start adding comments into my code just to help me understand just a little better. We create an account with the ID 67 and a balance of 10.0, then do the same (while expecting an error) for an account with the ID of 67 and a balance of 20.0.
##### 🟩 Test #5 Success
To fix this issue I had to create a new set for my IDs called `accountIds`. `accountIds` now holds whole numbers, never keeps the same number twice, and can quickly tell me whether a number is already in it. Then I have to throw an Illegal Argument Exception when the ID already exists in `accountIds` where we stop the method and an error is raised.

```java
import java.util.HashSet;  
import java.util.Set;  
  
public class BankAccountManagementSystem_26457288{  

    Set<Integer> accountIds = new HashSet<>();  

    int id;  
    double initBalance;  

    public void createAccount(int id){  

    }  

    public void createAccount(int id, double initBalance){  
        if (initBalance <= 0) {  
            throw new IllegalArgumentException("Initial balance cannot be negative.");  
        }  
        if (accountIds.contains(id)) {  
            throw new IllegalArgumentException("Account already exists.");  
        }  
  
        accountIds.add(id);  
          
        this.id = id;  
        this.initBalance = initBalance;  
    }  
}
```
![[Project_3_Test-Driven_Development_Success5.png]]

### 2.2 Requirement 2: Deposit
#### 2.2.1 Iteration 6 (Test #6)
##### 🟥 Test #6 Failure
**Requirement 2.1: Implement a successful deposit operation.**
Moving onto creating a way to deposit funds into an account we want to do something like the following:

```java
@Test
public void depositTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    Bank.deposit(67, 5.0);  
    assertEquals(15.0, Bank.initBalance);
```
![[Project_3_Test-Driven_Development_Error6.png]]

Now obviously this test tries to pass some information into a method that doesn't exist yet so we need to make one that achieves what the brief asks for.

**NOTE**: This is actually the step where I learned that adding a delta field to `assertEquals` is good practice for doubles. I will not include them because they are not necessary, but I did want to note it.
##### 🟩 Test #6 Success
To pass this test all I need is a method that accepts an int called `ID` and a double called `amount` and then adds `amount` to `initBalance`. This also made me question calling it `initBalance` since it is essentially now balance, but I will refactor later.

```java
public void deposit(int id, double amount){  
    this.initBalance = this.initBalance + amount;  
}
```

Here the newest thing is the local variable in the parameters. I take the passed in number and add it to the initial balance. 

![[Project_3_Test-Driven_Development_Success6.png]]

#### 2.2.2 Iteration 7 (Test #7)
##### 🟥 Test #7 Failure
**Requirement 2.2: Validate that deposited amounts are positive numeric values.**
To do this I tested to see if using the deposit method with a negative number would throw an `IllegalArgumentException` but, none was.

```java
@Test  
public void depositNegativeTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    assertThrows(IllegalArgumentException.class, () -> Bank.deposit(67, -5.0));  
}
```
![[Project 3 - Test-Driven Development_Error7.png]]
##### 🟩 Test #7 Success
This step was important, I realised earlier that my initial test (iteration 4), while passing later, did not meet the briefs criteria of only accepting a positive numeric value, that being not negative or 0. Rather than just get rid of negatives like earlier, I achieved what the brief wanted in one fell swoop by adding the following code before adding `amount`.

```java
public void deposit(int id, double amount){  
  
    // here we check if the amount is negative or zero and if it is, throw an error with a message.  
    if (amount <= 0) {  
        throw new IllegalArgumentException("Deposit amount must be positive.");  
    }  
  
    this.initBalance = this.initBalance + amount;  
}
```

As you can see it is very similar to iteration 4, where we use the if statement to ask if the number is non negative. If it is, throw an error.
### 2.3 Requirement 3: Withdrawal
#### 2.3.1 Iteration 8 (Test #8)
##### 🟥 Test #8 Failure
**Requirement 3.1: Implement a successful withdrawal operation.**
This will be quite similar to the deposit method but, in reverse. I set up the test case where we create a bank account and start it with the `id` 67 and the `initBalance` of `10.0`. Then we use the withdrawal method (does not exist yet) and pass through the same id and `5.0`to `initBalance` then we compare our expected number with the actual number and throw an error if it fails. Here is the test case:

```java
@Test  
public void withdrawalTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    Bank.withdrawal(67, 5.0);  
    assertEquals(5.0, Bank.initBalance);  
}
```
![[Project 3 - Test-Driven Development_Error8.png]]

Now this would still fail even if the method was found because it would not do anything and so our `assertEquals` would be incorrect because `Bank.initBalance` would still be 10.0.
##### 🟩 Test #8 Success
Here we just create the method that was missing before and enter the parameters for `id` and `amount`. Then we just take the `initBalance` and take amount away from its total.

```java
public void withdrawal(int id, double amount){  
  
    this.initBalance = this.initBalance - amount;  
}
```

**Test #8 Success**
![[Pasted image 20261122161857.png]]
#### 2.3.2 Iteration 9 (Test #9)
##### 🟥 Test #9 Failure
**Requirement 3.2: Validate that withdrawal amounts are positive numeric values.**
To do this I tested to see if using the withdrawal method with a negative number would throw an `IllegalArgumentException` but, none was.

```java
@Test  
public void withdrawalNegativeTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    assertThrows(IllegalArgumentException.class, () -> Bank.withdrawal(67, -5.0));  
}
```
![[Project 3 - Test-Driven Development_Error8-1.png]]
##### 🟩 Test #9 Success
Now we add an if statement within the `withdrawal` method to make sure it is a positive number. It is the same if statement from iteration #7.

```java
public void withdrawal(int id, double amount){  
  
    // here we check if the amount is negative or zero and if it is, throw an error with a message.  
    if (amount <= 0) {  
        throw new IllegalArgumentException("Withdrawal amount must be positive.");  
    }  
  
    this.initBalance = this.initBalance - amount;  
}
```
![[Pasted image 20261122163544.png]]
##### 🟨 Test #9 Refactoring
The names of the method and testing the method were incorrect. It is `withdraw`, not `withdrawal`.

```java
//TDD_26457288
@Test  
public void withdrawTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    Bank.withdraw(67, 5.0);  
    assertEquals(5.0, Bank.initBalance);  
}  
  
@Test  
public void withdrawNegativeTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    assertThrows(IllegalArgumentException.class, () -> Bank.withdraw(67, -5.0));  
}

// BankAccountManagementSystem_26457288
public void withdraw(int id, double amount){  
  
    // here we check if the amount is negative or zero and if it is, throw an error with a message.  
    if (amount <= 0) {  
        throw new IllegalArgumentException("Withdrawal amount must be positive.");  
    }  
  
    this.initBalance = this.initBalance - amount;  
}
```
### 2.4 Requirement 4: Overdraft Protection
#### 2.4.1 Iteration 10 (Test #10)
##### 🟥 Test #10 Failure
**Requirement 4.1 and 4.2: Implement overdraft prevention to disallow negative balances and Reject withdrawal attempts that exceed the available balance.**
Here I just created a test to use `withdraw` but making the `amount` more than what the accounts `initBalance` is.

```java
@Test  
public void overdraftTest() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    assertThrows(IllegalArgumentException.class, () -> Bank.withdraw(67, 50.0));  
}
```
![[Project 3 - Test-Driven Development-1.png]]
##### 🟩 Test #10 Success
We succeed the test by adding a single if statement AFTER our last one (I don't care if the `amount` > `initBalance` if the amount is not positive) that just checks if the `amount` > `initBalance`. If not we throw an `IllegalArgumentException` and say "Insufficient funds.".

```java
public void withdraw(int id, double amount){  
  
    // here we check if the amount is negative or zero and if it is, throw an error with a message.  
    if (amount <= 0) {  
        throw new IllegalArgumentException("Withdrawal amount must be positive.");  
    }  
    if (amount > initBalance) {  
        throw new IllegalArgumentException("Insufficient funds.");  
    }  
  
    this.initBalance = this.initBalance - amount;  
}
```
![[Project 3 - Test-Driven Development-2.png]]

### 2.5 Requirement 5: Balance Inquiry
#### 2.5.1 Iteration 11 (Test #11)
##### 🟥 Test #11 Failure
**Requirement 5.1: Implement a successful balance inquiry operation.**
Now for this again all we have to do is use an `assertEquals` on a new bank account. We use `Bank.getBalance(67)` to make sure it is the right account and it will not work because that method does not exist.

```java
@Test  
public void getCredit_afterOpen_returnsStartingCredit() {  
    BankAccountManagementSystem_26457288 Bank = new BankAccountManagementSystem_26457288();  
    Bank.createAccount(67, 10.0);  
    assertEquals(10.0, Bank.getBalance(67));  
}
```
![[Pasted image 20261122174938.png]]
##### 🟩 Test #10 Success
To pass this test we add the method, which takes an `id` and then return `initBalance`. When we run the test it passes with exit code 0.

```java
public double getBalance(int id){  
    return initBalance;  
}
```
![[Pasted image 20261122175301.png]]

## 3. Task 2: Data Flow Testing

> **Scope:** I analysed the `deposit` and `withdraw` methods exactly as they stand at the end of Task 1. The system stores a single balance in the class field `initBalance`, so the `id` parameter is never used inside either method. I note this in each section below.

**Terms used**
- **Definition:** a point where a variable is given a value (a parameter on method entry, or an assignment).
- **c-use:** a use in a computation or statement (right-hand side of an assignment).
- **p-use:** a use in a decision (an `if` condition). Each p-use gives two pairs, one for the true outcome and one for the false outcome.
- **DU-pair:** a definition of a variable, together with a use of it that can be reached from that definition along a path where the variable is not redefined (a definition-clear path).
- `initBalance` is a class field, so it gets its value outside the method (in `createAccount` or an earlier deposit or withdrawal). I treat it as defined on entry to the method.

---
## Task 2 - Data Flow Testing
### 3.1 DU-Pair Coverage (deposit method)
#### 3.1.1 The code under test
I numbered the lines on the right and use them as the nodes throughout this section.

```java
public void deposit(int id, double amount){                                // 1
    if (amount <= 0) {                                                     // 2
        throw new IllegalArgumentException("Deposit amount must be positive."); // 3
    }
    this.initBalance = this.initBalance + amount;                          // 4
}
```
#### 3.1.2 Step 1: Relevant data variables

| Variable | Kind | Relevant? | Reason |
|---|---|---|---|
| `id` | parameter | Defined, never used | Appears in the signature but no statement reads it |
| `amount` | parameter | Yes | Validated at node 2 and added to the balance at node 4 |
| `initBalance` | class field | Yes | Read and updated at node 4; holds the account balance |

#### 3.1.3 Step 2: Definitions and uses

| Variable | Definitions | Uses inside the method |
|---|---|---|
| `id` | Node 1 (parameter) | None |
| `amount` | Node 1 (parameter) | Node 2 (p-use), Node 4 (c-use) |
| `initBalance` | Node 1 (value on entry), Node 4 (new value assigned) | Node 4 (c-use of the entry value) |

The new value of `initBalance` assigned at node 4 is never used again inside the method. It is only read by other methods (`getBalance`, `withdraw`), so it creates no DU-pair within `deposit`.

**What I noticed:** `id` is given a value on entry but never used. It produces no DU-pairs, and it means every deposit goes to the single shared balance whatever ID is passed.

#### 3.1.4 DU-pairs ("All DU-pairs" criterion)

| Pair | Variable | Definition node | Use node | Meaning |
|---|---|---|---|---|
| P1 | `amount` | 1 | 2 (true) | `amount <= 0`, exception thrown |
| P2 | `amount` | 1 | 2 (false) | `amount > 0`, execution continues |
| P3 | `amount` | 1 | 4 | `amount` added to the balance |
| P4 | `initBalance` | 1 (entry) | 4 | Existing balance read for the addition |

#### 3.1.5 Step 3: Test plan (three test cases)

| Test | Setup | Call | Expected result | Path taken |
|---|---|---|---|---|
| D1: valid deposit | `createAccount(67, 10.0)` | `deposit(67, 5.0)` | No exception, balance becomes 15.0 | 1 → 2 → 4 |
| D2: negative amount | `createAccount(67, 10.0)` | `deposit(67, -5.0)` | `IllegalArgumentException`, balance still 10.0 | 1 → 2 → 3 |
| D3: zero amount (boundary) | `createAccount(67, 10.0)` | `deposit(67, 0.0)` | `IllegalArgumentException`, balance still 10.0 | 1 → 2 → 3 |

#### 3.1.6 Step 4: Pairs covered by each test

| Pair | D1 | D2 | D3 |
|---|---|---|---|
| P1 (`amount`, 1, 2 true) | | ✓ | ✓ |
| P2 (`amount`, 1, 2 false) | ✓ | | |
| P3 (`amount`, 1, 4) | ✓ | | |
| P4 (`initBalance`, 1, 4) | ✓ | | |
| **Pairs covered** | **3** | **1** | **1** |
D3 follows the same path as D2, so it covers no new pair. I included it because 0.0 is the boundary of the condition `amount <= 0`, so it would expose a mistake such as writing `<` instead of `<=`.
#### 3.1.7 Step 5: Coverage level
- Pairs covered by the three tests together: P1, P2, P3, P4 = **4 distinct pairs**
- All DU-pairs coverage = **100%**

D1 alone covers 3 of 4. I need D2 or D3 for P1, because a valid deposit never reaches the exception branch.

The 100% figure only covers the pairs that exist. `id` produces none, so a weakness in how `id` is handled cannot show up in this measure.

---
### 3.2 Definition Coverage (withdraw method)
#### 3.2.1 The code under test

```java
public void withdraw(int id, double amount){                               // 1
    if (amount <= 0) {                                                     // 2
        throw new IllegalArgumentException("Withdrawal amount must be positive."); // 3
    }
    if (amount > initBalance) {                                            // 4
        throw new IllegalArgumentException("Insufficient funds.");         // 5
    }
    this.initBalance = this.initBalance - amount;                          // 6
}
```
#### 3.2.2 Step 1: Definitions in the method

| Definition | Variable | Node | Uses reachable from it inside the method |
|---|---|---|---|
| d0 | `initBalance` (value on entry) | 1 | Node 4 (p-use), Node 6 (c-use) |
| d1 | `id` (parameter) | 1 | None |
| d2 | `amount` (parameter) | 1 | Node 2 (p-use), Node 4 (p-use), Node 6 (c-use) |
| d3 | `initBalance` (new value assigned) | 6 | None inside the method; read later by `getBalance`, `deposit` and `withdraw` |

**Total definitions: 4.** The criterion is **All-defs**: each definition must reach at least one of its uses in some test.

**Findings:**
- **d1 is never used.** `id` is never read, so no test can cover it.
- **d3 has no use inside `withdraw`.** It is only used by other methods. In the tests it is exercised through the `getBalance` call in the assertion after the withdrawal.
#### 3.2.3 Step 2: Test cases based on the definitions

| Test | Targets | Setup | Call | Expected result | Path taken |
|---|---|---|---|---|---|
| W1: valid withdrawal | d3 (also d0, d2) | `createAccount(67, 10.0)` | `withdraw(67, 5.0)`, then `getBalance(67)` | No exception, balance is 5.0 | 1 → 2 → 4 → 6 |
| W2: overdraft | d0 | `createAccount(67, 10.0)` | `withdraw(67, 50.0)` | `IllegalArgumentException`, balance still 10.0 | 1 → 2 → 4 → 5 |
| W3: invalid amount | d2 | `createAccount(67, 10.0)` | `withdraw(67, -5.0)` | `IllegalArgumentException`, balance still 10.0 | 1 → 2 → 3 |

- **W1** is the only test that reaches node 6, so it is the only one that exercises d3.
- **W2** targets d0. The balance on entry decides the outcome here, through the comparison at node 4.
- **W3** targets d2. It exercises the amount at its first use, the validation at node 2.
- No test is designed around d1, because it has no use to reach.
#### 3.2.4 Step 3: Coverage level

| Definition | W1 | W2 | W3 | Covered? |
|---|---|---|---|---|
| d0 (`initBalance` on entry) | ✓ (used at 4, 6) | ✓ (used at 4) | | Yes |
| d1 (`id`) | | | | **No (no use exists)** |
| d2 (`amount`) | ✓ (used at 2, 4, 6) | ✓ (used at 2, 4) | ✓ (used at 2) | Yes |
| d3 (`initBalance` assigned) | ✓ (via `getBalance` after the call) | | | Yes |

- Definitions covered: 3 of 4
- All-defs coverage = 3 / 4 = **75%**
- If only uses inside `withdraw` are counted, d3 is also uncovered and coverage is 2 / 4.
The gap is not a weakness in my test plan, because d1 cannot be covered by any test. Excluding it, the plan covers 3 of 3 achievable definitions (100%). Reaching 100% on all four would need a code change, for example making the methods use `id` to look up a per-account balance.

If I removed W1, coverage would drop to 2 / 4, because no other test reaches node 6. That is why a successful withdrawal is essential to the plan.