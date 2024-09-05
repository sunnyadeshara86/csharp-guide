# Advanced C# Concepts

## Working with collections and LINQ

### What are the key differences between the “IEnumerable” and “ICollection” interfaces? When is it optimal to use each?

Both IEnumerable and ICollection are interfaces in the .NET Framework designed for handling collections of data, but they serve different purposes:

> * IEnumerable provides the basic capability to iterate over a collection. It exposes an enumerator, which supports a simple iteration over a non-generic collection. Essentially, if you only need to enumerate over items, IEnumerable is sufficient.
> * ICollection extends IEnumerable and provides additional methods for manipulating the size of the collection and for adding, removing, and checking the existence of elements in the collection.

In practice, do the following:

> * Use IEnumerable when you simply want to iterate over a collection without needing to modify it
> * Use ICollection when you need to manipulate the collection itself, such as adding or removing items

### How does the “deferred execution” principle work in LINQ, and how does it impact performance?

Deferred execution in LINQ means that actual data processing or computation does not occur until the results are enumerated. When you construct a LINQ query, it just creates a query definition. The actual execution is delayed until you iterate over the query result, such as by using a foreach loop or converting the results with methods such as ToList() or ToArray(). This can enhance performance by avoiding unnecessary computations. However, it’s important to manage the moment when the data is actually materialized – that is, fetched and loaded into memory. Materializing the data too early can sometimes consume more resources, especially when the data source is substantial, such as a database. You might want to append more conditions or filters to the query before deciding to materialize the results to optimize resource usage and performance.

### What are the primary differences between the “Where” and “Select” LINQ methods, and when is it best to use each?

Both Where and Select are extension methods provided by LINQ, but they serve different purposes:

> * Where: This method is used for filtering collections based on a given predicate. It returns a new collection that includes only those elements that satisfy a specified condition.
> * Select: This method is used for projecting or transforming the elements of a collection. It returns a new collection with elements that have been transformed based on a specified function or projection.

In practice, do the following:

> * Use Where when you want to filter a collection and retain only those elements that meet certain criteria
> * Use Select when you want to transform the elements of a collection, such as extracting a specific property or converting the data in some way

### What are the differences between the “All” and “Any” LINQ methods, and how do they behave when applied to an empty collection?

Both All and Any are LINQ methods used to evaluate collections against specific criteria. Here are their differences:

> * All: Checks if every element in the collection satisfies a particular condition. Use All when you need to ensure that all elements of a collection meet a specific criterion.
> * Any: Checks if at least one element in the collection satisfies a particular condition. Use Any when you need to determine if there are any elements that fulfill a specific criterion.

When the collection is empty, the following happens:

> * All: Always returns true because there are no elements that would violate the condition. This might seem counter-intuitive, but in the absence of any elements to check, it defaults to true.
> * Any: Always returns false since there are no elements present to satisfy the condition.

For instance, if you want to verify that all numbers in a list are positive, you’d use All. If you’re going to check if there’s a negative number in the list, you’d use Any.

### What distinguishes “FirstOrDefault” from “SingleOrDefault”, and when do these methods return “null”?

Both FirstOrDefault and SingleOrDefault are used to retrieve an element from a collection, but they serve slightly different purposes:

> * FirstOrDefault: Returns the first element that matches a condition or the first element if no condition is specified. If no matching element is found, it returns the default value (typically null for reference types).
> * SingleOrDefault: Returns the only element that matches a condition but throws an exception if there’s more than one matching element. If no elements match the condition, it returns the default value.

In terms of returning null, the following applies:

> * For reference types, both methods return null when no matching elements are found in the collection
> * However, for value types (such as int and double), they would return the default value of the type (such as 0 for int)

### What are the primary collection types in .NET you consider, and what are their key differences?

.NET provides several primary collection types:

> * List<T>: A dynamic array of elements. It maintains order and allows duplicate elements.
> * Dictionary<TKey, TValue>: A collection of key-value pairs. It does not have a defined order, and keys must be unique.
> * HashSet<T>: A set of unique elements. It does not maintain any specific order.
> * Queue<T>: A collection supporting First-In-First-Out (FIFO) operations.
> * Stack<T>: A collection supporting Last-In-First-Out (LIFO) operations.

### What are the differences between “List<T>” and “Dictionary<TKey”, “TValue>”?

