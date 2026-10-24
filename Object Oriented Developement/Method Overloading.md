[[Method Overloading]], [[Types]]
Method overloading is when you want to pass multiple different pieces of data through a method in multiple different ways. Something like:
```java
System.out.println(2);
System.out.println("Hello");
```
The source method here is println(). It has two methods. One accepts a string and the other accepts an int. This makes it so if we had something like this:
```java
public void method1(int number){
	System.out.println("Method 1 recieved an int.");
}

// and we also have this method

public void method1(String string){
	System.out.println("Method 1 received a String.");
}
```
You can see both methods are the same but have different parameters. If I have something like:
```java
public static void main(String[] args){
	Method("string");
}
```
It would print "Method 1 received a String.". This is because passing in a string to the first method does not work but the second does and Java knows this.

You can use Method Overloading in a few ways, such as distinguishing between inputs for a user like we did above, or println itself which uses method overloading to make the case universal instead of printlnString, printlnint, printlndouble, etc...