# Android and Kotlin Interview Questions and Answers

## Question: What is an inline function in Kotlin?
Answer: An inline function in Kotlin is a function marked with the 'inline' keyword. The compiler replaces the function call with the actual function body at compile time, which can improve performance for small, frequently called functions.

## Question: What is the advantage of using const in Kotlin?
Answer: The 'const' keyword in Kotlin is used for compile-time constants. It provides better performance as the value is inlined where it's used, and it allows the constant to be used in annotations.

## Question: What is a reified keyword in Kotlin?
Answer: The 'reified' keyword is used with inline functions to access the type passed as a type parameter at runtime, which is normally erased due to type erasure in the JVM.

## Question: Suspending vs Blocking in Kotlin Coroutines
Answer: Suspending functions can be paused and resumed without blocking the thread, while blocking operations occupy the thread until completion. Suspending is more efficient for concurrent operations.

## Question: Launch vs Async in Kotlin Coroutines
Answer: 'launch' is used for fire-and-forget coroutines that don't return a result, while 'async' is used when you need to return a result (Deferred) from the coroutine.

## Question: internal visibility modifier in Kotlin
Answer: The 'internal' modifier makes a declaration visible only within the same module. It's more restrictive than 'public' but less so than 'private'.

## Question: open keyword in Kotlin
Answer: The 'open' keyword in Kotlin is used to allow a class or function to be inherited or overridden. By default, classes and functions in Kotlin are final.

## Question: lateinit vs lazy in Kotlin
Answer: 'lateinit' is used for var properties that will be initialized later, while 'lazy' is used for val properties that are computed on first access.

## Question: What is Multidex in Android?
Answer: Multidex is a feature that allows Android apps to overcome the 65,536 method limit of a single DEX file by splitting the app into multiple DEX files.

## Question: How does the Android Push Notification system work?
Answer: Android Push Notifications use Firebase Cloud Messaging (FCM). The app registers with FCM, receives a token, sends it to the server. The server uses this token to send messages to FCM, which then delivers them to the device.

## Question: What is a ViewModel and how is it useful?
Answer: ViewModel is part of Android Architecture Components. It stores and manages UI-related data, surviving configuration changes and providing clean separation of concerns.

## Question: Is it possible to force the Garbage Collection in Android?
Answer: While you can suggest garbage collection using System.gc(), it's not recommended as the system is better at deciding when to perform GC.

## Question: What is a JvmStatic Annotation in Kotlin?
Answer: @JvmStatic is used in Kotlin to generate additional static methods for functions in objects or companion objects, making them easier to call from Java.

## Question: init block in Kotlin
Answer: An init block in Kotlin is executed when the class is instantiated, right after the primary constructor. It's used for initialization logic.

## Question: JvmField Annotation in Kotlin
Answer: @JvmField exposes a Kotlin property as a field to Java, without getter and setter methods.

## Question: singleTask launchMode in Android
Answer: singleTask launch mode ensures only one instance of the activity exists in the task. If it exists, it's brought to the front and onNewIntent() is called.

Comparison and Use Cases
standard: Use when you want each activity to always create a new instance.
singleTop: Use when the activity should not create a new instance if it is already at the top of the stack. Ideal for activities like a news reader, where returning to the same content should not spawn multiple instances.
singleTask: Use for activities that should exist as a single instance within a task. This is often used for the main entry points of the app.
singleInstance: Use for activities that should not have any other activities in the same task. This is rare but useful for highly specialized activities.



## Question: Difference between == and === in Kotlin
Answer: '==' checks for structural equality (calls equals() method), while '===' checks for referential equality (checks if two references point to the same object).

## Question: JvmOverloads Annotation in Kotlin
Answer: @JvmOverloads generates multiple overloaded methods in Java for Kotlin functions with default parameter values.

## Question: Why is it recommended to use only the default constructor to create a Fragment?
Answer: Using only the default constructor ensures that the Fragment can be recreated by the system during configuration changes or process death and rebirth.

