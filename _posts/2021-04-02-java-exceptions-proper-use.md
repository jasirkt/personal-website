---
title: "How to Use Java Exceptions Properly"
published: true
---

Exceptions are an excellent way of handling errors or unexpected situations during the flow of a program. Exceptions also ensure that the code is kept clean by making sure that the error handling code is not mixed with the original code.

The Exception class is at the top of Exception Heirarchy. 


Java provides 2 broad types of exceptions, Checked and Unchecked exceptions.

### Checked Exceptions
These are the exceptions that must be caught. Your program won't compile unless you write code for handling these type of exceptions

### Unchecked Exceptions
These are the exceptions that can't be predicted at compile time. Catching or handling these type of exceptions everywhere might not be feasible. It is not mandatory to catch or throw these exceptions for your code to compile, but your program might stop running when such an exception occurs.

Unchecked exceptions in java will be an object of RunTimeException class or its subclasses. 

### adding a single catch block for all Exceptions

It is not recommended to do this. First of all Exceptions were not designed to be this way.

# Best Practices

### Be more specific
Don't just throw around the top-level `Exception` class. Use more specific Exception classes like `NumberFormatException` or `FileNotFoundException`. This can help everyone in your team use the method and handle exceptions appropriately. 

##### Change this
```java
try {
    //do something
} catch(Exception ex) {
    //handle exception 
}
```

### Do not log and throw exceptions. 
Logging and rethrowing the exception will result in multiple handling of the same exception. 

```java 
try {
    //do something
} catch (MyException ex) {
    log(ex);
    throw ex; //avoid this!
}

```

To avoid this, make sure the message in the exception thrown is pretty clear, so that whoever is handling it can log it properly.