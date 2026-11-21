**Tags**: [[Types]]

An enum is a powerful type of special class in java that stores a fixed set of named constants. They are like final variables. Lets take something like a family:

```java
public enum Family{
	Name1, Name2, Name3, Name4, Name5 
}
```

Each of these names is an object of the enum class "Family". Because they are objects we can get access to some cool things. For instance they are all scoped, so we don't just say `Name1`, we say `Family.Name1`.

One of the main reason to use things like this are to make switch cases for them. Since enum constants are basically variables they can be equated with equations and us