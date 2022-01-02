# Exception Handling 



## Exceptions 

exceptional handling is used in exceptional situations such as partner server is down or database is down 


Exception is an Object of class java.lang.Throwable 



checked exceptions: checked exceptions are dealt in exceptional situations because compiler guaranteees to sepcify in throw clause, and exception handling via a try/catch block 
These are the exceptions that are checked at compile time. If some code within a method throws a checked exception, then the method must either handle the exception or it must specify the exception using the throws keyword. 


Throwable -> Exceptions -> IOExceptions -FileNotFoundException/EOFException 
-> AWTException 

```java
iprivate static void checkedExceptionWithThrows() throws FileNotFoundException {
    File file = new File("not_existing_file.txt");
    FileInputStream stream = new FileInputStream(file);
}

private static void checkedExceptionWithTryCatch() {
    File file = new File("not_existing_file.txt");
    try {
        FileInputStream stream = new FileInputStream(file);
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    }
}
```

Some common checked exceptions in Java are IOException, SQLException and ParseException.




unchecked exceptions:  unchecked exceptions only happen in programming flaws/runtime or system errors. this is minimized at development &testing but it generally should be caught and almost never. Unchecked exceptions are not handled by compilers 


These are the exceptions that are not checked at compile time. In C++, all exceptions are unchecked, so it is not forced by the compiler to either handle or specify the exception. It is up to the programmers to be civilized, and specify or catch the exceptions. In Java exceptions under Error and RuntimeException classes are unchecked exceptions, everything else under throwable is checked. 


Java does not verify unchecked exceptions at compile-time. Furthermore, we don't have to declare unchecked exceptions in a method with the throws keyword. And although the above code does not have any errors during compile-time, it will throw ArithmeticException at runtime.

Some common unchecked exceptions in Java are NullPointerException, ArrayIndexOutOfBoundsException and IllegalArgumentException.

 

It's a good practice to use exceptions in Java so that we can separate error-handling code from regular code. However, we need to decide which type of exception to throw. The Oracle Java Documentation provides guidance on when to use checked exceptions and unchecked exceptions:

“If a client can reasonably be expected to recover from an exception, make it a checked exception. If a client cannot do anything to recover from the exception, make it an unchecked exception.”





Throwable -> Errors -> VirtualMachineError/LinkageError/NoClassDefFoundError 


Throwable -> RuntimeExceptions -> NullPointerException/ArrayIndexOutOfBoundsException/IllegalArgumentException/ClassCastException/NumberFormatException


## try...catch .. finally blocks 

When executing Java code, different errors can occur: coding errors made by the programmer, errors due to wrong input, or other unforeseeable things.

When an error occurs, Java will normally stop and generate an error message. The technical term for this is: Java will throw an exception (throw an error).

The try statement allows you to define a block of code to be tested for errors while it is being executed.

The catch statement allows you to define a block of code to be executed, if an error occurs in the try block.

```java
try{

}catch(Exception e){
    
}

```

The finally statement lets you execute code, after try...catch, regardless of the result. no code will run after finally block 

```java
try{

}catch(Exception e){
    
}finally{

}

```





```java
import javax.imageio.IIOException;

public class Test {

    public static void main(String []args){
        int [] a = {1,2,3,4,5};
        try { 
           
           a[5] = 10;
            
        } catch (ArrayIndexOutOfBoundsException e) {
            
         
            System.out.println("I handled array out of bounds");
 
        }finally{
            System.out.println("this will execute regardless");
        }
        // useless         System.out.println("but code will run after finally. you cannot do this");




    }
    
}
```





## throw keyword 
the throw statement allows you to create a custom error. 

The throw statement is used together with an exception type. There are many exception types available in Java: ArithmeticException, FileNotFoundException, ArrayIndexOutOfBoundsException, SecurityException


```java

import javax.imageio.IIOException;

public class Test {

    public static void main(String []args){
     int number = 8;
     
     if(number < 10){
      throw new ArithmeticException("i told you it is greater or equals to 10");
     }else{
         System.out.println(number);
     }

    }
    
}


```


Here are couple of rules when it comes to exceptions & method overriding.

Rule 1: If the super class method does not declare an exception, then the overriding method in the subclass cannot declare a checked exception, but can declare an unchecked exception.

Rule 2: 

(a) If the super class method declares a checked exception, then the overriding method in the subclass can declare same exception or a subclass exception or no exception at all, but cannot declare parent exception.

(b) If the super class method declares an unchecked exception, then the overriding method can declare any unchecked exception or no exception at all, but cannot declare a checked exception.


When to use throws throw VS try-catch in Java?

Answer: The “throws” keyword is used to declare the exception with the method signature. The throw keyword is used to explicitly throw the exception. The try-catch block is used to handle the exceptions thrown by others.

 Can we use throws, try and catch in a single method?

