**Tags**: [[Types]]

An enum is a powerful type of special class in java that stores a fixed set of named constants. Lets take something like a family:

```java
public enum Family{
	Name1, Name2, Name3, Name4, Name5 
}
```

Each of these names is an object of the enum class "Family". Because they are objects we can get access to some cool things. For instance they are all scoped, so we don't just say `Name1`, we say `Family.Name1`. 