The primary distinction between List<T> and Dictionary<TKey, TValue> lies in how you access elements. In List<T>, elements are accessed by their index, whereas in Dictionary<TKey, TValue>, elements are accessed by their key.

### How can you optimize the execution of LINQ queries when dealing with large datasets?

Optimizing LINQ queries, especially with substantial datasets, can be achieved through several approaches:

> * Utilize deferred execution whenever possible, ensuring that queries are only executed when the result is genuinely required. This avoids unnecessary computations.
> * Choose the most efficient collection type tailored for your specific use case, as the underlying data structure can impact performance.
> * Limit the size of the resulting dataset when feasible using methods such as Take to avoid processing more data than necessary.
> * Avoid or judiciously use nested queries. They can lead to performance issues due to multiple rounds of data retrieval or computations.
> * Use methods such as ToArray or ToList to materialize results into memory if you anticipate multiple operations on the data. This can prevent repeated execution of the same LINQ query.

### What are the key differences between the “IEnumerable” and “IQueryable” interfaces? Explain their implementation and usage scenarios.

IEnumerable and IQueryable are two primary interfaces representing collections in .NET. This is what they do:

> * IEnumerable: Operates at the object level in memory. When you execute LINQ queries against an IEnumerable interface, operations are performed in memory. It’s suitable for working with in-memory collections such as arrays or lists.
> * IQueryable: Designed for interacting with external data sources (for example, databases). Queries made with IQueryable get translated into queries specific to the data source (such as SQL for relational databases). This interface allows for deferred execution and out-of-memory (OOM) data querying, making it efficient for large datasets, especially in databases.

The main distinction between these two interfaces lies in the execution location: IEnumerable processes data in memory. Meanwhile, IQueryable allows the construction of an expression tree that can be translated into a query suitable for an external data source, such as SQL for databases. Then, it sends the parsed query for processing to the data source and fetches the results as IEnumerable.

### What’s the key difference between an array and “List<T>” in C#? When is it optimal to use each of these structures?

The primary distinction lies in flexibility and size. Arrays have a fixed size once defined, while List<T> can dynamically resize as elements are added or removed.

Arrays are typically faster for indexed access compared to other data structures, and they can be more memory-efficient since there’s no overhead associated with storing additional metadata or maintaining unused capacity, which is often the case with lists. Arrays are particularly suitable when the number of items is known upfront and remains constant, as they cannot dynamically resize as lists can.

On the other hand, List<T> provides a host of useful methods for manipulation and can grow or shrink as needed. It’s an optimal choice when the collection size is uncertain or if you need the added functionality and methods that List<T> provides over arrays.

In essence, while arrays are more lightweight and efficient for static collections, List<T> offers more versatility for dynamic collections.

### In which scenarios should one prefer “HashSet<T>” over “List<T>”?

> * HashSet<T> maintains a collection of unique elements and is optimized for operations that require fast lookups, insertions, and deletions, as well as ensuring uniqueness. Use HashSet<T> when you need to prevent duplicates or when frequent lookup operations are carried out.
> * List<T> is an ordered collection that can contain duplicates and is useful when the order of elements matters.

The choice between the two largely depends on the specific use case and the operations you intend to perform more frequently.

### What is the key distinction between “LinkedList<T>” and “List<T>” in C#? In which scenarios is it optimal to use “LinkedList<T>”?

LinkedList<T> is a doubly linked list, where each node has references to the previous and next nodes. In contrast, List<T> is a dynamic array. The fundamental difference lies in how the data is stored and how it can be modified. LinkedList<T> is optimal for insertion and deletion operations in the middle of the list, given its node-based structure, which allows for efficient node addition or removal without shifting other elements. Conversely, List<T> is efficient for indexed access due to its array-backed nature.

When frequent insertions or deletions are expected, especially in the middle of a collection, LinkedList<T> can be more efficient. However, if the primary operations involve indexed access or if the collection size remains relatively static, List<T> might be a better choice.

### What does “Dictionary<TKey, TValue>” represent in C#, and what are typical scenarios for its use?

Dictionary<TKey, TValue> in C# is a collection of key-value pairs where the keys are unique. This data structure allows fast lookups, insertions, and deletions based on keys. Typical scenarios for its use include storing configuration settings, caching data, and scenarios where you need to quickly retrieve a value associated with a unique key, such as a lookup table or a dictionary.

### What are immutable collections in C#? What are their advantages and disadvantages?

