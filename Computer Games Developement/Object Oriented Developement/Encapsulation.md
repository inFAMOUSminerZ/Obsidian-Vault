Encapsulation is achieved by creating a private variable that stores some value. Then we have a public **getter** method. Something like so
```java
public class Test{
	private int number = 1;
	
	public int getNumber(){
		return number;
	}
	
}
```
Here we set a private int named "number" to 1 and return it in the getter. Now we need to retrieve that number to set it. This is called a **mutater**. Something like this:
```java
public class Test{
	private int number = 1;
	
	public int getNumber(){
		return number;
	}
	
	public void setNumber(int number){
		this.number = number;
		number = 2;
	}
	
}
```
Now if we create a new Test object with a constructor we will be able to pass a number into the **setNumber** method without accessing the data in the private int.