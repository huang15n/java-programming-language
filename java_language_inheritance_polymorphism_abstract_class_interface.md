

# Advanced OOP concept 



## Inheritance 


duplicate code means maintenance nightmare and the ultimate solution is inheritance 


if superclass acquire new methods, then you can simply compile the modified superclass and replace the old .class file with this newer one 



### subclass 
it is specialized versions of superclasses, it inherits members, add new members and override superclass methods 

superclass is the supertype or base class 
subclass is the subtype or derived class 


### extending a class 
"extends" keywords, one class can extends only one class 

class in a package are like family 


### inhertiance accessibility
Private: The access level of a private modifier is only within the class. It cannot be accessed from outside the class.
Default: The access level of a default modifier is only within the package. It cannot be accessed from outside the package. If you do not specify any access level, it will be the default.
Protected: The access level of a protected modifier is within the package and outside the package through child class. If you do not make the child class, it cannot be accessed from outside the package.
Public: The access level of a public modifier is everywhere. It can be accessed from within the class, outside the class, within the package and outside the package.


```java


// PackageClass moved to package_name

package package_name;

public class PackageClass{

    private int value;

    public PackageClass(){

    }
    public PackageClass(int value){
        this.value = value;
    }

    public int getValue(){
        return this.value;
    }

    public void setValue(int value){
        this.value = value;
    }


}


// within the same package 
package package_name;

public class ProtectedClass extends PackageClass{

    public  ProtectedClass(){
        super();

    }

    public ProtectedClass(int value){
        super(value);
    }


    public static void main(String [] args){
        ProtectedClass pc = new ProtectedClass(100);
        System.out.println(pc.getValue());

        
    }





    
}




// PackageClass 

package package_name;

public class PackageClass{

     int value;

     PackageClass(){

    }
  PackageClass(int value){
        this.value = value;
    }

 int getValue(){
        return this.value;
    }

void setValue(int value){
        this.value = value;
    }


}

// within the same package 

package package_name;

class DefaultClass extends PackageClass {

    DefaultClass(int value){
        super(value);
    }





    public static void main(String [] args){
        DefaultClass dc = new  DefaultClass(100);
        System.out.println(dc.getValue());

        
    }
    
}


```


```java

// PackageClass 

package package_a;

public class A{
         private int privateValue = 10;
         public int publicValue = 20;
         int defaultValue = 30;
         protected int protectedValue = 40;

}

// same package 
package package_a;

public class B extends A{

 

    public static void main(String [] args){
     // compiler errror  System.out.println(privateValue);
    System.out.println(defaulteValue);
    
    System.out.println(protectedValue);
    
    System.out.println(publicValue);

        
    }





    
}


// different package 
 package package_b;

public class B extends A{

 

    public static void main(String [] args){
     // compiler errror  System.out.println(privateValue);
    System.out.println(defaulteValue);
    
    System.out.println(protectedValue);
    
    System.out.println(publicValue);

        
    }





    
}


```



### is-a Test versus has a test 

is-a test is the most fundamental test for inheritance 

An IS-A relationship is inheritance. The classes which inherit are known as sub classes or child classes. On the other hand, HAS-A relationship is composition.

In OOP, IS-A relationship is completely inheritance. This means, that the child class is a type of parent class. For example, an apple is a fruit. So you will extend fruit to get apple.

class Apple extends Fruit {

}
On the other hand, composition means creating instances which have references to other objects. For example, a room has a table. So you will create a class room and then in that class create an instance of type table.

class Room {

    Table table = new Table();

}
A HAS-A relationship is dynamic (run time) binding while inheritance is a static (compile time) binding. If you just want to reuse the code and you know that the two are not of same kind use composition. For example, you cannot inherit an oven from a kitchen. A kitchen HAS-A oven. When you feel there is a natural relationship like Apple is a Fruit use inheritance.


## Polymorphism 


polymorphism means the reference type and actual object type can be different 

```java

SupterType superObject = new Subtype();
// reference type         object type 
```


