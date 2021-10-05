

# Introduction to Java 

Java generated an incredible amount of excitement in mainstream media. Java has the distinction of being venture capital fund was set up solely for products. It is out in the field with existing code sets in. WE got a lot of flack very high up. It is a languge with a pleasant syntax and comprehensible semantics and Java fits the bill, so do doezens of others to catch up. However, the initial excitement soon turned into frustration. Java was dogged by serious security issues. This was a great achievement at the time and the library has since grown to huge proportions. Java library became increasily restrictive 


Java is general purpose, object-oriented, platform independent, concurrent. Java runs automatic memory managament - garbage collection. THe initial conclusion of java includes network of heterogeneous consumer devices and built on reliable, distributed, realtime embedded systems. THe goal was to consume less memory, delivery of multithreaded softare components that are usable with platform independence and security.
. It is based on various published sources led by people and generate very tight code. presumbly linked the note to market their techonoligies, the group then bid on a project with emerging services on demand. The datacenters increasily relied on commodity hardware instead of specialized servers. On the one hand, it is frustrating to have quality assurance, who are often overworked and not always experts in the fine points of java, make questionable decisions about bug reports 




This closes with a commented list of misconceptions about java.
Java and HTML have nothing in common except that there are html extensions for placing java onto webpage 
Java API contains excellent support for XML processing. 
You always have to distinguish between how easy it is to do serious work 
This possible in theory, but in practice, there are domains where other languages are entrentched. Some people prefer it to C or C# 
The sucess of a programming language is determined far more by the utility of the support system surrounding it than by the elegance of its syntax. The toolset integrate with the rest of computing infrastructure 

Java is not proprietary, and it should not be avoided. Oracle has committed to keeping it open source. THere is only on fly in the ointment -- patents 


Java virtual machine uses a just-in-time compiler, Java are not a major security risk. The technical failures that they found have been quickly corrected, thre wre no more serious explloits 

JavaScript is more tightly integrated with browseres than java. 

1. Java's object orientation was well established and lies in multiple simpler concepts of interface which has a richer capacity for runtime introspection 


2. Java's distributed routines takes this for granted 

3. Java is intended for reliable in a vareity of ways, it puts a lot of emphasis on checking possible problems 

4. to bring it on. untrsuted code was executed in a sandbox, towards thta end, java was designed to overrun the runtime stacks, attacks impossible, corrupting memory outside its process space, reading or writing files without permission. hackers spotting subtle flaws in the implementation of the security architecture after high profile attaks, increasingly cautious. 

5. the compiler generates an architecture neutral object file format, interpreting virtual machine instructions hae the option of translating the most frequently executed bytecode sequence into the machine code -- a process called just-in-time compilation 


6. java is always a 32 bit integer. the libraries are part of the system define portable interfaces.  java made the heoric effort, delivery a toolkit that provided common user interface elements. 

7. java interpreter can execute bytecode directly on any machine to which the interpreter has been ported. since linking is a more incremental lightweight process, the development process can be much more rapid 

8. java has high performance of interpreted bytecode is usually more than adquate. the bytecode can be translated on the fly at runtime into the machine code. a more sophisticated optimization is the elimination or inlining of function calls 

9. java was well ahead of its time support concurrent programming. concurrent programming was needed to make sure the user interface did not freeze and making it manageable. java carries out sophisticated calculations. 

10. java is dynamic to adapt to an evoling environment. libraries can freely add new methods and instance variable without any effect on their clients. ad java first appeared was responsible for the astonishing popularity of it.




## Java Versions 
Java SE, Java EE, Java ME

Java SE JDK includes dev tools and JRE
JRE consists of JVM and Java API for java runtime environment 









# Java Programming Environment 

you can run the up to date Java Development Kit -- JDK tools by typing ommands in a terminal window or prefer the comfort of an integrated development development environment. Java developers felt that a fractional version increment did not properly communicate to the momentous advances of JDK, the numbering was simplified 

1. JDK(Java Development Kit): JDK is intended for software developers and includes development tools such as the Java compiler, Javadoc, Jar, and a debugger.
2. JRE(Java Runtime Environment): JRE contains the parts of the Java libraries required to run Java programs and is intended for end-users. JRE can be view as a subset of JDK.
3. JVM: JVM (Java Virtual Machine) is an abstract machine. It is a specification that provides a runtime environment in which java bytecode can be executed. JVMs are available for many hardware and software platforms.


Here are installation instruction: 

For Windows:https://www.wikihow.com/Set-Up-a-Java-Programming-Environment

for Linux/Unix
1. download JDK: www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
or 

```shell
sudo apt-get install openjdk-8-jdk

```

2 set up environment variables. For the “JAVA_HOME” (Environment Variable) type command as shown below, in “Terminal” using your installation path…(Note: the default path is as shown, but if you have to install OpenJDK at another location then set that path.) 
```shell
export JAVA_HOME = /usr/lib/jvm/java-8-openjdk
export PATH = $PATH:/usr/lib/jvm/java-8-openjdk/bin
```


There is also Java Runtime Environment JRE that contains the virtual machine but not the compiler that was coned at 


```java
public class Welcome{
    public static void main(String [] args){

        System.out.println("Hello World");
    }
}


```

open a terminal window, (for windows, check this out: https://www.wikihow.com/Change-Directories-in-Command-Prompt) go to the directory and enter the following commands 

```shell
javac Welcome.java
java Welcome.java

```

the javac program is the java compiler, it compiles the .java file into the file .class. the java program launches the java virtual machine. it executes the bytecodes that the compiler placed in the class file 

in the age of visual development environment, you are unfamiliar with running programs in a terinal window. 
pay attention to the following thing: upper and lowercase ltters. the compiler requires a file name , when you run the program, you specify a class name without .java or .class extension. check your installation in particular executable path setting whether that file is present in the directory 







java comes with: 
compilation, interpretation, general platform indepencne on top of JVM. The java program is a set of instruction, the instruction is initially 0s & 1s machine language/ native code, which is obviously cumbersome and frustrating to write 
the java compiler compiles source code onto target language -- bytecode which verifies syntax & semantics of source code with code optimization and generate machine code 



then the assembly adds higher level of notations. the assembly language uses assembler to translate these instructions to machine language 


a typical platform dependency compilation process in C would be like: 
C -> compilation/ Linking -> machine code -> executable 

that is: 
source code -> compiler -> machne code -> cpu result 


java interpretation involves: 
source code -> interpreter -> result 
the interpreter runs on virtual machine uses fetch-and-execute cycle: fetch next program statement and execute precompiled machine code in its library 
the pros are: platform indepedent, no compilation step, easier to update 
the cons are: slow, costly memory access, source code is reinterpreted every time. Therefore, the compilation has fast execution but no platform independence as opposed to interpretation which has slow execution but high platform independence 


if you have remaned the file correctly and not make any typos in the source then when you compile this source code, you ned up with a file containing the bytecode for this class. the java compiler automatically names the bytecode file .class and stores it in the same directory as the source file 


java compilation process can be broken down into: 
source code -> java compiler -> java bytecode -> java interpreter(JVM) -> result 
which goes from an istance of 
.java -> compilation -> .class -> jvm 
the bytecode interpretation is much faster, java's bytecode is compact, compiled, and optimized which offers just in time compilation. This bytecode compactness has quick transfer across networks 


### JVM java virtual machine 
the core responsibilities and cornerstone of java platform are: loading & interpreting java bytecode, security, automatic memory management because bytecode is compact, compiled and optimized which are identified frequently with hotspots. the compiler converts hot spots to machine code, cache machine code for faster execution 









































