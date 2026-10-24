Types are a few things such as int or char or even String. They come in two categories, primitive and non-primitive.

**Primitive:** Primitive data types are predefined by the language. They represent the building blocks of data such as doubles (fractions) or chars (individual characters) **Examples: int, char, double**.

**Non-primitive:** Non-Primitive data types are defined by the programmer (with the exception of String) and use primitive data types. Instead of storing actual data they store a reference or memory address in heap. They always start with a capital letter in Java. **Examples: String, Array, Class**.

**Example File Class**
Here in this file we have our main class called UserExample. When we call main we create a new user which is specified with the string array we pass through main. However, we need to know what User is. We need to define its type and what it references in heap.
```java
public class UserExample{

	public static void main(String[] args){
	
		System.out.println("User!")
		User u = new.User();
	
	}
	
}
```
**Example User Class**
This is where we define what User means. We have User contain 2 strings that have a name and a membership.
```java
public class User{

	String name;
	String membership;
	
	}
	
}
```
**Changing UserExample**
Now we set the values within the main method.
```java
public class UserExample{

	public static void main(String[] args){
	
		System.out.println("User!")
		
		User u = new.User();
		u.name = "Joan";
		u.membership = "Gold";
			
		User u2 = new.User();
		u2.name = "Brandon";
		u2.membership = "Platinum";
			
		System.out.println(u.name);
		System.out.println(u2.name);
	
	}
	
}
```
**NOTE:** Non-primitives if not defined will return a base value of NULL, while primitives will return a base value of 0.