compiler uses reference type to decide whether a metod can be invoked 


```java

SupterType superObject = new Subtype();
// reference type         object type 
superObject.subMethod(); // compiler error 
```


JVM uses object type to decide which method is invoked. it invokes the most specific version of method implementation 
```java

public class SuperClass{


    public void method(){
        System.out.println("this is from super class ");
    }

}
import java.util.ArrayList;

public class SubClass extends SuperClass {

 @Override
    public void method(){
        System.out.println("this is from subclass");
    }



    public static void main(String []args){
     ArrayList<SuperClass> objects = new ArrayList<>();
     objects.add(new SubClass());
     objects.add(new SubClass());
     objects.add(new SubClass());

        for(SuperClass object : objects ){
            object.method();
        }






    }
    
}

```
The polymorphic part is when different code is executed for the same method call. The loop does the same thing everytime, but different instance methods may actually be getting called.


### Casting Objects & instanceof Operator




primivate type casting 

```java
//implicit : 
typeBigger f = typeSmallerValue;

// explicit 
explicit typeSmaller f = (typeSmaller)typeBiggerValue;

```


#### class casting implicit 

```java

type methodName(SupperClass object){

}

methodName(new SubClass());

```


when we use explict casting, the subclass-specific methods are no longer valid, that gives a ClassCastException at runtime 

```java

SupterType superObject = new Subtype();
// reference type         object type 
superObject.subMethod(); // compiler error 
((SubClass)superObject).subMethod();



type methodName(SupperClass object){
         object.subMethod(); // compiler error 

         ((Subclass)object).subMethod(); // runtime error 
}

methodName(new SubClass());

```


### instanceof operator 

objectA instanceof objectB 

the object type is what matters 

```java

SupterType superObject = new Subtype();
// reference type         object type 
if(object instanceof SubClass){
superObject.subMethod(); // compiler error 
((SubClass)superObject).subMethod();
}






public class SubClass extends SuperClass {

 @Override
    public void method(){
        System.out.println("this is from subclass");
    }

    public void method2(){
        System.out.println("this is subclass specific method");
    }



    public static void main(String []args){
   
       callMethod(new SubClass());


    }

    public static void callMethod(SuperClass object){
        object.method();

        if(object instanceof SubClass)
        ((SubClass)object).method2();

    }
    
}


```




#### java's Type Safety -- static type checking 

The big benefit of static type checking is that it allows many type errors to be caught early in the development cycle. Static typing usually results in compiled code that executes more quickly because when the compiler knows the exact data types that are in use, it can produce optimized machine code (i.e. faster and/or using less memory). Static type checkers evaluate only the type information that can be determined at compile time, but are able to verify that the checked conditions hold for all possible executions of the program, which eliminates the need to repeat type checks every time the program is executed.

static type checking: 


```java
int a = float_value;
int b = (int) float_value;

SuperClass s = new SubClass();
s.subMethod();
((SubClass) s).subMethod();

```
or generics 

dynamic type checking : 


ClassCastException is a runtime exception raised in Java when we try to improperly cast a class from one type to another. It's thrown to indicate that the code has attempted to cast an object to a related class, but of which it is not an instance.

For a more in-depth introduction to exceptions in Java, take a look here. It's really pretty simple: if you are trying to typecast an object of class A into an object of class B, and they aren't compatible, you get a class cast exception.

Let's think of a collection of classes.

class A {...}
class B extends A {...}
class C extends A {...}
You can cast any of these things to Object, because all Java classes inherit from Object.
You can cast either B or C to A, because they're both "kinds of" A
You can cast a reference to an A object to B only if the real object is a B.
You can't cast a B to a C even though they're both A's.


ArrayIndexOutOfBoundsException is also a runtime error 

in conclusion: strong typing has no loopholes as opposed to weak type 



## Method overriding 

method override redefines the behaviour of superclass method which 1. add new behaviour 2. extend behvaiour 3. providing better implementation 


