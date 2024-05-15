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