Immutable collections in C# are collections that cannot be modified after they are created. Instead of modifying them directly, any operation that would change the collection returns a new instance of the collection with the desired changes. Advantages of using immutable collections include thread safety (since there’s no risk of another thread modifying the collection unexpectedly) and the assurance that the data remains unchanged throughout its life cycle. On the downside, they can be less performant than mutable counterparts, especially when frequent modifications are needed, as each modification results in a new collection being created. This can also lead to increased memory usage.

## Exception handling and debugging

### What’s the difference between using “throw” and “throw ex” inside a “catch” block?

When you use throw without any argument, you’re essentially rethrowing the current exception, preserving the original stack trace. This allows for easier debugging as you maintain the information about where the exception was originally thrown. On the other hand, when you use throw ex, you reset the stack trace to the current catch block, potentially losing valuable information about where and how the exception originated. Therefore, in general, it’s recommended to use throw by itself within a catch block if you intend to rethrow the caught exception.

### What are the primary types of exceptions in C# and under what conditions do they typically arise?

C# features a wide variety of exception types to cater to different exceptional scenarios. Here are a few key ones:

> * ArgumentNullException: This is thrown when an argument passed to a method is null when a non-null value is expected
> * ArgumentOutOfRangeException: This occurs when an argument’s value is outside the permissible range
> * DivideByZeroException: This is thrown when there’s an attempt to divide by zero
> * InvalidOperationException: This arises when the state of an object doesn’t permit a particular operation
> * FileNotFoundException: This occurs when a file that’s being attempted to be accessed doesn’t exist
> * StackOverflowException: This is thrown when there’s a stack overflow due to excessive recursion or other reasons
> * NullReferenceException: This occurs when you try to access a member on an object reference that is null

### What does the “finally” block do in a “try-catch” structure, and are there scenarios where it might not execute?

The finally block ensures that the code inside it gets executed regardless of whether an exception was thrown in the preceding try or catch blocks. This is particularly useful for cleanup operations, such as closing files or database connections.

In most cases, the finally block will execute. However, there are rare circumstances, such as program termination or catastrophic exceptions (for example, StackOverflowException or a process termination), where the finally block might not get executed because these critical errors can disrupt the normal flow of program execution, and the app will stop, leaving no opportunity for the finally block to run.

### What is an “inner exception”, and how can it be used to improve debugging?

An inner exception refers to a previous exception that led to the current exception being thrown. It’s especially useful when the current exception arises as a result of another exception. By examining the inner exception, developers can trace back to the root cause of a problem, providing a clearer picture of the sequence of events leading up to the final exception. This can be invaluable during debugging, as it helps pinpoint the primary source of the issue and, potentially, cascading failures that led to the current state. When throwing a custom exception, you can include the original exception as the inner exception, preserving this chain of causality.

### What is a “stack trace”, and how can it be beneficial in tracing exceptions?

A stack trace provides a snapshot of the method call sequence leading up to the point where an exception was thrown. It essentially shows the hierarchy of method calls that the application went through before encountering the exception. This can be instrumental for developers as it offers insights into the execution flow and context in which the exception occurred. By analyzing the stack trace, developers can often pinpoint the exact location and reason for the exception, making debugging and resolving the issue more efficient.

### What is the essence of a “conditional breakpoint” in Visual Studio, and when is it beneficial to use?

A conditional breakpoint is a specialized breakpoint that pauses the execution of your code only when a specific condition is met. Instead of halting execution every time a particular line of code is reached, it only does so if the condition you’ve specified evaluates to true. This is particularly useful in scenarios where an issue arises only in certain circumstances or with specific data. By using a conditional breakpoint, developers can efficiently debug complex problems without having to manually pause and inspect the program state multiple times.

### How can we handle or avoid an “unhandled exception”?

An unhandled exception occurs when an exception arises in your code that isn’t caught by any catch block. To prevent this, do the following:

> * Surround potential exception-throwing code with appropriate try-catch blocks, ensuring that you are catching specific exception types or a general exception if necessary.
> * Utilize global exception handlers, such as AppDomain.UnhandledException for .NET Framework applications or TaskScheduler.UnobservedTaskException to handle exceptions from unobserved tasks. This provides a safety net, ensuring that any uncaught exceptions are still addressed in some manner.
> * Always validate and sanitize inputs, and be aware of potential exception sources such as I/O operations, database access, and third-party library calls.

### What is the difference between “Debug” and “Release” configurations?

