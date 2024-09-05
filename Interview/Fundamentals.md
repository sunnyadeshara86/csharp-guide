# Fundamentals of C#

## Essential C# concepts and principles


### What does the C# language represent, and for which platforms and applications is it intended?

C# is a programming language created by Microsoft and part of the .NET platform. With C#, a variety of applications can be developed, such as desktop applications, web applications, mobile applications, gaming applications (via Unity), cloud computing solutions, and more. C# is supported across various platforms thanks to .NET Core and Xamarin.

### What’s the fundamental difference between .dll and .exe files in the context of C# projects?

In the context of C# and .NET, an .exe (executable) file is an executable that contains an entry point for the program. In other words, when you run an .exe file, the program starts its execution. On the other hand, a .dll (dynamic-link library) file is a code library that doesn’t have a direct entry point but can be called by another program or application. It’s a means of code reuse among different projects.

### How does the entry point of a program written in C# look?

The entry point in a C# program is typically represented by the Main() method, which is located in the Program class. This method must be static and serves as the starting point for the program’s execution. Usually, its structure looks like this:

```
public class Program
{
    public static void Main(string[] args)
    {
       // program code
    }
}
```

The args argument contains an array of strings that is passed to the program upon its launch.

### Why is the main method static in C#?

In C#, the Main method is static because it serves as the entry point for the application, and it needs to be called by the runtime without creating an instance of the class in which it resides. Here’s a more detailed explanation:

### How is memory management conducted in C#?

In C#, memory management is handled automatically thanks to the garbage collector mechanism. It automatically identifies objects that are no longer used by the program and frees the memory they occupy. While the garbage collector simplifies memory management, developers need to carefully manage unmanaged resources that are not controlled by the .NET garbage collector, such as database connections or file streams. If developers do not release these resources, they will persist for the lifetime of the application, potentially causing memory leaks and system strain.

### What are the principles of OOP in C#?

OOP is based on four main principles: encapsulation, inheritance, polymorphism, and abstraction. In C#, this means the following:

> * Encapsulation allows data and methods to be bundled into a unit (class) and restricts access to certain components.
> * Inheritance permits one class (the child or derived class) to inherit the attributes and methods of another class (the parent or base class). This promotes the reuse of code and establishes a hierarchical relationship between classes.
> * Polymorphism is the capability of a single function or method to work in various ways based on its inputs or on which object it is called upon. In C#, polymorphism can be achieved through method overriding, using the override keyword, and method hiding, utilizing the new keyword to hide a method in the base class.
> * Abstraction allows developers to hide complex implementations and show only the essential features of an object. This means that the user interacts with only what’s necessary and the internal workings are kept hidden. In C#, abstract classes and interfaces are tools that can help achieve abstraction.

These principles help in designing robust and scalable applications, allowing for easy maintenance and further development. C# offers a rich set of features to implement and benefit from these principles effectively.

### What will be the output of below code?

```
class BaseClass
{
    public void Method()
    {
        Console.WriteLine("BaseClass Method");
    }
}

class DerivedClass : BaseClass
{
    public new void Method()
    {
        Console.WriteLine("DerivedClass Method");
    }
}
```

```
BaseClass obj = new DerivedClass();
obj.Method();
```

When you declare a variable of the base class type and initialize it with an instance of the derived class, the method call will use the base class implementation:

### What will be the output of below code?

```
class BaseClass
{
    public virtual void Method()
    {
        Console.WriteLine("BaseClass Method");
    }
}

class DerivedClass : BaseClass
{
    public override void Method()
    {
        Console.WriteLine("DerivedClass Method");
    }
}

```

```
BaseClass obj = new DerivedClass();
obj.Method();
```

When you declare a variable of the base class type and initialize it with an instance of the derived class, the method call will use the overridden implementation in the derived class:

### How is error handling done in C#?

In C#, the primary error handling mechanism is based on the use of try, catch, finally, and throw constructs. When code in a try block causes an error, execution jumps to the corresponding catch block, where the exception is handled. The finally block, if present, is typically executed after try/catch, regardless of whether there was an exception or not. However, there are critical exceptions, such as StackOverflowException or OutOfMemoryException, which can result in a program crash and thus the finally block won’t be executed.

### What does the dependency injection principle mean and how is it implemented in C#?

