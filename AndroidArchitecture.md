# Android Architecture

## Describe the Architecture of Your Last App

### RealisTix Architecture

The architecture of my last app, RealisTix, follows the **MVVM (Model-View-ViewModel)** pattern. Here's a brief overview:

- **Model**: Manages the data layer of the application. It includes data sources such as Firebase, repositories, and data models.
- **View**: Displays data and handles user interactions. In RealisTix, this includes various Compose UI components.
- **ViewModel**: Manages UI-related data in a lifecycle-conscious way. It interacts with the Model to fetch and process data, and exposes this data to the View.

The app uses **Jetpack Compose** for the UI, **Koin** for dependency injection, and **Firebase** for backend services.

## Describe MVVM

### MVVM Architecture

**MVVM (Model-View-ViewModel)** is an architectural pattern that separates the concerns of an application:

- **Model**: Represents the data and business logic of the application. It includes data sources, repositories, and domain models.
- **View**: Represents the UI components and displays the data. It binds to the ViewModel to get data and handle user interactions.
- **ViewModel**: Acts as a bridge between the Model and the View. It manages the UI-related data and exposes it to the View. It handles data operations and interacts with the Model.

## MVC vs MVP vs MVVM Architecture

### MVC (Model-View-Controller)

- **Model**: Manages the data and business logic.
- **View**: Displays the data and handles user interactions.
- **Controller**: Handles user input and updates the Model and View.

**Pros**:
- Simple and easy to understand.
- Good for small applications.

**Cons**:
- Can lead to tightly coupled code.
- Controller can become a god object if not managed properly.

### MVP (Model-View-Presenter)

- **Model**: Manages data and business logic.
- **View**: Displays the data and handles user interactions.
- **Presenter**: Acts as an intermediary between the Model and View. It handles user actions and updates the Model and View.

**Pros**:
- Separation of concerns is clearer than MVC.
- Easier to unit test the Presenter.

**Cons**:
- More boilerplate code compared to MVC.
- Can lead to multiple Presenters if not managed properly.

### MVVM (Model-View-ViewModel)

- **Model**: Manages data and business logic.
- **View**: Displays data and handles user interactions.
- **ViewModel**: Manages UI-related data and business logic. It interacts with the Model and exposes data to the View.

**Pros**:
- Clear separation of concerns.
- Better support for data binding and reactive programming.

**Cons**:
- Requires understanding of data binding and LiveData/StateFlow.
- Can lead to complex ViewModels for large apps.

## Clean Architecture

**Clean Architecture** is a design pattern that emphasizes separation of concerns and independence of components. It consists of the following layers:

- **Entities**: Core business logic and domain entities.
- **Use Cases**: Application-specific business rules.
- **Interface Adapters**: Adapters that convert data between the Use Cases and the external interfaces (e.g., UI, database).
- **Frameworks and Drivers**: External components such as databases, UI frameworks, and network services.

**Pros**:
- Promotes separation of concerns.
- Easier to maintain and test.
- Provides flexibility to change frameworks or tools.

**Cons**:
- Can be complex to implement.
- May introduce boilerplate code.

## Software Architecture vs Software Design

### Software Architecture

**Software Architecture** refers to the high-level structure of a software system. It defines the components, their interactions, and the overall design principles. It focuses on scalability, performance, and maintainability.

### Software Design

**Software Design** involves detailed planning and implementation of software components. It focuses on the detailed structure and behavior of individual components and how they interact within the architecture.

**Key Differences**:
- Architecture is concerned with high-level structure, while design focuses on low-level details.
- Architecture decisions impact the overall system, while design decisions affect individual components.

# Android System Design

## Design an Image Loading Library

### Key Features:

- **Image Caching**: Efficiently cache images in memory and disk.
- **Asynchronous Loading**: Load images asynchronously to avoid blocking the UI thread.
- **Placeholders and Error Handling**: Show placeholders while loading and handle errors gracefully.

### Components:

- **Image Loader**: Manages the loading and caching of images.
- **Image Cache**: Stores images in memory and disk.
- **Image Decoder**: Decodes image data into displayable formats.

## Design File Downloader Library

### Key Features:

- **Progress Tracking**: Track download progress and provide feedback to users.
- **Retry Mechanism**: Handle download failures and retry if necessary.
- **Background Downloads**: Support background downloads and notifications.

