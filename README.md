# Android & Kotlin: Most Important Topics

## ANDROID
## Core Building Blocks or Fundamental Components:

- **Activity** - Represents a single screen with a user interface
- **Views** - UI components for creating the user interface
- **Intents** - Facilitate communication between different components or apps
- **Services** - Long running background process. or Execute background tasks without a UI
- **Content Providers** - Used to share data between the apps
- **Fragments** - A modular portion of the user interface within an activity
- **Android Manifest** - Contains essential metadata about the application

## Activity Lifecycle:
- **onCreate()**: Called when the activity is first created. This is where initialization occurs.
- **onStart()**: Called when the activity becomes visible to the user.
- **onResume()**: Called when the activity starts interacting with the user. This is typically where animations and other things that require CPU resources should be started.
- **onPause()**: Called when the activity is partially obscured by another activity. This is a good place to commit unsaved changes or pause ongoing processes.
- **onStop()**: Called when the activity is no longer visible to the user.
- **onDestroy()**: Called before the activity is destroyed. This is where you should release any resources that aren't needed anymore.
- **OnRestart()**: Called when the activity has been stopped and is restarting again.

## Fragment Lifecycle:
 * Fragments are reusable UI components within activities. They have their own lifecycle methods similar to activities
- **onAttach()**: Attaches the fragment to its hosting activity.
- **onCreate()**: Initializes the fragment.
- **onCreateView()**: Creates the fragment's UI.
- **onViewCreated()**: Called after onCreateView() to initialize UI components.
- **onActivityCreated()**: Activity's onCreate() has completed; fragment's activity is fully initialized.
- **onStart()**: Fragment becomes visible.
- **onResume()**: Fragment starts interacting with the user.
- **onPause()**: Fragment no longer interacts with the user.
- **onStop()**: Fragment is no longer visible.
- **onDestroyView()**: Removes the fragment's UI.
- **onDestroy()**: Releases resources before the fragment is destroyed.
- **onDetach()**: Detaches the fragment from its hosting activity.

## Jetpack Components:
- **ViewModel**: Part of the Android Architecture Components. It is used to store and manage UI-related data in a lifecycle-aware manner, surviving configuration changes such as screen rotations.
- **LiveData**: An observable data holder class that notifies UI components when data changes. It’s lifecycle-aware, meaning it only updates active observers.
- **Navigation Component**: Simplifies the implementation of navigation between screens and supports features like deep linking and safe arguments.
- **Paging**: A component that allows users to load and display large data sets with infinite scrolling
- **Jetpack Compose**: A Kotlin-based toolkit for building native UI
- **Android KTX**: A library that increases support for the Kotlin language for app development 
- **WorkManager**: Used for background tasks that need guaranteed execution, such as periodic data syncing.
- **Room**: An abstraction layer over SQLite that handles database creation and management with type-safe access to database queries.
- **ViewBinding and DataBinding:** ViewBinding is a simpler approach for binding views, while DataBinding allows more complex UI bindings, supporting data binding expressions in XML layouts.

## RecyclerView
- A more advanced and flexible version of ListView, used to display a large number of items efficiently.
  Adapter and ViewHolder patterns are key concepts for recycling views and improving performance.
  DiffUtil: Used for calculating the difference between two lists and updating only the items that have changed.

## Networking
- Retrofit: A type-safe HTTP client for Android used for making network requests and parsing responses using converters like Gson or Moshi.
OkHttp: A powerful HTTP client that supports features like interceptors for handling custom headers and logging.
Handling errors (e.g., network failures, HTTP status codes) and using try-catch or custom error handling mechanisms.

## Data Storage:
- SharedPreferences: Simple key-value storage for saving small amounts of primitive data.
- Room Database: Structured storage using SQL with support for complex queries.
- SQLite: A database option for more manual management of structured data.

## Dependency Injection:

- Dagger 2: A compile-time dependency injection framework providing dependency management and injection with minimal runtime overhead.
- Hilt: A simpler way to integrate Dagger 2, making it easier to set up and use in Android projects.
- Koin: A lightweight dependency injection library for Kotlin that’s easy to learn and integrate.

## Multithreading and Background Work:

- Handler and Looper: Used for communicating between background threads and the main thread.
- WorkManager: Manages background tasks that should run even if the app is closed or the device is rebooted.
- Coroutines provide a modern approach to handle background work more efficiently compared to older methods like AsyncTask.
    
## Android Context Two types
- 1.Application Context - need to access resources that are not tied to any specific activity, use the Application context.
- 2.Activity Context - need to access resources that are tied to a specific activity, use the Activity context
- It allows us to access resources.
- It allows us to interact with other Android components by sending messages.
- It gives you information about your app environment.

## Image Loading libraries
- Picasso
- Glide
- Fresco
- COIL (Coroutine Image Loader)
- UIL (Universal Image Loader)

## Kotlin 
    Kotlin is a modern cross platform programming language. introduced by jetbrain-11
## kotlin coroutines
- Coroutines are lightweight threads that allow us to execute concurrent code without blocking threads
- it's essential to avoid blocking the main thread
- A coroutine is a concurrency design pattern that you can use on Android to simplify code that executes asynchronously
- Kotlin provides three basic building blocks
    - launch, async and runBlocking
- launch: is used to fire and forgot coroutine.

  ```kotlin
          import kotlinx.coroutines.*
          fun main() {
            GlobalScope.launch { 
                delay(1000L) 
                println("Hello from Coroutine!")
            }
            println("Hello from Main Thread!")
            Thread.sleep(2000L)
          }
  ```
 - async is used when you need a result computed in a coroutine.
 ```kotlin
    import kotlinx.coroutines.*
    fun main() {
    GlobalScope.launch {
        val result = async { 
            computeResult() 
        }
        println("Computed result: ${result.await()}")
    }
    Thread.sleep(2000L)
    }
    suspend fun computeResult(): Int {
    delay(1000L)
    return 42
    }
 ```
- runBlocking is a bridge between non-coroutine world and coroutine world.
-  ```kotlin
   import kotlinx.coroutines.*

    fun main() = runBlocking { 
    launch { 
        delay(1000L) 
        println("Hello from Coroutine!")
    }
    println("Hello from Main Thread!")
    }
   In this code, we’re starting a main coroutine using runBlocking, and inside this coroutine, we're launching a new coroutine.
   
- Coroutine Context and Dispatchers
- Every coroutine in Kotlin has a context associated with it, which is a set of various elements. The key elements in this set are Job of the coroutine and its dispatcher.
- Dispatchers.Main — for UI-related tasks.
- Dispatchers.IO — for input/output tasks, like reading or writing from/to a database, making network calls, or reading/writing files.
- Dispatchers.Default — for CPU-intensive tasks, like sorting large lists or doing complex computations.
  ``` kotlin
  import kotlinx.coroutines.*
    fun main() = runBlocking {
    launch(Dispatchers.IO) { 
        println("IO: ${Thread.currentThread().name}")
    }
    launch(Dispatchers.Default) { 
        println("Default: ${Thread.currentThread().name}")
    }
    launch(Dispatchers.Main) { 
        println("Main: ${Thread.currentThread().name}")
    }
    }

- There are basically 3 scopes in Kotlin coroutines:
- 1.Global Scope.
- 2.LifeCycle Scope.
- 3.ViewModel Scope

## Kotlin acesding order using for loops
``` kotlin
fun main(){
    val numbers = listOf(20, 18, 7, 10, 3, -12, 2, 1, -11, 15, -10, -5, -1, -19)
    val sortedNumbers = sortnumber(numbers)
    println(sortedNumbers)
}

fun sortnumber (numbers: List<Int>): List<Int>{
    val mutableNumbers = numbers.toMutableList()
    val n = mutableNumbers.size
    for (i in 0 until n -1 ){
       for (j in 0 until n - i - 1 ) {
           if (mutableNumbers[j] > mutableNumbers[j+1]){
               val temp = mutableNumbers[j]
              mutableNumbers[j] = mutableNumbers[j+1]
              mutableNumbers[j +1] = temp
           }
       }
    }
    return mutableNumbers
}

```
## Remove Vowel in the string
``` kotlin
fun main() {
   var string = "Welcome to Parthibhan!.."
    val result = removeVowels(string)
    println(result)
}
fun removeVowels(string: String): String{   
    val vowels = "aeiouAEIOU"
    return string.filter{
        char-> char !in vowels
    }
}
```