In Visual Studio, the two primary build configurations are Debug and Release. The Debug configuration is tailored for code debugging. It usually includes additional debugging information, doesn’t apply certain compiler optimizations, and might have different code paths (such as more verbose logging) enabled by using preprocessor directives. This ensures that the debugging experience is seamless, allowing developers to step through code, inspect variables, and use breakpoints effectively.

On the other hand, the Release configuration is optimized for the final deployment of the application. The code is compiled with full optimization, removing any debugging information, which leads to better performance and often a smaller binary size. Additionally, certain debug-specific code paths might be excluded, ensuring that the final product is lean and efficient.

Understanding and choosing the right configuration is essential as it can significantly impact both the performance and behavior of the application.

### How can one deliberately trigger an exception?

You can use the throw keyword to programmatically generate an exception. For instance, executing throw new Exception("Test exception"); will raise an exception with a "Test exception" message. Deliberately triggering exceptions can be useful in situations where you want to enforce certain conditions or validate assumptions in your code.

### What’s the distinction between using “Assert” and “Throw” in unit test development and debugging?

Assert is primarily used to validate conditions that are expected to be true at specific points in the code. If the condition is not met, an assertion failure typically halts the execution, alerting the developer of the discrepancy, especially during debugging sessions. It’s a tool to ensure code correctness and assumptions during development.

On the other hand, Throw is employed to raise exceptions, indicating error conditions or unexpected scenarios. These exceptions can be caught and handled further up the call stack.

While both can be used to identify and address issues, their primary purposes and usage contexts differ: Assert is more about validating code logic during development, whereas Throw is about handling exceptional runtime scenarios.

### How should one handle exceptions in “Task”? What’s the difference between “async void” and “async Task” in the context of error handling?

When dealing with exceptions in Task, there are several approaches. One can use the ContinueWith method on a task to handle exceptions, or use the await keyword and wrap the awaited task inside a try-catch block to catch any exceptions it might throw.

The distinction between async void and async Task methods is crucial when it comes to exception handling. async void methods don’t return a task, so exceptions thrown from such methods get thrown directly into the thread pool. This can lead to unobserved exceptions which, at best, could crash the application if not caught, and at worst, might silently fail without any indication to the developer. async Task, on the other hand, returns a task that encapsulates the operation, and exceptions can be observed and handled by awaiting the task or inspecting its result.

## Asynchronous programming with async and await

### What is the purpose of the “async” and “await” keywords in C#?

The async and await keywords in C# are used to denote and execute asynchronous operations, allowing for non-blocking code execution. The async keyword indicates that a method may contain asynchronous code, while await is used to asynchronously wait for a task to complete without freezing the main thread. This enables writing more responsive applications, especially when dealing with I/O-bound operations or long-running computations.

### What’s the main difference between multithreading and asynchronous programming?

Multithreading involves running multiple threads concurrently in a single process to optimize execution. It’s about using multiple threads to achieve parallelism. Asynchronous programming, on the other hand, focuses on allowing code to continue its execution without waiting for long-running operations (such as I/O) to complete. Asynchronous code can run on a single thread, utilizing mechanisms such as an event loop to handle non-blocking operations efficiently.

### What does an “async” method return?

An async method can return void, Task, Task<T>, or ValueTask<T>. However, it’s generally recommended to avoid returning void from async methods, except in event handlers, because it makes error handling difficult; exceptions thrown in an async void method can’t be caught by the caller, leading to unhandled exceptions, which can crash the application. Returning Task or Task<T> allows the caller to await its completion or chain other continuations.

### What pitfalls can arise from the careless use of “async” and “await”?

Careless use of async and await can lead to several issues:

> * Deadlocks: Especially when mixing synchronous and asynchronous code
> * Thread starvation: Over-relying on the thread pool can lead to situations where all threads are consumed, causing delays in processing
> * Performance overheads: Unnecessary usage can introduce performance overheads
> * Debugging complexity: Asynchronous code can be more challenging to debug due to its non-linear execution flow

### What is a “deadlock” in the context of asynchronous programming, and how can it be avoided?

In the context of asynchronous programming, a deadlock occurs when asynchronous code inadvertently gets blocked waiting for another operation to complete, which in turn is waiting for the original operation. This creates a situation where neither operation can proceed. Deadlocks often arise when mixing synchronous and asynchronous code or when awaiting tasks inappropriately. To avoid deadlocks, follow these guidelines:

