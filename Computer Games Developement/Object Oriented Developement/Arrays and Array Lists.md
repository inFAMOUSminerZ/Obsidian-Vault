### Arrays
Arrays are at their bases form a list of data that has a fixed size. By this I mean it may have 3 slots that can be filled. This has the benefit of rather than creating individual variables for each piece of data we can instead store all this data in an array. Two things to note about arrays
1. They can only hold a single data type. This is something like `String[]`. 
2. They are 0 indexed. This means the first item in the array is referenced by 0, not 1.
Take something like this in our main method:
```java
String[] cars = {"Blue", "Red", "Yellow"};
```
Here we see that we created a String array variable called cars that holds a list of Strings. Now how do we access this information? Well lets say we want to print it:
```java
String[] cars = {"Blue", "Red", "Yellow"};
System.out.println("First Car: " + cars[0]);
```
The way we accessed the data within the String array was we used `cars[0]`. This demonstrates what we said earlier where arrays are indexed at 0, so the first entry would be 0. The print we have above would print `"First Car: Blue"`.

But what if we want to input things into this array later by creating an array object? This is how you would do it:
```java
String[] cars = new String[3]; // the 3 sets the space within the array to 3 pieces of data
```
Now when we call `cars` we will be building an object that contains an array with a size of 3. Until we define what these hold they will output null if we ask for their values.

### Array Lists