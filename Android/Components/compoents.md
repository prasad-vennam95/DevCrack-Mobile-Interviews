# Android Components

Android applications are built using four main components:

1. **Activities**: Represent a single screen with a user interface. Example: Login screen.
2. **Services**: Run in the background to perform long-running operations. Example: Music playback.
3. **Broadcast Receivers**: Respond to system-wide broadcast announcements. Example: Battery low notification.
4. **Content Providers**: Manage shared app data. Example: Contacts app.

---

## Tricky Questions and Answers

### 1. **What is the difference between `Service` and `IntentService`?**
    - **Answer**: 
      - `Service` runs on the main thread, while `IntentService` runs on a background thread.
      - `IntentService` stops itself after completing the task, whereas `Service` needs to be stopped explicitly.

### 2. **How does the Android system manage the lifecycle of an Activity?**
    - **Answer**: The lifecycle is managed using methods like `onCreate()`, `onStart()`, `onResume()`, `onPause()`, `onStop()`, and `onDestroy()`. The system transitions between these states based on user interactions and system constraints.

### 3. **What is the purpose of a `ContentProvider`?**
    - **Answer**: It allows sharing of data between applications using a standard interface. For example, accessing contacts or media files.

### 4. **How do you handle configuration changes in Android?**
    - **Answer**: Use `onSaveInstanceState()` to save data and restore it in `onCreate()` or handle changes manually by overriding `onConfigurationChanged()`.

### 5. **What is the difference between `Implicit` and `Explicit` Intents?**
    - **Answer**: 
      - **Explicit Intent**: Specifies the exact component to start (e.g., `MainActivity`).
      - **Implicit Intent**: Declares a general action to be performed, allowing the system to choose the appropriate component.

### 6. **What is the role of `ViewModel` in Android?**
    - **Answer**: It stores and manages UI-related data in a lifecycle-conscious way, surviving configuration changes like screen rotations.

### 7. **How does Android handle background tasks efficiently?**
    - **Answer**: By using components like `WorkManager`, `JobScheduler`, and `Foreground Services` to manage tasks based on system resources and constraints.

### 8. **What are all the launch modes in Android?**
    - **Answer**: Android provides four launch modes for activities, defined in the `AndroidManifest.xml` or via `Intent` flags:
        1. **standard**: Default mode. A new instance of the activity is created every time it is launched.
          2. **singleTop**: If an instance of the activity is already at the top of the stack, no new instance is created; instead, the existing instance handles the intent.
          3. **singleTask**: A new task is created, and the activity becomes the root of the task. If an instance already exists, it is reused, and other activities in the task are cleared.
          4. **singleInstance**: Similar to `singleTask`, but the activity is the only one in the task. Other activities are launched in a separate task.
