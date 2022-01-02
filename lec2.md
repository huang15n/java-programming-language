# Fundamental Programming Structure in Java, Data Types, Variables, and Enumerate, Strings  


this would take us too far away from our goal, let's look more closely at one of the simplest java programs 

```java

public class ClassName{
    public static void main(String [] args){
        System.out.println("Hello World");
    }
}

```

the pieces will recur in all apps, it is worth spending all the time you need to become comfortable with the framework 

## Convention 
1. java is case sensitive, any mistakes in capitalization will not run 
2. public is called an access modifier; control the evel of access other parts of program 
3. program lives inside a class. basically everything must be inside a class. The rules for class names are quite generous being with a letter, and after that can have any combination of leters and digits. the length is essentially unlimited, we can use java reserved words 
the standard naming convetion is that class names are nouns that start with an uppercase letter. if a name consits of multiple words, use an initial uppoercase letter in each of the words. this use of upperccase letters in the middle of a word is called self-referentially CamelCase 
4. you need to make the filename for the source code the same as the name of the public class with the extension .java appended. according to the java language specification, the main method must be decalred public 

5. the braces {} in the source code delieates the parts usually called blocks in our programs. the code for any method msut be started by an opening brace { and ended by a clsoing brace }. brace stles have inspired an inordinate amount of useless controversey. follow a style that lines up matching braces. as whitespace is irrelevant to the java compiler, yo ucan use whatever brace style you like 



## Statements 
 braces mark the beginning and end of the body of the method. you can think of statements as setences of the language, every statement must end with a semicolon. in particular, carraige returns do not mark the end of a statement, so statements can span multiple lines if needed 

Notice the periods used to invoked a method. java uses the general syntax: object.method(parameter); as its equivalent of a function call. methods can use zero, one or more parameters  





## comments 
comments do not show up in the executable program 

the most common form is //

```java

// one line 

```


longer comments are need, you can use 

```java

/* multiline commends 

*/

```
the /* */ comments do not nest in java. you might not be able to deactivate code simply by surrounding it with /* */


to generate documentation automatically, use 
```java 
/** javadoc 
@Version 
@Author

*/

```




## Data types 

Java is a storngly typed language. this means that every variable must have a declared type 
there are primitive types in java. four of them are integers types, two are floating point numbers types. one is the character type char, used for code units in the Unicode encoding scheme and one is a boolean type for truth values.  since java mus trun with the same results on all machines, the ranges for the various types are fixed 


### Integer types 
the integer types are for numbers wihtou fractional parts. the int type is the most practical, resort to long if represent the numbre o finhbitatnts. byte and short types are mainly intended for specialzed apps 


|Type  | Storage Requirement |suffix |
| ------------- | ------------- | ------------- |
| int  | 4 bytes  | nothing|
| short  | 2 bytes | nothing|
| long  | 8 bytes | l/ L|
| byte  | 1 bytes | nothing|

### Floating Point types 
the floating point types denotes numbers with fractional parts. the double refers to the fact that these numbers have twice the precision of the float type, float have a suffix F or f. floating point numbres without a F are always considered to be of type double. note round off errors are caused by the fact that floating point numbres arre represented in the binary number systems 


|Type  | Storage Requirement |suffix |
| ------------- | ------------- | ------------- |
|double | 8 bytes  | nothing|
| float  | 4 bytes | f/F |

in particular three special floating point values to denote overflows anderrors Positive.infinity, Negative.infinity, Nan not a number 


###  The char type 
the char type was orginally intended to describe individual characters. however, this is no longer the case. literal value of type char are enclosed in single quote: 'A';
the unicode encoding scheme was invented to overcome the limitations of tranditonal character encoding schemes with large character sets have variable lengths and insufficient to describe all unicode characters. 
the characters in a basic multiligual plane are represented as 18 bits values, called code units. the supplementary characters are encoded as consecutive paris of code units 

### Escape Sequence 
| Escape Sequence  | Name | 
| ------------- | ------------- |  
|\b | backspace  |  
| \t  | tab | 
| \n  | line feed | 
| \"  | double quotes | 
| \'  | single quotes | 
| \\  | backslash | 


###  boolean types 
the boolean types are two values, false and true. it is used for evaluating logical conditoins. you cannot convert between integers and boolean values 