generally speaking, supertype defines contract and common protocol and mehtod overriding is agreeing to fulfil this contract 



rule1:Same parameters + same or compatible (only for non-primitive) return types
rule2: cannot be less accessible 


## super keyword and  Constructor chaining 
this allows access to superclass method which is not override ~ direct or super. overriden ~ super. keep in mind that we cannot use in static method. 
it allows access for hidden field. 


```java

public class SuperClass{

    
    private int value;

    public SuperClass(){
        
    }

    public SuperClass(int value){
this.value = value;
    }

    

 
}

public class SubClass extends SuperClass {

    public SubClass(int value){
        super(value);
    }

    public static void main(String []args){
        SuperClass sc = new SubClass(10);
        
    }
  

   
}

// redundant 

 

public class SubClass extends SuperClass {

    // no use private int value;

    public SubClass(int value){
        super(value);

    }

 


  

   
}


```


###### you can either use this() or super(), but never both. with overloaded constructor, the last invoked will ccall super() 



super keyword invokes superclass constructor. it must be the first statement unless this() keyword is used.

```java



public class SubClass extends SuperClass {
    doubel value2;


    public SubClass(int value,double value2){
        this(value,value2);
    }

    public SubClass(int value){
        super(value);
    }

    public static void main(String []args){
        SuperClass sc = new SubClass(10);

    }
  

   
}



public class SubClass extends SuperClass {

    private int value;

    private double value2;

    public SubClass(int value, double value2){
        super(value);
        this.value2 = value2;
    }

    public SubClass(int value){
        super(value);

    }

 


  

   
}


```



```java



public class SubClass extends SuperClass {

 @Override
    public void method(){
        super.method();
        System.out.println("this is from subclass");
    }

 


// same 
    public static void main(String []args){
   
       SuperClass superClassObject =new SubClass();
       superClassObject.method();

       System.out.println("**********************************");
       ((SubClass) superClassObject).method();


    }

   
}

```





the motivation of constructor chaining is because it is inherited methods might depend on superclass state, and every super classe must be intialized first, constructor initialize object's state 



###### if not provided, compiler will automatically insert a super() constructor 

 ```java


public class SubClass extends SuperClass {
    public SubClass(){
        // super();
    }

 

    public static void main(String []args){
        SuperClass sc = new SubClass(10);

    }
  

   
}


 ```


 ##### superclass constructor cannot be invoked which can cause compiler error 

 ```java

public class SubClass extends SuperClass {
    public SubClass(int value){
        // cannot work here this();
       // cannot work SuperClass();
       super();


    }

 

    public static void main(String []args){
        SuperClass sc = new SubClass(10);

    }
  

   
}


 ```


## method binding 
Binding means an association of method call to the method definition. The picture below clearly shows what is binding. There are two types of Binding: Static and Dynamic Binding in Java.


method signature bindling -- compiler checks if reference type has comptaible method 
it writes method signature dtails into bytecode 
The reason for the binding of private, final and static methods during the compile-time is that the compiler determines the type of the class at the compile-time and therefore we can not override them during the runtime. Another reason is that the static binding of methods provides better performance than the runtime binding. The compiler becomes aware of these methods and understands that method overriding is not possible with such methods.

```java

public class SuperClass{


    public static void method(){
        System.out.println("this is from super class ");
    }

}



public class SubClass extends SuperClass {

 
    public static void method(){
 
        System.out.println("this is from subclass");
    }

 



    public static void main(String []args){
   
       SuperClass superClassObject =new SubClass();
   SuperClass.method();
     SubClass.method();
    // above shown different outputs 

    System.out.println("**********************************");

    SuperClass subClassObject = new SubClass();
  subClassObject.method();
  superClassObject.method();
  // all uses superclass's static method 
  /*
The reference for the parent class and the child class is the same  That is, a single object refers to both of them.
Since the method is static, the compiler is aware that this method can not be overridden in the child class and it knows which method to call. Therefore there is no ambiguity and the output is the same for both cases.


  */


 

    }

   
}


```
therefore, static method is run at compile time or early binding 