> * Avoid synchronously waiting on asynchronous methods (for example, avoid using .Result or .Wait())
> * Use ConfigureAwait(false) judiciously to prevent marshaling the continuation back to the original context, which can be a source of deadlocks, especially in UI applications

### How does asynchrony impact the call stack?

Asynchrony can fragment the call stack into several segments. When asynchronous methods are invoked, they return almost immediately, often before the work is complete. This means the traditional call stack might not represent the full sequence of execution, complicating debugging. Tools such as the Tasks window in Visual Studio can help developers understand the state and flow of asynchronous operations.

### What’s the difference between “Task”, “Task<T>”, and “ValueTask<T>”?

Let’s have a look at what the differences between these types are:

> * Task represents an asynchronous operation that doesn’t return a value. It’s essentially a promise that some work will be completed in the future.
> * Task<T> represents an asynchronous operation that returns a value of type T upon completion.
> * ValueTask<T> is a newer type optimized for scenarios where the result might be available synchronously, potentially avoiding heap allocation. It’s particularly useful for high-performance scenarios to reduce overhead, but it should be used with care as misuse can introduce subtle bugs or decrease performance.

### How can multiple asynchronous operations be executed concurrently and awaited for their completion?

You can use Task.WhenAll() to execute multiple asynchronous operations concurrently and await their completion. This method returns a single Task object that completes when all of the provided tasks have been completed. It’s a way to initiate several tasks at once and then continue execution when all of those tasks are done.

### What issues might arise when using asynchronous methods in class constructors or finalizers?

A few issues may arise, such as the following:

> * Using asynchronous methods in constructors can complicate object initialization since constructors can’t return a Task object. This means you can’t call await an asynchronous method directly inside a constructor, making it challenging to perform asynchronous operations during object initialization.
> * Using asynchronous methods in finalizers may lead to a problem because the object might get garbage collected before the asynchronous operation completes. Finalizers are not meant to have asynchronous code, and doing so can lead to unpredictable behavior.

### How are exceptions handled in asynchronous methods?

Exceptions in asynchronous methods can be handled using standard try-catch blocks. However, it’s important to note that exceptions might not be thrown until the task becomes faulted. This means that the exception will be thrown at the point where you call await for the task. If an exception occurs in an awaited asynchronous method, it will propagate to the calling method, just as with synchronous code. It’s also worth noting that if multiple exceptions are thrown by concurrent tasks awaited with Task.WhenAll(), all exceptions will be bundled into an AggregateException exception.

### What is “synchronization context” in asynchronous programming, and what is its significance?

Synchronization context represents the environment in which asynchronous operations run. It ensures that asynchronous code can interact correctly with environments that have specific requirements, such as UI threads in Windows Forms or WPF applications. This is crucial to ensure that operations interacting with the UI are executed on the appropriate thread. In essence, synchronization context acts as a bridge between asynchronous code and its execution context, allowing for thread-safe updates to UI or other thread-specific resources.

### How does “ConfigureAwait” work, and why is there a recommendation to use “ConfigureAwait(false)”?

ConfigureAwait allows developers to specify whether or not to return the execution to the original synchronization context after an asynchronous operation completes. Using ConfigureAwait(false) indicates that the continuation code shouldn’t run in the original context, potentially preventing deadlocks and improving performance, especially in library code. This ensures that the asynchronous method does not attempt to marshal the continuation back to the original context, which might be unnecessary or even detrimental.

### What is “task continuation”, and how is it used?

Task continuation allows you to specify a segment of code to execute after a Task instance completes. It’s often used via methods such as ContinueWith on a Task instance, allowing developers to chain operations without nesting callbacks. Continuations can be useful to define the logic that should run after an asynchronous operation without blocking the thread, making it easier to sequence asynchronous operations or handle results.

### How do asynchronous methods interact with threads?

Asynchronous methods don’t inherently spawn new threads. Instead, they use mechanisms to execute code asynchronously on the current thread, leveraging the thread pool for compute-bound operations when necessary. The key benefit of asynchronous methods is that they allow potentially blocking operations, such as I/O-bound work, to yield control, freeing up the current thread to perform other tasks. This leads to more efficient use of system resources, especially in scenarios where many operations might be waiting on external factors such as network responses or file reads.

### What is “TaskCompletionSource” in the context of asynchronous operations?

TaskCompletionSource provides a way to manually control the completion of a task. It’s particularly useful in scenarios where you need to integrate asynchronous code with other asynchronous mechanisms that don’t natively use the Task pattern. Essentially, with TaskCompletionSource, you have the ability to directly set the result, exception, or cancellation state of its associated task.