Dependency injection (DI) is a software design approach that reduces tight coupling between system components. At the core of DI is the passing of dependencies (services, objects) to components rather than creating them inside those components. In C# and .NET, DI is often implemented using dependency containers, such as Microsoft.Extensions.DependencyInjection, Ninject, Autofac, StructureMap, and others.

### What are boxing and unboxing in C#, and why can they be a problem?

Boxing is the process of converting a value type (e.g., int) to an object type or any interface type implemented by that value type. Unboxing is the reverse process, where a value from an object type is converted back to the corresponding value type. The primary concern with boxing and unboxing in C# is their potential to degrade application performance. Boxing necessitates heap memory allocation and value type copying, thus slowing operations, especially with large datasets or in high-frequency scenarios. Unboxing, if incorrectly managed, can lead to runtime errors due to improper type casting, disrupting program execution. Additionally, these operations can increase the workload on the garbage collector, causing more frequent collection cycles and negatively impacting the application’s responsiveness.

### What does Entity Framework represent and how is it applied?

Entity Framework (EF) is an object-relational mapping (ORM) framework developed by Microsoft for the .NET ecosystem. It enables developers to work with databases using object models instead of writing direct SQL code. This tool simplifies the process of creating and managing data models, automating database schema migrations, and writing queries that make database interaction more intuitive.

### What’s the difference between threads and processes in C#?

In an operating system, a process is a distinct execution entity that has its own memory space. A thread is the smallest unit of execution within a process. Each process can have one or multiple threads. In C#, threads can be managed using the Thread class from the System.Threading namespace. The main difference lies in the fact that threads within a single process can share the same memory area, whereas each process has its own isolated memory context.

### What are the main development environments used for C#?


> * Visual Studio:
>   * Features: Comprehensive IDE with advanced tools for large-scale projects and multi-language support
>   * Use case: Best suited for enterprise-level applications, offering a range of tools for collaborative and complex projects
> * Visual Studio Code:
>   * Features: Lightweight, open source code editor with a rich ecosystem of extensions, including C# support
>   * Use case: Ideal for individual developers or small teams, providing a flexible and extensible environment for various languages and frameworks
> * JetBrains Rider:
>   * Features: Cross-platform .NET IDE with powerful tools for .NET development and a rich set of plugins
>   * Use case: Excellent for cross-platform development, offering consistent experiences and high-quality code analysis and refactoring tools

### Can you describe different software testing methods and their primary differences?

There are several types of testing, including the following:

> * Unit testing: Focuses on individual pieces of code, particularly functions or methods
> * Integration testing: Checks the interaction between different parts of the software
> * System testing: Tests the entire system

The main difference lies in the level of access and the scope of testing.

### How do you determine the best time to conduct unit testing compared to integration or system testing?

> * Unit testing is best conducted during development when a specific component or function is being created or modified.
> * Integration testing should be applied after several components have been combined to verify their correct interaction.
> * System testing should be applied when the entire product or a significant portion of it is ready for release.

### What is NuGet, and how can it be used to add libraries to your project?

NuGet is a package manager for the .NET platform that allows developers to easily add, update, and remove external libraries and dependencies in their projects. To add an external library to a project through NuGet, you need to open the NuGet console in the development environment (e.g., in Visual Studio) or use its graphical interface, find the desired package, and install it.

## Working with data types, variables, and operators in C#

### What are the basic primitive data types in C#? What is the main difference between value type and reference type?

In C#, there are primitive data types, such as int, float, double, char, bool, byte, and others. The main difference between is the value type and reference type lies in how they are stored and how their memory management is done. Value types are stored on the stack and directly contain their value, while reference types are stored in the heap and contain a reference to the object in memory.

### What is the primary distinction between string and StringBuilder in the context of strings?

The string type in C# is immutable, meaning every time the string is modified, a new instance is created. On the other hand, StringBuilder is designed for efficiently modifying strings without the need to create numerous new instances.

### How do you initialize and interact with one-dimensional and multidimensional arrays? What differentiates "string[][]" from "string[,]"?

A one-dimensional array in C# is initialized like this: ```int[] arr = new int[5];```. As for multidimensional arrays, ```string[,]``` is a two-dimensional array, while ```string[][]``` is an array of arrays, also known as a jagged array.

### What are bitwise operations and which operators in C# support these operations?

Bitwise operations allow for manipulations at the level of individual bits of a numerical value. The primary bitwise operators in C# are & (AND), | (OR), ^ (XOR), and ~ (NOT).

### What is the purpose of "nullable" types in C# and how do you work with them correctly?