instance method is compiled by JVM based on obejct type 


static method is for runtime or late binding 



note: fields are early bounded 




```shell

javac *.java

javap -v ClassName.class 

```


### Dynamic Binding or Late Binding in Java

When the compiler resolves the method call binding during the execution of the program, such a process is known as Dynamic or Late Binding in Java. We also call Dynamic binding as Late Binding because binding takes place during the actual execution of the program.

The best example of Dynamic binding is the Method Overriding where both the Parent class and the derived classes have the same method. And, therefore the type of the object determines which method is going to be executed.

The type of object is determined during the execution of the program, therefore it is called dynamic binding.


From the above code, we got different output because:

We have not declared the methods as static in the code.
During compilation, the compiler has no idea of which method to call. This happens because the compiler doesn’t go according to the type of the object but it checks only according to the reference variable. Therefore the binding gets delayed to runtime, so the respective version of the method will be called on the basis of the type of the object.


```java

public class SuperClass{


    public void method(){
        System.out.println("this is from super class ");
    }

}

public class SubClass extends SuperClass {

 
    public  void method(){
 
        System.out.println("this is from subclass");
    }

 



    public static void main(String []args){

        SuperClass sc = new SubClass();
        sc.method();
   
       
    }

   
}

```




#### not override 
- final methods ~ final returnType methodName(){}
- fileds ~ instance fields or static fields 
- static method 


#### static methods & overriding 

 difference between static and dynamic binding in Java.

Static binding happens at compile-time while dynamic binding happens at runtime.
Binding of private, static and final methods always happen at compile time since these methods cannot be overridden. When the method overriding is actually happening and the reference of parent type is assigned to the object of child class type then such binding is resolved during runtime.
The binding of overloaded methods is static and the binding of overridden methods is dynamic.


- it cannot use super keyword which qualified with superclass name 
- it canont hide instance method, static means no states 
- it cannot be overried by instance method 



## Object class 
java.lang.Object is the mother of all classes, it is the super clss of everything 

the main purpose is that it acts as polymorphic type which includes core methods 

core methods including: 
- toString(), returns a string representation of object
 default: memory addresss
##### we always overiride toString() method which is very helpful for debuggin and returning all relevant info 


- hashCode(), returns object's hascode which is the memory address hexadecimal used in hashtable. By definition, if two objects are equal, their hash code must also be equal. If you override the equals() method, you change the way two objects are equated and Object's implementation of hashCode() is no longer valid. Therefore, if you override the equals() method, you must also override the hashCode() method as well.



- equals(object) is used to test object's equality, default uses == operator 

- getClass() , the final method that returns Class object. Class object-> class name, superclass name, method name .... 


- clone() protected methods that returns a copy of this object 




### final keywords and final Class 

final keywords prevents inheritance
when all methods are final. 
or class semantics invariants is final such as String. 
this is not extensible, but instantiable,

```java
final class ClassName{} 

```


private constructors are neither extendible nor instantiatable

enforce noninstantiability with a private constructor, utility classes like Math, saves up heap space 
it cannot be invoked from subclasses -- no constructor chaining no subclass 


state -> final 
utility class -> private constructor 



## Abstract Class 
Why And When To Use Abstract Classes and Methods?
To achieve security - hide certain details and only show the important details of an object.

Note: Abstraction can also be achieved with Interfaces

Data abstraction is the process of hiding certain details and showing only essential information to the user.
Abstraction can be achieved with either abstract classes or interfaces
The abstract keyword is a non-access modifier, used for classes and methods:

Abstract class: is a restricted class that cannot be used to create objects (to access it, it must be inherited from another class).

Abstract method: can only be used in an abstract class, and it does not have a body. The body is provided by the subclass (inherited from).

 

```java

abstract class AbstractClass{

}

```

 
Rules
Note 1: there are cases when it is difficult or often unnecessary to implement all the methods in parent class. In these cases, we can declare the parent class as abstract, which makes it a special class which is not complete on its own.

