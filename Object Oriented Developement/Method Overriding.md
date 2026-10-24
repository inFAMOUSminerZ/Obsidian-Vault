Method overriding
```java
public class Animal{
	public void makeSound(){
		System.out.println("Animal Sound");
	}
}

public class Dog extends Animal{
	@Override
	public void makeSound(){
		System.out.println("Dog Sound");
	}
}
```

Now if we ever create a dog object we will be able to do dogName.makeSound() and it will print "Dog Sound" instead of "Animal Sound" because it is a method contained in the dog object.

If we did not extent this and just had another makeSound() method in another class, depending on how the files were structured there would be a variety of issues