### Components:

- **Download Manager**: Manages the download process.
- **Progress Tracker**: Monitors and reports download progress.
- **Retry Handler**: Manages retry logic for failed downloads.

## Design WhatsApp

### Key Features:

- **Real-time Messaging**: Support real-time text, audio, and video messaging.
- **Media Sharing**: Allow users to share images, videos, and documents.
- **User Presence**: Show user online/offline status and typing indicators.

### Components:

- **Messaging Service**: Handles message sending and receiving.
- **Media Service**: Manages media uploads and downloads.
- **User Service**: Manages user profiles and presence information.

## Design Instagram Stories

### Key Features:

- **Media Upload**: Allow users to upload images and videos.
- **Stories Display**: Display a sequence of stories in a feed.
- **Story Expiry**: Automatically remove stories after a certain period.

### Components:

- **Story Manager**: Handles story creation and expiry.
- **Media Service**: Manages media uploads and retrieval.
- **Feed Display**: Displays stories in a user-friendly format.

## Design Networking Library

### Key Features:

- **Request Management**: Handle HTTP requests and responses.
- **Error Handling**: Manage network errors and retries.
- **Caching**: Cache network responses to improve performance.

### Components:

- **Network Client**: Handles HTTP requests and responses.
- **Cache Manager**: Manages cached responses.
- **Error Handler**: Handles network errors and retries.

## Design Facebook Near-By Friends App

### Key Features:

- **Location Tracking**: Track and update user locations.
- **Proximity Detection**: Detect and display nearby friends.
- **Privacy Controls**: Allow users to control who can see their location.

### Components:

- **Location Service**: Manages location updates and tracking.
- **Proximity Service**: Detects and displays nearby friends.
- **Privacy Manager**: Manages user privacy settings.

## Design Caching Library

### Key Features:

- **In-Memory Cache**: Store frequently accessed data in memory.
- **Disk Cache**: Persist cache data on disk for offline use.
- **Cache Expiry**: Implement cache expiration policies.

### Components:

- **Cache Manager**: Manages in-memory and disk caches.
- **Cache Expiry**: Handles cache expiration and eviction.
- **Cache Store**: Stores and retrieves cached data.

## Design Problems Based on Location-Based App

### Key Features:

- **Location Tracking**: Continuously track user location.
- **Geofencing**: Trigger actions based on location boundaries.
- **Offline Support**: Handle location data offline.

### Components:

- **Location Service**: Manages location tracking and updates.
- **Geofencing Service**: Handles geofencing and location-based triggers.
- **Offline Storage**: Manages offline storage of location data.

## How to Build an Offline-First App? Explain the Architecture

### Key Features:

- **Local Data Storage**: Store data locally for offline access.
- **Sync Mechanism**: Sync local data with a remote server when online.
- **User Feedback**: Provide feedback when offline actions are performed.

### Architecture:

1. **Local Data Layer**: Manages local data storage (e.g., SQLite, Room).
2. **Sync Manager**: Handles data synchronization with the remote server.
3. **Repository**: Manages data access from local and remote sources.
4. **ViewModel**: Provides data to the UI and manages UI-related data.

## Design LRU Cache

### Key Features:

- **Least Recently Used**: Evict the least recently used items when the cache reaches its limit.
- **Efficient Access**: Provide fast access to cached items.
- **Size Management**: Manage the size of the cache.

### Components:

- **Cache Store**: Stores cached items.
- **Eviction Policy**: Implements the LRU eviction policy.
- **Access Mechanism**: Provides efficient access to cached items.

## Design Analytics Library

### Key Features:

- **Event Tracking**: Track and record user events and interactions.
- **Data Aggregation**: Aggregate and process collected data.
- **Reporting**: Generate reports and insights from analytics data.

### Components:

- **Event Tracker**: Records user events and interactions.
- **Data Processor**: Aggregates and processes analytics data.
- **Report Generator**: Generates reports and visualizations.

## HTTP Request vs HTTP Long-Polling vs WebSockets

### HTTP Request

- **Description**: A standard HTTP request-response model.
- **Pros**: Simple and widely supported.
- **Cons**: Not suitable for real-time applications

.

### HTTP Long-Polling