## Question: Why do we need to call setContentView() in onCreate() of Activity class?
Answer: setContentView() sets the content view (layout) for the Activity. It's called in onCreate() to define the UI as soon as the Activity is created.

## Question: When only onDestroy is called for an activity without onPause() and onStop()?
Answer: This can happen when finish() is called from the onCreate() method, or when the system kills the app process due to memory pressure without giving it time to go through the usual lifecycle.



# Kotlin Programming Concepts

## Higher-Order Functions in Kotlin

Higher-order functions are functions that take other functions as parameters or return them. They allow for more abstract and reusable code. For example:

```kotlin
// Higher-order function
fun higherOrderFunction(operation: (Int, Int) -> Int, a: Int, b: Int): Int {
    return operation(a, b)
}

// Usage
val sum = higherOrderFunction({ x, y -> x + y }, 5, 3)
println(sum) // Output: 8
```

## Lambdas in Kotlin

Lambdas are anonymous functions that can be used to create function objects. They are often used as arguments to higher-order functions. For example:

```kotlin
// Lambda expression
val multiply: (Int, Int) -> Int = { x, y -> x * y }

// Usage
val result = multiply(4, 5)
println(result) // Output: 20
```

## `associateBy` - List to Map in Kotlin

`associateBy` transforms a list into a map, where the keys are derived from the list elements. For example:

```kotlin
data class Person(val name: String, val age: Int)

val people = listOf(Person("Alice", 30), Person("Bob", 25))
val peopleMap = people.associateBy { it.name }

println(peopleMap["Alice"]) // Output: Person(name=Alice, age=30)
```

## `open` Keyword in Kotlin

The `open` keyword allows a class or method to be extended or overridden. By default, classes and methods are final and cannot be subclassed or overridden.

```kotlin
open class Base {
    open fun show() {
        println("Base class")
    }
}

class Derived : Base() {
    override fun show() {
        println("Derived class")
    }
}
```

## `companion object` in Kotlin

A `companion object` is a singleton object that is associated with a class. It can hold methods and properties that can be accessed without creating an instance of the class.

```kotlin
class MyClass {
    companion object {
        fun create(): MyClass = MyClass()
    }
}

// Usage
val instance = MyClass.create()
```

## `internal` Visibility Modifier in Kotlin

The `internal` modifier makes a class or member visible within the same module. It is more restrictive than `public` but less restrictive than `private`.

```kotlin
internal class InternalClass {
    internal fun internalFunction() {
        println("Internal function")
    }
}
```

## `partition` - Filtering Function in Kotlin

The `partition` function splits a list into two lists based on a predicate. It returns a `Pair` of lists.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val (evens, odds) = numbers.partition { it % 2 == 0 }

println(evens) // Output: [2, 4]
println(odds)  // Output: [1, 3, 5]
```

## Infix Notation in Kotlin

Infix notation allows you to call methods without using parentheses. The method must be a member function or an extension function with a single parameter.

```kotlin
infix fun Int.add(other: Int): Int = this + other

val sum = 5 add 3
println(sum) // Output: 8
```

## Kotlin Multiplatform

Kotlin Multiplatform allows you to write shared code that can run on multiple platforms, including JVM, JavaScript, and native. It enables code sharing across different platforms while maintaining platform-specific code.

```kotlin
expect fun platformName(): String

actual fun platformName(): String = "Android"
```

## Suspending vs Blocking in Kotlin Coroutines

Suspending functions are non-blocking and can be paused and resumed, while blocking functions block the thread until completion. Coroutines are designed to handle suspending operations efficiently without blocking the thread.

```kotlin
// Suspending function
suspend fun fetchData(): String {
    delay(1000)
    return "Data"
}

// Blocking function
fun fetchDataBlocking(): String {
    Thread.sleep(1000)
    return "Data"
}
```

## String vs `StringBuffer` vs `StringBuilder`

- `String` is immutable; any modification creates a new string.
- `StringBuffer` is mutable and thread-safe.
- `StringBuilder` is mutable but not thread-safe.

```kotlin
val string = "Hello"
val stringBuffer = StringBuffer("Hello")
val stringBuilder = StringBuilder("Hello")

