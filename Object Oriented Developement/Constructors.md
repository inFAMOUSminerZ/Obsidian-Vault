Constructors use blueprints (classes) to create objects. They execute some function such as setting a value or returning a value and when the constructor is called it initialises a class which has one of these constructor methods and uses the blueprint within the class to create a new object.

Take something like this:
```java 
public class Test{

	private int number = 1;
	
	public int getNumber(){
		return number;
	}
	
	public void setNumber(int number){
		this.number = number;
	}
	
	public Test(){
	}
	
}
```

And now we add the constructor so that when we add another class with a main method and do the following:
```java
public class Main{

	public static void main(String[] args){
		
		Test t = new Test(); //This is an initialisation.
		t.setNumber(10);
	
	}
	
}
```

As you can see we initialise a new Test object and pass in the number 10 with the setNumber method. This only changes the new objects instance variable with setNumber as t is a single object, not the blueprint. It is not the Test class itself.