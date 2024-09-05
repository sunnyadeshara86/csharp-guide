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