stringBuffer.append(" World")
stringBuilder.append(" World")
```

## Difference Between `val` and `var`

- `val` declares a read-only (immutable) variable.
- `var` declares a mutable variable.

```kotlin
val immutable = 10
var mutable = 20

mutable = 30 // OK
// immutable = 15 // Error
```

## Checking if a `lateinit` Variable has Been Initialized

You can use the `::propertyName.isInitialized` syntax to check if a `lateinit` variable has been initialized.

```kotlin
lateinit var name: String

println(::name.isInitialized) // Output: false

name = "Kotlin"
println(::name.isInitialized) // Output: true
```

## Lazy Initialization of Variables in Kotlin

Use `lazy` to initialize a variable only when it is accessed for the first time.

```kotlin
val lazyValue: String by lazy {
    println("Initialized")
    "Hello"
}

println(lazyValue) // Output: Initialized, Hello
println(lazyValue) // Output: Hello
```

## Visibility Modifiers in Kotlin

- `public`: Visible everywhere.
- `private`: Visible only within the file or class.
- `protected`: Visible to the class and its subclasses.
- `internal`: Visible within the same module.

```kotlin
class Example {
    private val privateVal = "private"
    protected val protectedVal = "protected"
    internal val internalVal = "internal"
    public val publicVal = "public"
}
```

## Equivalent of Java Static Methods in Kotlin

Kotlin does not have static methods. Instead, you use `companion objects` to hold methods and properties that are associated with a class rather than instances.

```kotlin
class Example {
    companion object {
        fun staticMethod() {
            println("Static method")
        }
    }
}

// Usage
Example.staticMethod()
```

## Creating a Singleton Class in Kotlin

Use the `object` keyword to create a singleton class.

```kotlin
object Singleton {
    fun show() {
        println("Singleton instance")
    }
}

// Usage
Singleton.show()
```

## Difference Between `open` and `public` in Kotlin

- `open` allows a class or method to be overridden.
- `public` specifies visibility and does not affect inheritance.

```kotlin
open class Base {
    open fun show() {
        println("Base class")
    }
}

class Derived : Base() {
    override fun show() {
        println("Derived class")
    }
}
```

## Use-Case of `let`, `run`, `with`, `also`, `apply` in Kotlin

- `let`: Executes the code block with the object as a parameter and returns the result.
- `run`: Executes the code block with the object as a receiver and returns the result.
- `with`: Executes the code block with the object as a receiver and returns the result.
- `also`: Executes the code block with the object as a parameter and returns the object.
- `apply`: Executes the code block with the object as a receiver and returns the object.

```kotlin
val result = "Hello".let { it.toUpperCase() }
println(result) // Output: HELLO

val runResult = "Hello".run { length }
println(runResult) // Output: 5

val withResult = with("Hello") { length }
println(withResult) // Output: 5

val alsoResult = "Hello".also { println(it) }
println(alsoResult) // Output: Hello \n Hello

val applyResult = StringBuilder().apply { append("Hello") }.toString()
println(applyResult) // Output: Hello
```

## Choosing Between `apply` and `with`

- Use `apply` when you want to configure an object and return the object itself.
- Use `with` when you want to operate on an object and return a result, without modifying the original object.

## Difference Between `List` and `Array` Types in Kotlin

- `List` is an interface with immutable or mutable implementations.
- `Array` is a fixed-size data structure with a specific type.

```kotlin
val list = listOf(1, 2, 3)
val array = arrayOf(1, 2, 3)