A class derived from the abstract class must implement all those methods that are declared as abstract in the parent class.

Note 2: Abstract class cannot be instantiated which means you cannot create the object of it. To use this class, you need to create another class that extends this this class and provides the implementation of abstract methods, then you can use the object of that child class to call non-abstract methods of parent class as well as implemented methods(those that were abstract in parent but implemented in child class).

Note 3: If a child does not implement all the abstract methods of abstract parent class, then the child class must need to be declared abstract as well.



```java

//it must be abstract in order to use abstract method, public class AbstractClass 
public abstract class AbstractClass {
    // The type AbstractClass must be an abstract class to define abstract methods :
    // private abstract int variable;

    /*
    public AbstractClass(int variable){
        this.variable = variable;
    }

    */

 /* you cannot implement an abstract method 
    public abstract void method(){
        System.out.println("this is abstract method from Abstract Class");
    }

*/

//        public abstract void method(){};


        public abstract void method();
    
}


public class SubClass extends AbstractClass{

    private int variable;
    public SubClass(int variable){
      // you cannot do this  super(variable);
       this.variable = variable;
    }

    @Override
    public void method(){
        System.out.println("implement abstract method");
    }



    public static void main(String []args){
    // you cannot do this because it is not instantiable      AbstractClass ac = new AbstractClass(10);
        
     AbstractClass ac = new SubClass(10);

     ac.method();


    }

    
    
}


```


 

 Key Points:

An abstract class has no use until unless it is extended by some other class.
If you declare an abstract method in a class then you must declare the class abstract as well. you can’t have abstract method in a concrete class. It’s vice versa is not always true: If a class is not having any abstract method then also it can be marked as abstract.
It can have non-abstract method (concrete) as well.

Following are some important observations about abstract classes in Java.

An instance of an abstract class can not be created.
Constructors are allowed.
We can have an abstract class without any abstract method.
Abstract classes can not have final methods because when you make a method final you can not override it but the abstract methods are meant for overriding.
We are not allowed to create object for any abstract class.
We can define static methods in an abstract class

For now lets just see some basics and example of abstract method.
1) Abstract method has no body.
2) Always end the declaration with a semicolon(;).
3) It must be overridden. An abstract class must be extended and in a same way abstract method must be overridden.
4) A class has to be declared abstract to have abstract methods.
5) abstract class can have constructors
an abstract class can have a constructor. Consider this:
```java
abstract class Product { 
    int multiplyBy;
    public Product( int multiplyBy ) {
        this.multiplyBy = multiplyBy;
    }

    public int mutiply(int val) {
       return multiplyBy * val;
    }
}

class TimesTwo extends Product {
    public TimesTwo() {
        super(2);
    }
}

class TimesWhat extends Product {
    public TimesWhat(int what) {
        super(what);
    }
}
```
The superclass Product is abstract and has a constructor. The concrete class TimesTwo has a constructor that just hardcodes the value 2. The concrete class TimesWhat has a constructor that allows the caller to specify the value.

Abstract constructors will frequently be used to enforce class constraints or invariants such as the minimum fields required to setup the class.

NOTE: As there is no default (or no-arg) constructor in the parent abstract class, the constructor used in subclass must explicitly call the parent constructor.
 

You would define a constructor in an abstract class if you are in one of these situations:

you want to perform some initialization (to fields of the abstract class) before the instantiation of a subclass actually takes place
you have defined final fields in the abstract class but you did not initialize them in the declaration itself; in this case, you MUST have a constructor to initialize these fields
Note that:

you may define more than one constructor (with different arguments)
you can (should?) define all your constructors protected (making them public is pointless anyway)
your subclass constructor(s) can call one constructor of the abstract class; it may even have to call it (if there is no no-arg constructor in the abstract class)
In any case, don't forget that if you don't define a constructor, then the compiler will automatically generate one for you (this one is public, has no argument, and does nothing).




## multiple inheritance 
 