Nullable types in C# allow representing an absent or uninitialized value for value types. They are typically used when there is a need to distinguish a zero value from the absence of a value. To check for the presence of a value, you can use the HasValue property, and to retrieve the value itself, you use Value.

### What is known about operator overloading in C# and why can it be useful?

Operator overloading allows defining the actions of operators for user-defined data types, such as classes. This can be useful, for instance, for easy manipulation of complex numbers, vectors, or other mathematical structures.

### How can one overload an operator in C# and could you provide an example?

In C#, operator overloading allows you to redefine the way built-in operators work for user-defined types such as classes and structs. To overload an operator, you define a static method in your class or struct with the operator keyword followed by the operator symbol you want to overload. The method must return a result and take at least one parameter of the type you’re overloading the operator for.

Here’s a simple example of overloading the + operator for a custom Vector class:

```
public class Vector
{
    public int X { get; set; }
    public int Y { get; set; }
    public Vector(int x, int y)
    {
        X = x;
        Y = y;
    }
    // Overload + operator
    public static Vector operator +(Vector v1, Vector v2)
    {
        return new Vector(v1.X + v2.X, v1.Y + v2.Y);
    }
}
// Usage:
Vector vector1 = new Vector(1, 2);
Vector vector2 = new Vector(2, 3);
Vector result = vector1 + vector2;  // This will call the overloaded + operator
```

### How do comparison and relational operators work in C#?

Comparison (==, !=) and relational (<, >, <=, >=) operators are used to compare two values. It’s important to remember that when comparing reference types, the == operator checks for reference equality, not content.

### What is the purpose of logical operators in C#, how do they function, and why is it important to pay attention to operator precedence?

Logical operators, such as && (logical “and”), || (logical “or”), and ! (logical negation), are used for combined logical conditions. It’s important to know operator precedence as it affects the order of operations. For example, the expression A && B || C will be interpreted as (A && B) || C, not A && (B || C), which can lead to different results.

Logical Operators and Their Precedence
* Logical NOT (!)
* Logical AND (&&)
* Logical OR (||)

### When and why should you use “const” variables in C#? What’s the difference between them and “readonly”?

const variables should be used when you need to define a variable that doesn’t change throughout the program’s life cycle. They must have a value assigned at compile time. On the other hand, readonly can be initialized in a class constructor and ensure that its value cannot be changed afterward.

### Which method of object comparison in C# is better to use, “==” or “Equals()”, and why?

For value types, == and Equals() usually work the same way, but for reference types, == checks for reference equality, not content. Equals() can be overridden for custom classes to ensure content-based comparison. As a rule, if you want to compare the content of objects, it’s better to use Equals().

### What’s the primary distinction between “is” and “as” when converting types in C#?

```is``` checks whether an object is an instance of a certain type and returns a Boolean value. ```as``` is used for safe type casting and will return null if the conversion is not possible, rather than throwing an exception.

### What do explicit and implicit type conversions mean in C#?

Implicit-type conversion happens automatically when a data type that can hold less information is converted to one that can hold more (for example, from int to double). Explicit-type conversion (casting) is required when there’s a risk of data loss during the conversion.

### What is the purpose of the "??" operator in C# and in which scenarios should it be used?

The ?? operator is a null-coalescing operator that returns the left operand if it’s not null; otherwise, it returns the right one. It’s useful for setting default values for potentially null values.

### What are tuples, how are they used in C#, and what are their advantages compared to classes?

Tuples in C# are ordered collections of various types. They are useful for representing datasets without creating specific types. Compared to classes, tuples are typically lighter and more convenient for small, temporary datasets.

## Writing control structures and loops in C#

### What are the main loops available in C# and how do you choose the best loop for a specific situation?

In C#, several types of loops are available: for, foreach, while, and do-while. Let’s look at each of them:

> for: This is the most commonly used loop when you know the number of iterations beforehand.
> foreach: This type of loop is perfect for iterating through collections or arrays when you need to work with each element sequentially.
> while: This loop executes as long as the specified condition is true. It’s useful when you don’t know the number of iterations beforehand.
> do-while: This loop is similar to while, but the condition is checked after executing the loop body, ensuring the loop body is executed at least once.

Choosing the best loop depends on the specific situation. If you need to iterate over all elements of a collection, foreach would be the most convenient. If you know the number of iterations, for would be the most efficient. In cases where you don’t know the number of iterations in advance, you can use while or do-while, depending on whether you want the loop body to execute at least once or not.