println(list[0]) // Output: 1
println(array[0]) // Output: 1
```

## Labels in Kotlin

Labels are used to break out of nested loops or to continue from the outer loop.

```kotlin
outer@ for (i in 1..3) {
    for (j in 1..3) {
        if (j == 2) break@outer
        println("i = $i, j = $j")
    }
}
```

## Coroutines in Kotlin

Coroutines are lightweight threads that allow you to perform asynchronous programming. They can be suspended and resumed, making them suitable for managing concurrency.

```kotlin
suspend fun doSomething() {
    delay(1000)
    println("Done")


}
```

## Coroutine Scope

A `CoroutineScope` defines the context in which coroutines run and their lifecycle.

```kotlin
CoroutineScope(Dispatchers.Main).launch {
    // Coroutine code
}
```

## Coroutine Context

The `CoroutineContext` is a set of elements that configure coroutine behavior, such as dispatcher and job.

```kotlin
val context = CoroutineName("Example") + Dispatchers.IO
```

## `launch` vs `async` in Kotlin Coroutines

- `launch` starts a new coroutine and returns a `Job`.
- `async` starts a new coroutine and returns a `Deferred`, which can be used to obtain a result.

```kotlin
// Using launch
CoroutineScope(Dispatchers.Main).launch {
    // Code
}

// Using async
val deferred = CoroutineScope(Dispatchers.IO).async {
    // Code
    "Result"
}
println(deferred.await())
```

## `Thread.sleep()` vs `delay()` in Kotlin

- `Thread.sleep()` blocks the thread for a specified duration.
- `delay()` is a suspending function that does not block the thread.

```kotlin
// Using delay
suspend fun suspendFunction() {
    delay(1000)
    println("Delayed")
}

// Using Thread.sleep
fun blockingFunction() {
    Thread.sleep(1000)
    println("Blocked")
}
```

## When to Use Kotlin Sealed Classes

Sealed classes are used to represent a restricted class hierarchy, where a value can have one of a limited set of types. They are useful for representing a closed set of types.

```kotlin
sealed class Result
class Success(val data: String) : Result()
class Error(val message: String) : Result()
```

## Collections in Kotlin

Kotlin collections include `List`, `Set`, and `Map`. They can be mutable or read-only.

```kotlin
val list = listOf(1, 2, 3) // Read-only list
val mutableList = mutableListOf(1, 2, 3) // Mutable list
val set = setOf(1, 2, 3) // Set
val map = mapOf("key" to "value") // Map
```

## Elvis Operator (`?:`) in Kotlin

The Elvis operator is used to return a default value if the expression on the left is `null`.

```kotlin
val name: String? = null
val length = name?.length ?: 0
println(length) // Output: 0
```




# Kotlin Coroutines Guide for Android Interviews

## 1. Coroutines

Coroutines are a lightweight concurrency design pattern in Kotlin for asynchronous programming. They allow you to write asynchronous code in a sequential manner, making it easier to read and maintain.

Example:
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    launch {
        delay(1000L)
        println("World!")
    }
    println("Hello")
}
```

Output:
```
Hello
World!
```

## 2. Suspend

The `suspend` keyword is used to mark functions that can be paused and resumed. These functions can only be called from within a coroutine or another suspend function.

Example:
```kotlin
suspend fun fetchUserData(): String {
    delay(1000L) // Simulate network delay
    return "User Data"
}

fun main() = runBlocking {
    val userData = fetchUserData()
    println(userData)
}
```

## 3. Launch, Async-Await, WithContext

### Launch
`launch` is a coroutine builder that launches a new coroutine without returning the result.

Example:
```kotlin
fun main() = runBlocking {
    launch {
        delay(1000L)
        println("Task from launch")
    }
    println("Main task")
}
```

### Async-Await
`async` starts a new coroutine and returns a `Deferred` object, which can be used to get the result using `await()`.

Example:
```kotlin
fun main() = runBlocking {
    val deferred = async {
        delay(1000L)
        "Async result"
    }
    println("Processing...")
    println(deferred.await())
}
```

### WithContext
`withContext` is used to switch the context of a coroutine. It's often used to switch between dispatchers.

Example:
```kotlin
fun main() = runBlocking {
    val result = withContext(Dispatchers.Default) {
        // Compute intensive task
        "Result from withContext"
    }
    println(result)
}
```

## 4. Dispatchers

Dispatchers determine which thread or threads the corresponding coroutine uses for its execution. Kotlin provides several dispatchers:

