[[Encapsulation]], [[Types]], [[Constructors]]
Getters and Setters are often used for encapsulation. Getters return some value using a method and setters (also called mutators) set the values of some value within your code. 

For example:
```java
// the java file name
public class Test{

	private int number = 1; // and integer called number set to 1 and is private
	
	// our getter method which returns the value of number
	public int getNumber(){
		return number;
	}
	
	// our setter method which equates a global variable with the local variable, then sets the local variable to 2, without           changing the global variable
	public void setNumber(int number){
		this.number = number;
	}
	// a constructor that we can call to build the object from the class
	public Test(){
	}
	
}
```

And now we add the constructor so that when we add another class with a main method and do the following:
```java
public class Main{

	public static void main(string[] args){
		
		Test t = new Test(); //This is an initialisation.
		t.setNumber(10);
	
	}
	
}
```

As you can see we initialise a new Test object and pass in the number 10 with the getNumber method. If it was public we could do something like t.number = 10; BUT since it is private it is only changed in the created object not the template/blueprint of the class.