## Variable 

every variable has a type, you can declare a variable by placing the type first, followed by the name of the variable. 
a variable name must begin wit ha letter and must be a sequence of letters or digits. a ltter is defined as alphabets, _. $(not recommended). or any unicode character that denotes a letter in a lnaguage 

```java
data_type variableName;

```

you can not use a java reserved words a a variable 
variable names are case sensitive 

you can declare mutiple variables on a single line. However, we do not recommend this style. if you declare each variable separately, your programs are easier to read 

```java
data_type variableName1,variableName2, variableName3;

```


### Initializing variables 
you must explictly initialize a variable afeter you declare a variable by means of an assignment statement -- you can never use the value of an unintialized variable 

```java
data_type variableName;
variableName = value;

```

you can both declare and initialize a variable on the same line 

```java
data_type variableName = value;

```
finally, you can put decalraitons anywhere in your code. but in java, it is considered good style to decalre variables as closely as possible to the poin where they are first used 


### Conversion between numeric types and Casts 

| Sort  | Result | 
| ------------- | ------------- |  
| double(either) + any type | double |  
| float (either) + any type|  float| 
| long  (either) + any type | long | 
 | int  + int | int | 

conversion in which loss of information is possible done by means of casts. the syntax for casting is to give the target type in parentheses, follow by the variable name 


```java
data_type variableName1;
(newType) variableName2 = (newType) variableName1; 


```
caution, if you try to cast a number of a type to another that is out of range for the target type, the result will be a truncated number that have a different value 




## Constant 
you use the keyword *final* to denote a constant. the keyword *final* indicates you can asisgn to the variable once, and then its value is set once and for all. it is customary to name constants in all uppercases 


```java
final data_type CONSTANT_NAME = VALUE;

```



*it is probably more common in java to create a onstant so it is asvaible to muliple methods inside a single class. thes eare usually caleld class constant, set up a class cosntant with the kwyrod static final*



```java
public class Constant{
public final data_type CONSTANT_NAME = VALUE;

}

```

note he defintion of the class constant appears outside the main method, thus the constant can also be used in other methods of hte same class. furthermore, if the constant is declared, , methods of other classes can also use it 



## Operators, Assignment 

the useful arithmetic operators +,-,*,/ are used for addition, subtraction, mulitplciation and division. 
the / opreator dnotes integer division if both arguments are integers, and floating point division otherwise 
note that integer division by 0 raises an exception, whereas floating point division by 0 yields an infinite or NaN result 
there is no operator for rasing a quantiy to a power, either way it is a hassle. 

### Mathmatical functions and const 

the math class contain an assortement of mathematical functions that you may occasionally need, depending on th ekind of programming 



```java 

double value1= Math.pow(base, exponentials); // noth double returns a double 

// trigonometric functions 
Math.sin
Math.cos
Math.tan
Math.atan
Math.atan2

// exponential functions with it s inverse , the natural logarithm, decimal logairthm 
Math.exp
Math.log
Math.log10

// two constants denotes the cloest possible approximation to the mathematical constants PI and E 
Math.PI
Math.E

```

### Combinng assignment with operators 
there is a conveninent shortcut for using binary operators in an assignment 


```java
variable += value; // equivalent to variable = variable + valuel
variable -= value;
variable *= value;
variable /= value;
```

### Increment and Decrement Operators 

programmers, know that one of the most operations with a numeric variable is to add or subtract 1, java, following in the footsteps of C has both increment and decrement operator. we recomend against using ++ inside expressions because this often leads to confusing code and annoying bugs 


```java
variable ++; // equivalent to variable = variable + 1;
variable --;
++variable;
--variable;
```


### Relational and boolean operators 

java has the full complement of relational operators. to test for equality, ues a double qual sign , == 
finally, you have less than <, greather than>, less than or equal <=, greater than or equal >=


| operator  | defintion | 
| ------------- | ------------- |  
| >| greater than |  
 | < | less than | 
  | <= | less than or equal | 
  | >= | greater than or equal| 
  | == |  equal| 
| != | not equal| 

   


java ues && for the logical operator "and" || for th elogical opreator "or"
| operator  | defintion | 
| ------------- | ------------- |  
| expression && expression | and |  
 | expression||expression | or | 
 