### How do you use the “if”, “else if”, and “else” operators in C#? In which situations would you recommend using each of them?

The if, else if, and else operators are used for conditional code execution. if checks a condition and, if it’s true, executes the code block following it. else if allows you to check additional conditions if the previous conditions were false. else executes a code block when none of the previous conditions were met. Use if to check a single primary condition, else if to check additional conditions, and else as a fallback code block to execute.

### What’s the difference between “for” and “foreach” loops? In which cases is it better to use each?

The for loop is used when you know in advance how many times you need to execute the loop. The foreach loop is designed for iterating over collections, such as lists or arrays. Use for when you have a specific number of iterations, and foreach when you need to iterate over all elements in a collection.

### What is the “switch” operator and how is it different from a sequence of “if-else” operators?

The switch operator allows you to check a variable against multiple values. It is more compact and often more convenient for checking the values of a single variable. An if-else sequence, on the other hand, offers more flexibility as it can check different conditions, not being limited to just one variable.

### What do the “continue” and “break” operators do in loops, and when can they be useful?

continue skips the current loop iteration and proceeds to the next one. break exits the loop prematurely. continue is useful when some loop iterations need to be skipped, and break when you need to terminate the loop execution under a certain condition.

### How do you combine multiple conditions in a single “if” statement using logical operators?

You can use logical operators && (logical “and”) and || (logical “or”) to combine multiple conditions, for example, if (x > 5 && y < 10) {...}.

### What is the peculiarity of the “do-while” loop compared to the regular “while” loop?

The primary difference is that in the do-while loop, the condition is checked after the loop body is executed, ensuring that the loop body runs at least once, regardless of the condition.

### What does a nested loop look like and why can it be useful?

A nested loop is a loop placed inside another loop. It is often used for processing a two-dimensional array or matrix. See the following for an example:

```
for (int i = 0; i < 3; i++)
{
    for (int j = 0; j < 3; j++)
    {
        Console.WriteLine($"i = {i}, j = {j}");
    }
}
```

### How can you prevent a potentially infinite loop execution?

To prevent an infinite loop, it’s crucial to ensure that a loop termination condition will be met. This can be done by checking conditions before entering the loop, using execution time limiters, or through internal counters and monitoring tools.

### What is recursion in C# and how do you prevent stack overflow when using recursive methods?

Recursion is a technique where a method calls itself. To prevent stack overflow, it’s important to have a clear base case that will halt the recursive calls and to limit the recursion depth.

### How can you optimize a loop for processing a large amount of data in C#?

To optimize a loop, you can use parallelism, employ efficient data structures, reduce the number of operations within the loop, and utilize caching where possible.

### What is “yield return” in C# and when can it be useful?

yield return allows you to create iterators without the need to generate an auxiliary collection. It’s useful when you want to lazily generate values as you iterate through a collection.

### How do you create an infinite loop using “for”?

An infinite loop can be created using for in the following manner:

```
for(;;)
{
// loop code
}
```

Here, the condition, initialization, and increment are absent, so the loop will run indefinitely.

## Exploring the basics of OOP using C#

### How does C# integrate the principles of OOP?

C# supports all the core principles of OOP: encapsulation, inheritance, polymorphism, and abstraction. For instance, classes and interfaces in C# allow for the implementation of inheritance and polymorphism, while access modifiers facilitate encapsulation.

### How does encapsulation work in C#?

In C#, encapsulation is ensured through access modifiers such as ```private, protected, internal, and public```. These modifiers determine the visibility of class members, allowing for the hiding of implementation details and exposing only the necessary API.

### How is polymorphism implemented in C#?

Polymorphism in C# is realized through the ability to override methods in subclasses using the ```virtual and override``` keywords, as well as through interfaces that allow different classes to have a consistent set of methods.

### What does inheritance entail in C#?

Inheritance in C# allows for the creation of a new class based on an existing one, inheriting its attributes and behavior. This is achieved using the : keyword, followed by the name of the base class.

### What is the difference between a class and its instance in C#?

A class serves as a schematic or prototype that delineates the characteristics and functions of objects. An object (or instance of a class) is a specific representation of that class with a unique set of attribute values.

### Why are access modifiers such as “public”, “private”, “protected”, and “internal” used in C#?

These modifiers determine the level of access to class members. public makes a member accessible to any code; private restricts access to only the methods of the given class; protected allows access to the given class and its descendants, and internal makes a member accessible to any code within the same assembly.