C++ , Common lisp and few other languages supports multiple inheritance while java doesn’t support it. Java doesn’t allow multiple inheritance to avoid the ambiguity caused by it. One of the example of such problem is the diamond problem that occurs in multiple inheritance.




## Interfaces 

An interface is a contract (or a protocol, or a common understanding) of what the classes can do. When a class implements a certain interface, it promises to provide implementation to all the abstract methods declared in the interface. Interface defines a set of common behaviors. The classes implement the interface agree to these behaviors and provide their own implementation to the behaviors. This allows you to program at the interface, instead of the actual implementation. One of the main usage of interface is provide a communication contract between two objects. If you know a class implements an interface, then you know that class contains concrete implementations of the methods declared in that interface, and you are guaranteed to be able to invoke these methods safely. In other words, two objects can communicate based on the contract defined in the interface, instead of their specific implementation.

Secondly, Java does not support multiple inheritance (whereas C++ does). Multiple inheritance permits you to derive a subclass from more than one direct superclass. This poses a problem if two direct superclasses have conflicting implementations. (Which one to follow in the subclass?). However, multiple inheritance does have its place. Java does this by permitting you to "implements" more than one interfaces (but you can only "extends" from a single superclass). Since interfaces contain only abstract methods without actual implementation, no conflict can arise among the multiple interfaces. (Interface can hold constants but is not recommended. If a subclass implements two interfaces with conflicting constants, the compiler will flag out a compilation error.)


interface defines common protocol, supertype defines common protocols. 

supertype defines contracts. 
class -> public/protected methods 
abstract class -> public/ protected/abstract methods 
interface -> mostly only public abstract methods, interface defines no state and it is no instantiable at all 

interface defines representative behaviour of subclasses, it includes one or more implementations. the public API ~ rarely subclased outside API 


for mixins, it defines additional capability of subclasses 
it is very generic ~ subclasses can come from anywhere 




interface syntax:

#### interfaces is public/abstract by default 
#### variables are public, static, final by default 
#### all memebrs are public by defualt 
#### members cannot be private and protected 

```java
public interface InterfaceName{
    static final fields;
    abstract returnType methodName();
    //100% abstract class 
    default methods();
    static methods();
    nestedTypes();


}


public class SubClass implements Interface(){
    public returnType methodName();
}


```

implementing multiple interfaces 


```java
public class ClassName extends SuperClass implements Interface1,Interface2, Comparable{
public int comapreTo(Object o){

}


public static void main(String []args){
    Comparable obj = new ClassName();
}

}


```


### extending interface 
class can implement interface, but not extend 


```class 
public interface Interface1 extends Interface2, Interface3{

}



```

abstract subclasses no need to implement abstract methods 



##### why variables are static and final in interfaces? 
static: interface are not instantiable 
final: interface represent pure contracts 
it is like arguments set in stone 

static method in an interface is inherited by a subtype 

```java

public interface Interface1{
    int A = 1;
    //public static final int a = 1;

    int method1();
    //public abstract int method();
}

public interface Interface2{
    int B = 1;
    //public static final int a = 1;

    int method2();
    //public abstract int method();
}

public abstract AbstractClass implements Interface1{

    public int method1(){
        return 1;

    }


 
}

public class ConcreteClass extends AbstractClass implements Interface2{

@Override
    public int method2(){
        return 1;

    }

}

```





```java
public interface Interface1 {

    int VARIABLE1 = 100;

    void method1();
    
}
public interface Interface2 {

    int VARIABLE2 = 100;

    void method2();
    
}




//it must be abstract in order to use abstract method, public class AbstractClass 
public abstract class AbstractClass {


    public abstract void method3();
  
    
}


public class Class1 extends AbstractClass implements Interface1, Interface2 {

    @Override
    public void method1(){
        System.out.println(VARIABLE1);
        System.out.println("this is method 1");
    }


    @Override
    public void method2(){
        System.out.println(VARIABLE2);
        System.out.println("this is method 2");
    }


    @Override
    public void method3(){
        System.out.println("this is method 3");

    }


    public static void main(String []args){

        Interface1 c1 = new Class1();
        c1.method1();

        Interface2 c2 = new Class1();
        c2.method2();

        AbstractClass c3 = new Class1();
        c3.method3();

    }
    
}


```