### What is a “cancellation token”, and how is it used?

A cancellation token provides a mechanism to request the cancellation of an ongoing operation. It’s typically passed into an asynchronous method, which can periodically check the token to see if a cancellation has been requested, allowing the operation to gracefully terminate early. This is especially important for long-running operations where you want to give the user or calling code the ability to interrupt and stop the operation.

### What’s the difference between “Parallel” from TPL and “async/await”?

Parallel is designed for parallel execution of code across multiple threads, focusing on CPU-bound operations that can be executed concurrently. It’s about optimizing CPU usage by distributing computations over multiple cores.

On the other hand, async/await is designed for the non-blocking execution of code, particularly for I/O-bound operations. It’s about improving responsiveness and scalability by allowing a thread to perform other tasks while waiting for a long-running operation to complete.

### What are Parallel loops in TPL, and how to control them?

In TPL, there are two main Parallel loops: Parallel.For and Parallel.ForEach.

You can control the number of threads by using ParallelOptions and setting MaxDegreeOfParallelism. The default value of MaxDegreeOfParallelism is set to -1, indicating that TPL automatically decides the number of threads to use, typically based on the number of processor cores. However, you can modify this value to limit the maximum number of threads. This can be useful in scenarios where tasks are resource-intensive and you don’t want to overload the system.

To manage loops, you can use the Break() and Stop() methods, as outlined here:

> * Break(): The Break() method indicates the need to cease the current iteration’s execution.Here’s an example:
> ```
> var options = new ParallelOptions { MaxDegreeOfParallelism = 2 };
> Parallel.For(0, 10, options, (i, state) => {
>     if (i == 5) {
>         state.Break();
>         return;
> }
>     Console.WriteLine($"Processing item {i}");
> });
> ```
> In the preceding example, Parallel.For processes numbers from 0 to 9. If it encounters the number 5, it uses Break() to halt further processing in the iteration.
> * Stop(): The Stop() method halts execution as quickly as possible. This method is essential for controlling the loop’s state.Here’s an example:
> ```
> Parallel.ForEach(dataCollection, (data, state) => {
>     if (someCondition) {
>         state.Stop();
>         return;
>     }
>     // Process data
> });
> ```
> In the preceding example, if you’re processing a large list of data and encounter a critical error, you can use Stop() to immediately cease processing.

### How to use Parallel.ForEachAsync, and what is the difference between it and Parallel.ForEach?

Parallel.ForEach is a synchronous method used for executing iterations in parallel.

Parallel.ForEachAsync supports asynchronous operations within iterations. This is useful when you need to perform asynchronous requests or operations with waiting times, such as interactions with databases or web services.

Here’s an example:

```
await Parallel.ForEachAsync(dataCollection, async (data, cancellationToken) => {
    // Asynchronous processing of each data item
    await ProcessDataAsync(data);
});
```

In the preceding example, Parallel.ForEachAsync allows each item in the data collection to be processed asynchronously, which is beneficial for tasks that involve latency, such as database queries or calls to web services.

### When is it appropriate to call an asynchronous function without using await, and how does this affect execution?

You can invoke an asynchronous function without await if you do not need to wait for its completion before moving to the next line of code. However, this can lead to issues such as untracked errors and difficulties in managing thread execution. The method’s execution continues irrespective of the state of the asynchronous operation, potentially leading to unpredictable behavior, especially if it affects shared resources or the application’s state.

Also, an asynchronous function can be called without await when you need to initiate several asynchronous tasks simultaneously. However, without await, you cannot catch exceptions that might occur during task execution, and the result of the operation will be ignored.

Here are some examples:
> * Here, it’s ignoring the result:
> ```
> _ = DoSomeAsync();
> ```
> * Here, it’s running tasks in parallel:
> ```
> public async Task ProcessDataAsync(IEnumerable<Data> dataList) {
>     var tasks = new List<Task>();
>     foreach (var data in dataList) {
>         tasks.Add(ProcessSingleDataAsync(data));
>     }
>     await Task.WhenAll(tasks);
> }
> public async Task ProcessSingleDataAsync(Data data) {
>     await Task.Delay(TimeSpan.FromSeconds(1));
>     return data;
> }
> ```

In the second example, ProcessDataAsync initiates several asynchronous tasks in parallel and waits for their completion using Task.WhenAll. This approach is useful for efficiently processing multiple tasks concurrently.