### Can a class in C# inherit from multiple other classes simultaneously?

No, C# does not support multiple inheritance for classes. However, a class can implement multiple interfaces.

### How do method overloading and method overriding differ in C#?

Method overloading allows having multiple versions of a single method in one class with different parameters. Method overriding allows a subclass to replace the implementation of a method provided by its base class.

### What are the main differences between interfaces and base classes in C#?

Interfaces define a contract (a set of methods without implementation) that must be adhered to by the class that implements it. Base classes contain an implementation that can be inherited and extended. A class can inherit only one base class but can implement multiple interfaces.

### Why is composition sometimes considered a better choice than inheritance?

Composition offers greater flexibility, allowing dynamic changes to an object’s behavior on the fly, and reduces the risk of issues associated with tight coupling between classes. It also promotes the principle of composition over inheritance, suggesting that using composition for the reusability of code is a more desirable approach.

### What are properties in C# and how do they differ from fields?

Properties are a special kind of class member in C# that represents access to data with the ability to define logic when reading or writing that data. They allow you to control access to internal fields and can contain additional logic, for instance, for validation. Fields, on the other hand, are variables defined in the class and are used to store data.

### What’s the main difference between abstract classes and interfaces in C#?

Abstract classes can contain methods both with and without implementation. They cannot be instantiated directly. Interfaces only contain method declarations without implementation. A class can implement multiple interfaces but can inherit only one abstract class.

### Why is encapsulating fields important for the SOLID principles?

Encapsulation helps keep the internal state of an object protected and hidden from the external world, which supports adherence to the Open/Closed Principle of SOLID. It also helps prevent unwanted state changes that could violate the Single Responsibility Principle.

### What is the role of delegates in OOP in the context of C#?

Delegates in C# are objects that can point to methods. They allow for the realization of the function pointers concept in a type-safe manner. Delegates are often used to implement events and callbacks.

### How are constructors used for object initialization and how do they differ from static constructors?

Constructors help initialize an object at the time of its creation, setting the necessary state or performing any other required setup. Static constructors are used to initialize static members of a class or to perform actions that should occur only once for the class, not for each individual object.

### What do aggregation and association mean in OOP, and how are they implemented in C#?

Aggregation and association represent two distinct relationships between classes within the OOP paradigm. Association denotes a broader connection between two classes, indicating that one class incorporates the other.

Let me show some examples of how they are implemented:

> Association is a bi-directional relationship between two classes. Here, we demonstrate a one-to-many association between a Library class and a Book class:

```
public class Book
{
    public string Title { get; set; }
}

public class Library
{
    public List<Book> Books { get; set; }
    public Library()
    {
        Books = new List<Book>();
    }
}
```

> Aggregation represents a relationship where one class is a part of another class. Here, we illustrate an aggregation between a Car class and an Engine class:

```
public class Engine
{
    public string Model { get; set; }
}

public class Car
{
    public Engine CarEngine { get; set; }
    public Car(Engine engine)
    {
        CarEngine = engine;
    }
}
```

In this example, the Car class contains an Engine object, demonstrating an aggregation relationship where the Engine class represents a part of the Car class.

Through these examples, we can see how both association and aggregation relationships can be implemented in C# using class properties and constructors.

### How can multiple inheritance be implemented in C# if there is no direct support?

In C#, there’s no direct support for multiple inheritance. However, multiple inheritance can be realized using interfaces. A class can implement multiple interfaces that may come from different sources.

### What does the principle of “composition over inheritance” mean and when is it useful?

Composition over inheritance is a software design approach that encourages the use of composition (where objects utilize other objects) over inheritance for code reusability. It can be useful when a class’s behavior requires dynamic changes or when inheritance might lead to undesired rigid coupling between classes.

### Why are exceptions in C# considered objects, and how do you create your own exception class?

In C#, exceptions are implemented as objects that inherit from the base Exception class. This allows for passing additional information about the exception and creating custom exception types. To create your own exception class, simply inherit it from the Exception class or one of its subclasses.

### What is the purpose of the “base” keyword in the context of inheritance in C#?

The base keyword allows you to call members from the base class when in a derived class. It is most commonly used in derived classes to call the constructor of the base class or to access other base class members that were overridden in the derived class.

### How is the “this” keyword used in C#?

The this keyword points to the present instance of the class. It is often used to point to the fields or methods of the current object, especially when method parameter names overlap with class field names.