Answer: No. You cannot throw the exception and also catch it in the same method. The exception that is declared using throws is to be handled in the calling method that calls the method that has thrown the exception.

What happens when a catch block throws an exception?

Answer: When an exception is thrown in the catch block, then the program will stop the execution. In case the program has to continue, then there has to be a separate try-catch block to handle the exception raised in the catch block.


```java

import javax.imageio.IIOException;

public class Test {

    public static void main(String []args){
        int [] a = {1,2,3,4,5};
        try { 
           
           a[5] = 10;
            
        } catch (ArrayIndexOutOfBoundsException e) {
            
         
           throw e;
 
        }finally{
            System.out.println("this will execute regardless");
        }



    }
    
}


```


## try with rsources 


general syntax 

```java

try(java.lang.AutoCloseable){

}

```
remember catch and finally are not required here 


### AutoCloseable hierachy 
java.lang.AutoCloseable -> java.io.Closeable <- java.net.Socket / java.util.Scanner  





Simply put, to be auto-closed, a resource has to be both declared and initialized inside the try:

```
try (PrintWriter writer = new PrintWriter(new File("test.txt"))) {
    writer.println("Hello World");
}

```

Replacing try–catch-finally With try-with-resources. The simple and obvious way to use the new try-with-resources functionality is to replace the traditional and verbose try-catch-finally block.


The first is a typical try-catch-finally block:
```java
Scanner scanner = null;
try {
    scanner = new Scanner(new File("test.txt"));
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} finally {
    if (scanner != null) {
        scanner.close();
    }
}
```
And here's the new super succinct solution using try-with-resources:

```java
try (Scanner scanner = new Scanner(new File("test.txt"))) {
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException fnfe) {
    fnfe.printStackTrace();
}
```

try-with-resources With Multiple Resources
We can declare multiple resources just fine in a try-with-resources block by separating them with a semicolon:
```java
try (Scanner scanner = new Scanner(new File("testRead.txt"));
    PrintWriter writer = new PrintWriter(new File("testWrite.txt"))) {
    while (scanner.hasNext()) {
	writer.print(scanner.nextLine());
    }
}
```


## supressed exceptions 

Suppressed exceptions, as name suggest, are exceptions thrown in the code but were ignored somehow. If you remember try-catch-finally block execution sequence and how they return any value or exceptions, you will recall that exceptions thrown in finally block are suppressed if an exception is thrown in try block also. Before java 7, you were informed about these exceptions by logging if implemented, but you didn’t have any control over these types of exceptions once finally block is over.

In Java 7, perhaps the most common use case for encountering suppressed exceptions is when a try-with-resources statement. When we encounter an exception within the try block, application tries to close the resource. If it encounters multiple exceptions which may occur while closing AutoCloseable resources, additional exceptions are attached to a primary exception as suppressed exceptions.
For example while writing to output stream, an exception can be thrown from the try block, and up to two exceptions can be thrown from the try-with-resources statement when it tries to close the stream.

If an exception is thrown from the try block and one or more exceptions are thrown from the try-with-resources statement, then those exceptions thrown from the try-with-resources statement are suppressed, and the exception thrown by the block is the one that is thrown by the closeStream() method.


## Exception Chaining 

Chained Exception helps to identify a situation in which one exception causes another Exception in an application.

For instance, consider a method which throws an ArithmeticException because of an attempt to divide by zero but the actual cause of exception was an I/O error which caused the divisor to be zero.The method will throw the ArithmeticException to the caller. The caller would not know about the actual cause of an Exception. Chained Exception is used in such situations.
We need to chain the exceptions to make logs readable. Let's write two examples. First without chaining the exceptions and second, with chained exceptions. Later, we will compare how logs behave in both of the cases.

To start, we will create a series of Exceptions:

```java

public class MainClass {
    public void main(String[] args) throws Exception {
        getLeave();
    }

    public getLeave() throws NoLeaveGrantedException {
        try {
            howIsTeamLead();
        } catch (TeamLeadUpsetException e) {
             throw new NoLeaveGrantedException("Leave not sanctioned.", e);
        }
    }

    public void howIsTeamLead() throws TeamLeadUpsetException {
        throw new TeamLeadUpsetException("Team lead Upset.");
    }
}
```


## Best Pratice 

- use checked exceptions for recoverable conditions and runtime exceptions for programming errors 

