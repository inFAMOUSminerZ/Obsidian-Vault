[[Types]][[Getters and Setters]]
The list functionality we will be looking at here is actually a type. We will create it the same way we would create an object in main. Something like the following:
```java
public class Main{

	public static void main(string[] args){
		Animal a = new Animal;
		a.setAnimal("Dog");
		
		// these List and ArrayList classes should be imported from Java.Util
		List<Animal> animals = new ArrayList<Animal>();
		
		animals.add(a);
	
	}
	
}
```

As you can see above we create (presuming we created a class animal with a constructor and a setAnimal method) an object and set the animal string variable in it to "Dog". We then create a list called animals that expects an object of the Animal class and have that create a new array list that expects an object of the Animal class.

Finally we access the list object and add our new object a (which is of class Animal) and add it to the ArrayList.