- `Dispatchers.Main`: For Android main thread operations
- `Dispatchers.IO`: For I/O operations (network, disk)
- `Dispatchers.Default`: For CPU-intensive tasks
- `Dispatchers.Unconfined`: Not confined to any specific thread

Example:
```kotlin
fun main() = runBlocking {
    launch(Dispatchers.Default) {
        println("Running on ${Thread.currentThread().name}")
    }
}
```

## 5. Scope, Context, Job

### Scope
A `CoroutineScope` defines the lifecycle of coroutines. It ensures that no coroutines are leaked.

### Context
`CoroutineContext` is a set of elements that define the behavior of a coroutine, including its dispatcher and job.

### Job
A `Job` is a handle to a coroutine. It can be used to manage the coroutine's lifecycle.

Example:
```kotlin
fun main() = runBlocking {
    val job = launch {
        delay(1000L)
        println("Job completed")
    }
    job.join() // Wait for the job to complete
}
```

## 6. LifecycleScope, ViewModelScope, GlobalScope

### LifecycleScope
`lifecycleScope` is an extension property available on `LifecycleOwner` objects. Coroutines launched in this scope are cancelled when the `Lifecycle` is destroyed.

Example:
```kotlin
class MyFragment : Fragment() {
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        viewLifecycleOwner.lifecycleScope.launch {
            // Coroutine that will be canceled when the Fragment's view is destroyed
        }
    }
}
```

### ViewModelScope
`viewModelScope` is an extension property available on `ViewModel` objects. Coroutines launched in this scope are cancelled when the `ViewModel` is cleared.

Example:
```kotlin
class MyViewModel : ViewModel() {
    fun loadData() {
        viewModelScope.launch {
            // Coroutine that will be canceled when the ViewModel is cleared
        }
    }
}
```

### GlobalScope
`GlobalScope` is used to launch top-level coroutines which are operating on the whole application lifetime. Use it sparingly, as it may lead to resource leaks.

Example:
```kotlin
GlobalScope.launch {
    // Long-running task
}
```

## 7. SuspendCoroutine, SuspendCancellableCoroutine

These functions are used to wrap callback-based APIs into suspend functions.

### SuspendCoroutine
Used when the operation cannot be cancelled.

Example:
```kotlin
suspend fun fetchData(): String = suspendCoroutine { continuation ->
    someAsyncOperation { result ->
        continuation.resume(result)
    }
}
```

### SuspendCancellableCoroutine
Used when the operation can be cancelled.

Example:
```kotlin
suspend fun fetchDataCancellable(): String = suspendCancellableCoroutine { continuation ->
    val job = someAsyncOperation { result ->
        continuation.resume(result)
    }
    continuation.invokeOnCancellation {
        job.cancel()
    }
}
```

## 8. CoroutineScope, SupervisorScope

### CoroutineScope
`coroutineScope` is a suspend function that creates a new scope and doesn't complete until all launched children have completed.

Example:
```kotlin
suspend fun doWork() = coroutineScope {
    launch {
        delay(500L)
        println("Task 1")
    }
    launch {
        delay(1000L)
        println("Task 2")
    }
}
```

### SupervisorScope
`supervisorScope` is similar to `coroutineScope`, but it doesn't cancel other children when one child fails.

Example:
```kotlin
suspend fun doWorkWithSupervisor() = supervisorScope {
    launch {
        delay(500L)
        throw Exception("Task 1 failed")
    }
    launch {
        delay(1000L)
        println("Task 2 completed")
    }
}
```








# Kotlin Flow API for Android Interview

## Flow Basics

### Flow Builder

# Kotlin Flow Builders

In Kotlin, `Flow` builders are functions that create instances of `Flow`. Here’s a comprehensive list of the main `Flow` builders along with their explanations:

## 1. `flow`

The `flow` builder is the most commonly used builder. It allows you to create a `Flow` by emitting values in a sequential manner. You use a `suspend` lambda to emit values and handle asynchronous operations.

**Example:**

```kotlin
import kotlinx.coroutines.flow.*
import kotlinx.coroutines.*

fun simpleFlow(): Flow<Int> = flow {
    for (i in 1..3) {
        delay(1000) // Simulate some work
        emit(i) // Emit next value
    }
}
```