### What are “asynchronous streams” in C# 8.0, and how can “IAsyncEnumerable” transform real-time data processing?

Introduced in C# 8.0, asynchronous streams allow you to asynchronously iterate over collections using await foreach. IAsyncEnumerable is an interface that facilitates creating data streams that can be read asynchronously. This is particularly beneficial when dealing with large data streams or data sources that produce data asynchronously. It provides a way to process data as it becomes available, rather than waiting for the entire dataset, making it especially valuable for real-time applications.

### How can you use “SemaphoreSlim” for asynchronous synchronization of resource access?

SemaphoreSlim offers a WaitAsync method, which allows for asynchronously obtaining a semaphore. This is advantageous when you need to limit concurrent access to a shared resource in asynchronous code without blocking the executing thread. By using SemaphoreSlim, you can ensure that a limited number of tasks can access a particular resource or section of code at the same time, providing a mechanism for throttling or controlling access.

### What is “asynchronous disposal” in C# 8.0 with the use of “IAsyncDisposable”?

Asynchronous disposal in C# 8.0 provides a mechanism for objects to release resources asynchronously. The IAsyncDisposable interface introduces the DisposeAsync() method, which can be implemented to perform asynchronous cleanup operations. This is particularly beneficial for resources that require asynchronous interactions for their disposal, such as network streams or database connections. By allowing asynchronous disposal, resources can be released more efficiently, and it helps prevent potential deadlocks or blocking scenarios, especially in contexts that heavily rely on asynchronous operations.

## Garbage collection

### What is the primary difference between the stack and heap in the context of memory management and garbage collection in C#?

The stack is used for storing local variables, method execution details, and controlling program flow. It operates in a LIFO manner, and memory is automatically reclaimed when the method or block of code exits. The heap, on the other hand, is used for storing dynamically allocated memory such as objects. Memory on the heap is managed by the GC in C#. Objects in the heap exist until the GC determines that they are no longer reachable and reclaims the memory.

### How does .NET recognize that an object has no active references and is ready for garbage collection?

.NET uses a mark-and-sweep algorithm for garbage collection. Initially, all objects on the heap are considered unreachable. Starting with root objects (for example, global and static objects, local variables on the stack, and CPU registers), the GC traces and marks each object that is accessible. After the marking phase, any object that remains unmarked is considered garbage and is a candidate for collection. These unreachable objects are then swept or collected, freeing up the memory they occupied.

### Why are generations in garbage collection important, and how do they function?

Generations in garbage collection optimize the collection process. The .NET GC uses a generational approach, dividing the heap into three generations: 0, 1, and 2. Let’s take a closer look at these:

> * Generation 0 (Gen 0): Contains short-lived objects, such as temporary variables. Collecting this generation is fast and occurs frequently.
> * Generation 1 (Gen 1): Acts as a buffer between short-lived objects and long-lived objects.
> * Generation 2 (Gen 2): Contains long-lived objects.

The idea behind this approach is that most objects are short-lived. By collecting Gen 0 frequently, the GC can efficiently reclaim memory from short-lived objects without having to scan older generations. Objects that survive a collection are promoted to the next generation, and the GC checks older generations less frequently.

### What is the difference between the “Finalize” and “Dispose” methods in memory management?

> * Finalize: The Finalize method is called by the GC before it reclaims the memory occupied by an object. It’s defined in the object’s destructor and is intended to release unmanaged resources that the object might be holding. However, relying on finalization has its pitfalls as you can’t predict when the GC will run, making it non-deterministic.
> * Dispose: The Dispose method is a part of the IDisposable interface. When implemented, it provides a deterministic way to release both managed and unmanaged resources. Typically, you’d call the Dispose method explicitly or use the object inside a using statement in C#, ensuring that Dispose gets called when the object goes out of scope. Using Dispose allows for timely resource cleanup, ensuring that resources such as file handles, database connections, and so on are released as soon as they are no longer needed.

### How can you signal to the GC about the need for a garbage collection?

You can explicitly request the GC to perform a collection using the GC.Collect() method. However, it’s important to note that manually invoking garbage collection is usually discouraged. The GC is optimized to run at optimal times based on the application’s memory consumption patterns. Forcing a collection can disrupt these optimizations and potentially degrade performance.

### What does “memory leak” mean in .NET, and how can garbage collection assist in detecting it?