we use objects to refer to interfaces, the benefits are use implementations with better performance, polymorphism benefits with maxium flexible code and clean code 



### Interface versus Abstract classes 
interface: mixins and representative behaviour with no state 

abstract classes: core identity of subclasses or skeletal implementation 

use utmost care when designing interfaces 

What you like : thousands of abstract methods in one Abstract Class and inherit this class OR make as many interfaces for specific abstract methods and use those only you want by inheriting as many interfaces as needed...


```java

abstract class A
{
 //thousands of abstract method();
 abstract methodA();
 abstract methodB();
 abstract methodC();
}

//OR
interface ForOnlymethodA
{
 void methodA();
}
interface FormethodBandmethodC
{
 void methodB();
 void methodC();
}


```

So, use that method only what you just need by inheriting particular interface, if you are inheriting Abstract classes then you are unnecessarily inheriting all methods that you don't need in one class and may be needed in some other classes..



#### marker interfaces 

A marker interface is an interface that has no methods or constants inside it. It provides run-time type information about objects, so the compiler and JVM have additional information about the object.

A marker interface is also called a tagging interface.

Though marker interfaces are still in use, they very likely point to a code smell and should be used carefully. The main reason for this is that they blur the lines about what an interface represents since markers don't define any behavior. Newer development favors annotations to solve some of the same problems.


it has no methods and it merely marks a class as having some properties such as java.util.RandomAccess and java.io.Serializable 

By introducing annotations, Java has provided us with an alternative to achieve the same results as the marker interfaces. Moreover, like marker interfaces, we can apply annotations to any class, and we can use them as indicators to perform certain actions.



#### Serializable interface and Cloneable interface  TODO 





### default method 


before java 8, it is pain to evolve interfaces. abstract classes have multiple inheritance issue. and the default methods came into play with interface evolution with strong compatibility 

default mehods cannot have static & final modifiers 

Default method cannot be defined in an abstract class. it is interface only 

we must use `default datatype methodName()` in instance methods
the conflict resolution strategie is 
1. classes win over interfaces, default methods cannot override `Object's` methods 
2. sub interface win over super interfaces 
3. manual resolutions 


```java
public interface Interface1 {

    int VARIABLE1 = 100;

    default void method1(){
        
        System.out.println("see the default implementation of interface 1");
    };
    
}

public class Class1  implements Interface1 {







    public static void main(String []args){

        Interface1 c1 = new Class1();
        c1.method1();


    }
    
}


```



we can only use superword in parent.super() way  but not in grandparent.super() or only super() 
it can reabstract default methods 
we cannot use final & synchronized modifiers in front of this `default`

the benefits of default methods are, it allows interface evolutions, the default implementationcan be overriden 
it also eliminate utility classes such as list.sort() instead of Collection.sort(List)
it allows interface to stay as functinal interfaces 




### static methods in interfaces 

there was no static methods before java 8 because interfaces are stateless and static methods are stateless too. the real purpose of interface is that it is only a contract without any implementations 


interfaces can be associated with utility methods, to accomodate such utility matters, the convention or pattern is to provide a companion utility 

the evolution of interfaces hold for static mtehods too 

the static methods in interfaces meaning only static keyword and it cannot be inherited. this can only be invoked via interface name 


```java
/*
Illegal combination of modifiers for the interface method add; only one of abstract, default, or static permitted

you cannot do default static int add(int value1, int value2);
*/


public interface Interface1 {

    int VARIABLE1 = 100;

  static int add(int value1, int value2){
        return value1 + value2;
    }
    
}


public class Class1  implements Interface1 {







    public static void main(String []args){

        System.out.println(Interface1.add(1,2));


    }
    
}

```