- **Description**: Keeps an HTTP connection open until new data is available.
- **Pros**: Provides near real-time updates.
- **Cons**: More resource-intensive than standard HTTP requests.

### WebSockets

- **Description**: A persistent connection allowing bi-directional communication.
- **Pros**: Provides real-time, low-latency updates.
- **Cons**: More complex to implement and manage.

## How Do Voice and Video Calls Work?

### Voice and Video Calls

- **Voice Calls**: Use codecs to compress and transmit audio data in real-time.
- **Video Calls**: Use codecs to compress and transmit video and audio data.
- **Protocols**: Commonly use protocols like SIP (Session Initiation Protocol) and WebRTC (Web Real-Time Communication).

## Design Uber App

### Key Features:

- **Ride Request**: Allow users to request rides and view available drivers.
- **Real-Time Tracking**: Track rides and display driver locations in real-time.
- **Payment Integration**: Handle payments and provide receipts.

### Components:

- **Ride Manager**: Handles ride requests and driver assignments.
- **Tracking Service**: Provides real-time tracking of rides and drivers.
- **Payment Gateway**: Manages payments and transactions.

## Database Normalization vs Denormalization

### Normalization

- **Description**: Process of organizing data to reduce redundancy and improve data integrity.
- **Pros**: Reduces data duplication and improves data consistency.
- **Cons**: Can lead to complex queries and reduced performance.

### Denormalization

- **Description**: Process of adding redundant data to improve query performance.
- **Pros**: Simplifies queries and improves performance.
- **Cons**: Increases data redundancy and complexity in data management.

## Hash vs Encrypt vs Encode

### Hash

- **Description**: Converts data into a fixed-size hash value (e.g., MD5, SHA).
- **Use Case**: Data integrity checks and password storage.
- **Pros**: Fast and efficient.
- **Cons**: Not reversible.

### Encrypt

- **Description**: Converts data into a secure format using encryption algorithms (e.g., AES).
- **Use Case**: Data protection and confidentiality.
- **Pros**: Reversible with the correct key.
- **Cons**: Requires key management.

### Encode

- **Description**: Converts data into a specific format (e.g., Base64).
- **Use Case**: Data serialization and transmission.
- **Pros**: Reversible and simple.
- **Cons**: Not intended for security purposes.

# Android Unit Testing

## Unit Testing ViewModel with Kotlin Coroutines and LiveData

### ViewModel with Kotlin Coroutines and LiveData

- **Test**: Use `LiveData` and coroutines to test ViewModel logic.
- **Libraries**: Use `JUnit`, `Mockito`, and `Coroutines Test` libraries.
- **Example**:

```kotlin
@Test
fun testViewModelWithCoroutines() = runBlockingTest {
    // Arrange
    val viewModel = MyViewModel()
    // Act
    viewModel.someFunction()
    // Assert
    assertEquals(expected, viewModel.liveData.value)
}
```

## Unit Testing ViewModel with Kotlin Flow and StateFlow

### ViewModel with Kotlin Flow and StateFlow

- **Test**: Use `Flow` and `StateFlow` to test ViewModel logic.
- **Libraries**: Use `JUnit`, `Mockito`, and `Kotlin Flow Test` libraries.
- **Example**:

```kotlin
@Test
fun testViewModelWithFlow() = runBlockingTest {
    // Arrange
    val viewModel = MyViewModel()
    // Act
    viewModel.someFunction()
    // Assert
    assertEquals(expected, viewModel.stateFlow.value)
}
```

## What is Espresso?

**Espresso** is a testing framework for Android UI testing. It allows you to write reliable and efficient UI tests by providing APIs to interact with and assert the state of UI components.

## What is Robolectric?

**Robolectric** is a testing framework that allows you to run Android tests on the JVM, bypassing the need for an emulator or physical device. It provides shadow objects to simulate Android framework classes.

## What are the Disadvantages of Using Robolectric?

- **Limited Support**: May not support all Android features or latest API changes.
- **Performance**: Can be slower compared to real device testing.
- **Accuracy**: Tests may not always reflect real-world behavior accurately.

## What is UI-Automator?

**UI-Automator** is a testing framework for Android that provides APIs to interact with and test UI components across multiple apps. It is used for UI testing on real devices.

## Explain Unit Test

**Unit Test**: A unit test focuses on testing individual components or functions of the codebase in isolation. It ensures that each component behaves as expected and adheres to its design specifications.

