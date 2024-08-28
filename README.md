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

This guide covers the main topics related to Kotlin Coroutines that are important for Android interviews. Remember to practice implementing these concepts in real Android projects to gain a deeper understanding.