the value of expression || expression is automatically true if the first expression is true, without evaluating the second expression 

finally, java supports tenary ?: operator 

```java

condition? expression1 : expression2;

```


### Parentheses, precedence and opertor hierachy 
operators on the same level are processed from left to right, except those that are right associatve 
| operator  |  
| ------------- | 
| [] . () (method call)  |  
 | ! ~ ++ -- + (unary) - (unary) () (cast) new  |  
| * / % | 
| + - | 
| < <= > >= instanceof | 


## Enumerated types 
a variable should only hold a restricted set of values. you can define your own enumerate type whenever such a situation arises. An emuerated type ha sa finite number of name values But it works closely with Classesin greater detail 

```java 
enum YourType{VALUE,VALUE2,VALUE3};

```


## String 

conceptually, strings are sequence of unicode characters. 
Java does not have a builtin string type. the standard library contains a predefined classs called, naturally enough, String. each quoted string is an instance of the String class 

```java 

String emptyString = "";
String string = "this is a string";

```
## Immutable 
the String gives no methods that let you change a character in an existing string, you cannot directly change the positions. The documentation refer to objects of the String class as immutable 

```java

//aka you cannot do 
String string1 = "string1";
string1[0] = 'a';
// you will have to build a new string 

```
it would seem simpler to change the code units than to build up a whole new string from scratch. but immutable strings ahve one great advantage: the compilre can arrange that string are shared! sitting in a commmon pool, copy a string variable, both orginal and the copy share the same characters. the efficiency of sharing outweights the inefficiency of string editing by extracting substrings and concatenating 



### Substring 
you can extract a substring from a larger string, the seoncd parameter o fsubstring is the first position that you do not want to copy. as substring counts it, this means from position start inclusive to positoin end exclusive. 

```java 
String string1 = "string1";
String string2 = string1.substring(start, end);
String string2 = string1.substring(0, 1);

```


### Concatenation 

java allows yo uto use + to join/concatenate two strings which is pefectly acceptable  
```java 
String string1 = "string1";
String string2 = "string2";
String string3 = string1 + string2;
```



### Testing for equality 

to test whether two strings are equal, use the equals method, the expressoin 

```java

string1.equals(string2);
string1 == string2 // don't work 
```
*Note: do not use the == operator to test whether two strings are equal! it only determines whether or not the strings are stored in the same memory location. If strings are in the same location, they must be equal. but it is entirely possible to store mutiple copies of identical strings in different places *


the expression is perfectly legal to test whether two strings are identical except for the lower and upper case 

```java

string1.equalsIgnore(string2);
```

### Empty and Null string 
the empty string "" is a string of length 0, you can test whether a string is empty py calling 

```java 

if(string.length() == 0){}
//or 
if(string.equals("")){}

```
an empty string is a java object which holds the string length namely 0 and an empty ontents. however, a String variable can also hold a special value, called null, that indicates that no object is currently associated with the variable 


to test whether a string is null use: 
```java 

if(string == null){}
// to test neither null nor empty 
if(string == null && string.length() != 0){}
 

```

## String API
String class contains various methods, a surprisingly large number of them are suffciently useful so that we can imaggine using them frequently . The API note summarizes the ones we found most useful 

```java 
string.equals(string);
string.compareTo(string);
string.charAt(index);
string.length();
string.substring(inclusive_start,exclusive_end);
string.toLowerCase();
string.toUpperCase();
string.indexOf(string/character);
string.lastIndexOf(string/character);

string.trim();  // like python stripe() by elimaiting all leading and trailing whitespace in the original string and returns a new string

string join(delimiter, character_elements); // return a new string joining all elements with given delimier 

```

### Building Strings 
occassionally, you need to build up strings from shorter string, such as keystrokes or word from a file. it would be inefficient to use string concatenation for this pourpose 

every time you concatenate a string, a new Sring object is constructed. this is time consuming and waste memory. 

Using StringBuilder class avoid this 


you need to build a string from small pieces, first, construct an emoty string builder, when you are done building the string, call the toString method and you will get a String object with the character sequence contained in the builder 

```java
StringBuilder builder = new StringBuilder();
builder.append(character/string);
String result = builder.toString();


// other methods 
builder.insert(offset, string/character);
builder.delete(start,end);
```