## Explain Instrumented Test

**Instrumented Test**: An instrumented test runs on an Android device or emulator and interacts with the Android framework. It is used to test interactions between components and the behavior of the application in a real environment.

## Why Mockito is Used?

**Mockito** is a mocking framework used for unit testing in Java. It allows you to create mock objects and define their behavior, making it easier to isolate and test individual components.

## Describe Code Coverage

**Code Coverage** measures the percentage of code that is executed during testing. It helps identify untested parts of the codebase and ensure that tests cover critical areas.

# Android Tools and Technologies

## What is ADB?

**ADB (Android Debug Bridge)** is a command-line tool used for interacting with Android devices. It allows you to perform actions like installing and debugging apps, running shell commands, and accessing device logs.

## What is the StrictMode?

**StrictMode** is a tool for detecting and diagnosing performance issues in Android applications. It helps identify potential problems like disk access on the main thread, unclosed resources, and more.

## What is Lint? What is it Used For?

**Lint** is a static analysis tool for detecting potential bugs and performance issues in Android code. It helps identify code smells, deprecated API usage, and other issues that could affect the quality of the application.

## Git

**Git** is a distributed version control system used for tracking changes in source code. It allows multiple developers to collaborate on a project, manage branches, and maintain a history of changes.

## Firebase

**Firebase** is a mobile and web application development platform by Google. It provides tools and services for building, managing, and analyzing applications, including real-time databases, authentication, analytics, and cloud functions.

## How to Measure Method Execution Time in Android?

Use `System.currentTimeMillis()` or `System.nanoTime()` to measure the execution time of a method:

```kotlin
val startTime = System.currentTimeMillis()
// Method execution
val endTime = System.currentTimeMillis()
val executionTime = endTime - startTime
```

## Can You Access Your SQLite Database for Debugging?

Yes, you can access and debug your SQLite database using Android Studio's Database Inspector. It allows you to view and interact with the database schema and data in real-time.

## What Are Things That We Need to Take Care While Using Proguard?

- **Configuration**: Properly configure ProGuard rules to avoid stripping essential code.
- **Obfuscation**: Be aware of the impact on code readability and debugging.
- **Testing**: Thoroughly test the application after applying ProGuard to ensure no functionality is broken.

## How to Use Android Studio Memory Profiler?

- **Open Profiler**: Navigate to `View > Tool Windows > Profiler`.
- **Select App**: Choose the app to profile.
- **Analyze Memory**: Use the Memory Profiler to monitor memory usage, identify leaks, and analyze heap dumps.

## What is Gradle?

**Gradle** is a build automation tool used for compiling, testing, and packaging Android applications. It supports custom build configurations and dependencies.

## APK Size Reduction

- **Optimize Images**: Use tools like PNGCrunch or WebP.
- **Remove Unused Resources**: Use ProGuard to strip out unused code and resources.
- **Split APKs**: Generate APKs for different screen densities and architectures.

## How Can You Speed Up the Gradle Build?

- **Use Gradle Daemon**: Enable Gradle Daemon for faster builds.
- **Parallel Builds**: Enable parallel builds in `gradle.properties`.
- **Configure Build Caches**: Use build caches to reuse previously built outputs.

## About Gradle Build System

**Gradle** is the build system used by Android Studio to manage project dependencies, compile code, and package APKs. It provides flexibility and configurability for building Android apps.

## About Multiple APKs for Android Application

**Multiple APKs**: Generate different APKs for various device configurations (e.g., screen density, CPU architecture). This allows you to optimize APK size and ensure compatibility with different devices.

## What is ProGuard Used For?

**ProGuard** is a code shrinker and obfuscator used to minimize and protect Android code. It reduces the size of the APK and makes reverse engineering more difficult.

## What is Obfuscation? What is it Used For? What About Minification?

- **Obfuscation**: The process of making code difficult to read and understand. It is used to protect code from reverse engineering.
- **Minification**: The process of removing unnecessary code and reducing file size. It helps in optimizing the application for better performance.

## How to Change Some Parameters in an App Without an App Update?

- **Remote Configuration**: Use Firebase Remote Config to update parameters remotely.
- **Server-Based Configuration**: Store configuration parameters on a server and fetch them dynamically

 in the app.