## 2. `flowOf`

The `flowOf` builder creates a `Flow` from a fixed set of values. It’s a convenient way to create a `Flow` with known values.

**Example:**

```kotlin
val numbersFlow: Flow<Int> = flowOf(1, 2, 3, 4, 5)
```

## 3. `asFlow`

The `asFlow` extension function converts various types of collections and sequences into a `Flow`.

**Example:**

```kotlin
import kotlinx.coroutines.flow.*

val list = listOf(1, 2, 3, 4, 5)
val listFlow: Flow<Int> = list.asFlow()
```

## 4. `callbackFlow`

The `callbackFlow` builder allows you to create a `Flow` from a callback-based API. It enables the flow to emit values based on asynchronous callback invocations.

**Example:**

```kotlin
import kotlinx.coroutines.flow.*

fun fetchDataFlow(): Flow<Int> = callbackFlow {
    val callback = object : Callback {
        override fun onResult(result: Int) {
            trySend(result).isSuccess
        }
    }

    fetchData(callback) // Start the data fetching process

    awaitClose { 
        // Cleanup if necessary
    }
}
```

## 5. `channelFlow`

The `channelFlow` builder is used to create a `Flow` that can emit values from multiple coroutines. It is useful when you need to handle complex scenarios involving channels and concurrent operations.

**Example:**

```kotlin
import kotlinx.coroutines.flow.*
import kotlinx.coroutines.*

fun combinedDataFlow(): Flow<Int> = channelFlow {
    launch {
        send(fetchFromSource1())
    }
    
    launch {
        send(fetchFromSource2())
    }
}
```

## 6. `flowOf` with vararg

`flowOf` can also be used with a `vararg` parameter, allowing you to create a flow with a variable number of elements.

**Example:**

```kotlin
val flow = flowOf(1, 2, 3)
```

## 7. `emitAll`

Although not a standalone builder, `emitAll` is used within a flow builder to emit all values from another flow.

**Example:**

```kotlin
import kotlinx.coroutines.flow.*
import kotlinx.coroutines.*

fun mergeFlows(): Flow<Int> = flow {
    emitAll(flowOf(1, 2, 3))
    emitAll(flowOf(4, 5, 6))
}
```

## Summary

- **`flow`**: General-purpose flow builder for creating a flow from scratch.
- **`flowOf`**: Creates a flow from a fixed set of values.
- **`asFlow`**: Converts collections or sequences into a flow.
- **`callbackFlow`**: Creates a flow from a callback-based API.
- **`channelFlow`**: Creates a flow that can emit values from multiple coroutines.
- **`emitAll`**: Used within a flow to emit all values from another flow.

These builders provide various ways to create and work with flows in Kotlin, allowing you to handle different asynchronous and concurrent scenarios effectively.

# `flowOn` and `Dispatchers` in Kotlin Flow

In Kotlin Flow, `flowOn` and `Dispatchers` are used to control the context in which flow operations run. They help manage the threading and execution of coroutines.

## `flowOn`

The `flowOn` operator changes the context in which the upstream flow is executed. It allows you to specify a dispatcher for the `Flow`'s upstream operations.

**Usage:**

- `flowOn` is used to shift the context for the upstream operations (i.e., the part of the flow before the `flowOn` operator).
- This operator does not affect the context of the downstream operations.

**Example:**

```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

fun performWork(): Flow<Int> = flow {
    emit(1) // Emitting value
    delay(1000) // Simulate work
    emit(2)
}
.flowOn(Dispatchers.IO) // Change context for the upstream operations

fun main() = runBlocking {
    performWork()
        .collect { value -> println("Received: $value") }
}


### Operator

Operators transform or manipulate the emitted values from a `Flow`.

#### `filter`

Filters emitted values based on a predicate.

```kotlin
simpleFlow()
    .filter { it % 2 == 1 } // Only odd numbers
    .collect { value -> println(value) }