use checked exceptions for exceptional conditions that should be handled by what you consider part of your application logic, e.g: user typed in a non existing user name to log in, user tried to save and item beyond the limit allowed for her subscription, etc. That way the client of the code that finds the exceptional condition is forced to at least acknowledge the fact that the condition might occur and hopefully will handle it in the most appropriate way
use unchecked exceptions to fail early and noisily under circumstances not under your control and from which you cannot recover with application logic, e.g: your function receives the wrong parameters as arguments: sounds like the perfect scenario to throw an 'illegal argument exception', which is a runtime exception in most of programming languages out there

Checked Exceptions are great, so long as you understand when they should be used. The Java core API fails to follow these rules for SQLException (and sometimes for IOException) which is why they are so terrible.

Checked Exceptions should be used for predictable, but unpreventable errors that are reasonable to recover from.

Unchecked Exceptions should be used for everything else.

I'll break this down for you, because most people misunderstand what this means.

Predictable but unpreventable: The caller did everything within their power to validate the input parameters, but some condition outside their control has caused the operation to fail. For example, you try reading a file but someone deletes it between the time you check if it exists and the time the read operation begins. By declaring a checked exception, you are telling the caller to anticipate this failure.
Reasonable to recover from: There is no point telling callers to anticipate exceptions that they cannot recover from. If a user attempts to read from an non-existing file, the caller can prompt them for a new filename. On the other hand, if the method fails due to a programming bug (invalid method arguments or buggy method implementation) there is nothing the application can do to fix the problem in mid-execution. The best it can do is log the problem and wait for the developer to fix it at a later time.
Unless the exception you are throwing meets all of the above conditions it should use an Unchecked Exception.

Reevaluate at every level: Sometimes the method catching the checked exception isn't the right place to handle the error. In that case, consider what is reasonable for your own callers. If the exception is predictable, unpreventable and reasonable for them to recover from then you should throw a checked exception yourself. If not, you should wrap the exception in an unchecked exception. If you follow this rule you will find yourself converting checked exceptions to unchecked exceptions and vice versa depending on what layer you are in.

For both checked and unchecked exceptions, use the right abstraction level. For example, a code repository with two different implementations (database and filesystem) should avoid exposing implementation-specific details by throwing SQLException or IOException. Instead, it should wrap the exception in an abstraction that spans all implementations (e.g. RepositoryException


- do not ignore exceptions 
- include failure capture info in detail messagse 

- include failture-capture information in detail messages 



- throw exceptions appropriate to the abstraction 

an exception is thrown when a fundamental assumption of the current code block is found to be false.

Example 1: say I have a function which is supposed to examine an arbitrary class and return true if that class inherits from List<>. This function asks the question, "Is this object a descendant of List?" This function should never throw an exception, because there are no gray areas in its operation - every single class either does or does not inherit from List<>, so the answer is always "yes" or "no".

Example 2: say I have another function which examines a List<> and returns true if its length is more than 50, and false if the length is less. This function asks the question, "Does this list have more than 50 items?" But this question makes an assumption - it assumes that the object it is given is a list. If I hand it a NULL, then that assumption is false. In that case, if the function returns either true or false, then it is breaking its own rules. The function cannot return anything and claim that it answered the question correctly. So it doesn't return - it throws an exception.


- use eceptions only for exceptional conditions, do not use them for regular control flow 



- avoid uncessary use of checked exceptions -- used careless = unpleasant API 
make judagement based on preventable exceptional condition and recoverable


- favor the use of standard exceptions 
easy to understand API, API client programs are easy to read 
standard exceptions are : IllegalArgumentException, NullPointerException, IndexOfBoundsException

- document all exceptions throw by each method 

- take time to carefully document all exceptions 


- for checked exceptions, declare and document each exception precisely 
- for uncheck exceptions, document them too , only document but do not declare , document unchecked exceptions in interface methods. check parameters for validity 


## Assertion 


syntax: 

```java
assert boolean-expressin 

assert boolean-expression: messages 
```

beneifts of assertions are, it is effecive in detecting bugs during development, assertion -> obviously true. and it serves as documentations 


Assertions are disabled by default 
assertions throw universal AssertionError
nonpublic methods are assertions 

assertions complement unit testings 
automated repeatable testing for program correctness 
it is the part of junit methods, assertions are less granular 

### disable & enable assertions 
assertions are disabled by default 
-ea or -enableassertions 
-ea & -da at class and package level 

java -ea: packageName ClassName 

java -ea -da: packageName ClassName 



```java
import javax.imageio.IIOException;
//java -ea Tets.java
public class Test {

    public static void main(String []args){
            assert 1 == 1;

            assert 1 > 2: "this is wrong";
            /*
Exception in thread "main" java.lang.AssertionError: this is wrong
        at Test.main(Test.java:8)

            */
    }
    
}


```


what is the superclass of all Exception classes? Throwable 

checked exception that you need to extend is. Exception 

always document unchecked exceptions precisely, but do not specify them in method declaration 

