A memory leak in .NET refers to situations where objects remain in memory even though they are no longer needed or accessible. While the GC is designed to automatically reclaim memory occupied by unreachable objects, it can’t free objects that still have active references. Therefore, even if an object is no longer in use but still has references pointing to it (for example, due to event handlers or static collections), it will not be collected, leading to memory leaks.

### How can weak references help prevent objects from being locked by the GC?

Weak references allow you to hold a reference to an object without preventing that object from being collected by the GC. This can be useful when you want to maintain a cache or temporary reference to an object but don’t want that reference to be the sole reason the object remains in memory. When the only existing references to an object are weak references, the object becomes eligible for garbage collection. By using the WeakReference class in .NET, you can access the target object if it’s still in memory, but you don’t prevent the GC from collecting it when necessary.

### What is the purpose of the “GC.KeepAlive()”method, and when should it be used?

The GC.KeepAlive() method ensures that a specified object remains alive and is not collected by the GC until the method call. This can be useful for preventing premature garbage collection, especially for objects with significant finalization logic. For example, if an object holds a resource such as a file handle or network connection and its finalizer releases that resource, using GC.KeepAlive() can prevent the finalizer from running prematurely.

### How do GC modes of operation (for example, workstation and server) influence its activity?

The GC in .NET operates in different modes to optimize for different scenarios:

> * Workstation mode: Typically used for single-threaded applications or applications running on a single-core machine. It does not utilize parallelism for garbage collection and is designed to be less intrusive, prioritizing application responsiveness.
> * Server mode: Optimized for multi-core systems and uses parallel garbage collection to maximize throughput. It’s suitable for server applications where performance and scalability are essential.

These modes adjust the GC’s behavior to better match the expected application workload and hardware.

### What’s the difference between the Large Object Heap and the regular heap, and how does it impact garbage collection?

The Large Object Heap (LOH) is a special heap in .NET’s memory management used to store objects that are 85,000 bytes or larger. The primary differences between LOH and a regular heap are set out here:

> * LOH is not compacted as frequently as regular heaps. Compacting large objects can be performance-intensive.
> * Objects in LOH are collected during a Gen 2 garbage collection.

Because of these characteristics, it’s essential to be cautious when allocating large objects frequently, as it can lead to memory fragmentation and increased Gen 2 collections.

### What impact do pinned objects have on the operation of the GC, and what is the Pinned Object Heap?

Pinned objects are objects that the GC is instructed not to move during a memory compaction phase. This is essential when the memory address of an object needs to remain constant, typically when interfacing with native code. Pinned objects can disrupt the efficient compaction of memory and lead to fragmentation. The Pinned Object Heap (POH), introduced in .NET 5, is a dedicated segment for storing pinned objects, ensuring that they don’t interfere with regular heaps and providing more efficient management of pinned objects.

### How does the presence of finalizers in objects impact the garbage collection process?

Objects with finalizers complicate the garbage collection process because they require two garbage collection cycles for their complete cleanup. In the first cycle, when the object is detected as unreachable, its finalizer is called. The object is then moved to a list of finalized objects. Only in a subsequent garbage collection cycle is the object actually reclaimed. This means objects with finalizers stay in memory longer, which can potentially lead to increased memory usage if not managed correctly.

### How does the GC handle objects that are frequently created and destroyed (for instance, in a loop)?

The GC employs generational collection. Objects that are frequently created and likely to be short-lived are placed in the younger generation (Gen 0). The idea is that it’s more efficient to collect from this generation (Gen 0) frequently, as many objects will become unreachable quickly. When garbage collection occurs for this generation, only a subset of the heap (the younger generation) is considered, making the process faster. Objects that survive multiple collections are promoted to older generations, which are collected less frequently.

### How does the usage of unmanaged resources impact the GC, and how can one ensure their proper disposal?

Unmanaged resources, such as file handles, database connections, or native memory, are not managed by the .NET GC. If not handled properly, they can lead to resource leaks. To ensure their proper disposal, follow these guidelines:

> * Implement the IDisposable interface: This allows you to provide a Dispose method where you can release unmanaged resources.
> * Use a using statement: This ensures that the Dispose method is called automatically when the object goes out of scope.
> * Use finalizers: In situations where developers might forget to call Dispose, a finalizer (~ClassName method) can be used to release resources. However, relying solely on finalizers can introduce delays in resource cleanup, so it’s recommended to use them as a backup to the Dispose method.