```

#### `map`

Transforms each value emitted by the `Flow`.

```kotlin
simpleFlow()
    .map { it * 2 } // Double each value
    .collect { value -> println(value) }
```

#### `zip`

Combines values from two flows into a single flow.

```kotlin
val flow1 = flowOf(1, 2, 3)
val flow2 = flowOf("A", "B", "C")

flow1.zip(flow2) { a, b -> "$a$b" }
    .collect { value -> println(value) } // Outputs: 1A, 2B, 3C
```

#### `flatMapConcat`

Flattens values from multiple flows into a single flow, preserving order.

```kotlin
val flow1 = flowOf("A", "B")
val flow2 = flowOf("1", "2")

flow1.flatMapConcat { a ->
    flow2.map { b -> "$a$b" }
}
.collect { value -> println(value) } // Outputs: A1, A2, B1, B2
```

#### `retry`

Retries the flow on failure.

```kotlin
flow {
    emit(1)
    throw RuntimeException("Error")
}
.retry(3) // Retry up to 3 times
.collect { value -> println(value) }
```

#### `debounce`

Only emits the most recent value if no new values are emitted within the specified time period.

```kotlin
simpleFlow()
    .debounce(500) // Only emit if no new values within 500ms
    .collect { value -> println(value) }
```

#### `distinctUntilChanged`

Only emits values if they are different from the previous emitted value.

```kotlin
flowOf(1, 1, 2, 2, 3)
    .distinctUntilChanged()
    .collect { value -> println(value) } // Outputs: 1, 2, 3
```

#### `flatMapLatest`

Maps each value to a new flow and only collects from the latest flow.

```kotlin
val flow1 = flowOf(1, 2)
val flow2 = flowOf("A", "B")

flow1.flatMapLatest { _ ->
    flow2
}
.collect { value -> println(value) } // Outputs: A, B
```

## Terminal Operators

Terminal operators are used to collect or consume the values emitted by a `Flow`.

### `collect`

Collects values emitted by the `Flow`.

```kotlin
simpleFlow().collect { value -> println(value) }
```

### `toList`

Collects values into a `List`.

```kotlin
val list = simpleFlow().toList()
println(list) // Outputs: [1, 2, 3]
```

## Flow vs Hot Flow

### Cold Flow

Cold flows start emitting values only when they are collected. Each collector gets its own independent flow.

```kotlin
val coldFlow = flow {
    emit(1)
    delay(1000)
    emit(2)
}
```

### Hot Flow

Hot flows start emitting values regardless of whether there are collectors or not. All collectors share the same flow of data.

```kotlin
val hotFlow = MutableSharedFlow<Int>()

// Emit values regardless of collectors
hotFlow.emit(1)
```

## StateFlow and SharedFlow

### `StateFlow`

A state holder that provides the current value and emits updates. It always has a value and emits updates to all collectors.

```kotlin
val stateFlow = MutableStateFlow(0)

stateFlow.value = 1
stateFlow.collect { value -> println(value) }
```

### `SharedFlow`

A hot stream that emits values to multiple collectors but does not have a state. It can be configured with replay and extra buffer capacity.

```kotlin
val sharedFlow = MutableSharedFlow<Int>(replay = 1)

sharedFlow.emit(1)
sharedFlow.collect { value -> println(value) }
```

## `callbackFlow` and `channelFlow`

### `callbackFlow`

Creates a `Flow` from callbacks, providing a way to work with APIs that use callbacks.

```kotlin
val callbackFlow = callbackFlow {
    val listener = object : Callback {
        override fun onResult(result: Int) {
            trySend(result)
        }
    }
    addCallback(listener)
    awaitClose { removeCallback(listener) }
}
```

### `channelFlow`

Creates a `Flow` that can emit values from multiple coroutines and allows for more complex operations.

```kotlin
val channelFlow = channelFlow {
    launch {
        send(1)
        delay(1000)
        send(2)
    }
}
```

This covers the main concepts of Kotlin Flow API with examples. Understanding these topics will help you navigate Kotlin's Flow API effectively in your Android development work.
```

