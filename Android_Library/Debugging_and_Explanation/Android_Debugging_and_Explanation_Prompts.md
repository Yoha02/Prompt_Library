# Android Debugging and Explanation Prompts

This document contains a collection of prompts for debugging and explaining Android code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Explain a Complex Code Snippet](#explain-a-complex-code-snippet)
2. [Diagnose an ANR (Application Not Responding)](#diagnose-an-anr-application-not-responding)
3. [Interpret a Crash Log](#interpret-a-crash-log)
4. [Diagnose a Memory Leak](#diagnose-a-memory-leak)

---

## Explain a Complex Code Snippet

### Purpose

Get a clear, expert-level explanation of a piece of code, helping you understand its logic, identify hidden bugs, and learn best practices without having to ask a senior developer.

### Prompt

```
You are an expert Android developer and code reviewer.

Analyze the following Kotlin code snippet. Provide a clear, step-by-step explanation of its logic and purpose. Then, identify any potential issues or "code smells."

- Analysis: What is the code trying to accomplish? How does it do it?

- Potential Issues: Look for problems related to:
  - Concurrency: Improper use of Coroutine Dispatchers, blocking the main thread.
  - Memory: Potential memory leaks (e.g., leaking Context, un-disposed listeners).
  - Architecture: Violating MVVM/MVI principles (e.g., business logic in the UI layer).
  - Bugs: Logical errors, improper null handling, or race conditions.

- Suggestions: Recommend specific improvements to make the code more robust, readable, and performant.

Code to Analyze:
kotlin
// [PASTE THE COMPLEX or UNFAMILIAR KOTLIN CODE SNIPPET HERE]
```

**Notes:** This is incredibly useful when you inherit a new module or encounter a piece of legacy code that isn't well-documented. Providing context (e.g., "this is from a ViewModel") will yield better results.

---

## Diagnose an ANR (Application Not Responding)

### Purpose

Understand the root cause of a critical ANR freeze, pinpoint the exact problematic code from a system trace, and get an actionable plan to fix it using modern concurrency patterns.

### Prompt

```
You are an expert in Android application performance.

My app is experiencing an ANR (Application Not Responding) error in the [FEATURE_NAME] feature. I have the ANR trace from Logcat.

- Explain the Cause: Based on the stack trace, explain in simple terms what is blocking the main thread.

- Pinpoint the Code: Identify the exact class and method in my application code that is the source of the blockage.

- Provide a Solution: Recommend a specific, modern solution to fix the issue. For example:
  - "Move the network call [ApiService.fetchData()] into viewModelScope.launch(Dispatchers.IO)."
  - "Perform the complex for loop calculation on a background thread."
  - "Optimize the database query that is taking too long."

ANR Trace Log:

// [PASTE THE FULL ANR STACK TRACE FROM LOGCAT HERE]
```

**Notes:** The key to a good ANR diagnosis is the stack trace. The trace clearly shows what the main thread was doing (or waiting for) when it became unresponsive. Always provide the full trace.

---

## Interpret a Crash Log

### Purpose

Quickly decode a cryptic crash log to understand the precise cause of a bug and get an actionable solution, drastically reducing debugging time and improving app stability.

### Prompt

```
You are an expert Android debugger.

My app crashed, and I have the stack trace from my crash reporting tool. Analyze this crash log and explain the problem.

- Identify the Exception: Name the specific exception that occurred (e.g., NullPointerException, IllegalStateException, IndexOutOfBoundsException).

- Find the Root Cause: Pinpoint the exact line of code in the file [FILE_NAME.kt] that caused the crash and explain why it crashed (e.g., "The user object was null when you tried to access user.name").

- Suggest a Fix: Provide a robust code fix to prevent this crash. For example:
  - "Add a null check using a safe call (user?.name) or a let block."
  - "Ensure the list is not empty before trying to access an element at a specific index."

Crash Log Stack Trace:

// [PASTE THE FULL STACK TRACE FROM LOGCAT or a CRASH REPORTING TOOL HERE]
```

**Notes:** The most important part of the log is usually the "Caused by:" section. It points directly to the origin of the exception in our own codebase.

---

## Diagnose a Memory Leak

### Purpose

Identify and fix common memory leaks that can lead to poor performance and OutOfMemoryError crashes, ensuring the app remains stable and responsive over long user sessions.

### Prompt

```
You are an expert in Android memory management.

I suspect a memory leak in my [Activity/Fragment NAME]. After navigating away from this screen, the Android Studio Profiler shows its instance is not being garbage collected. Analyze the provided code for common causes of leaks.

- Check for Common Causes:
  - Static References: A static field holding a reference to a View or Context.
  - Anonymous Classes/Lambdas: An inner class or lambda holding an implicit reference to the outer Activity/Fragment.
  - Listeners/Callbacks: A system or singleton listener that was registered but never unregistered.

- Pinpoint the Leak: Identify the specific line of code that is causing the leak.

- Provide the Fix: Show how to resolve the leak (e.g., "Unregister the listener in onDestroyView()," "Use an ApplicationContext instead of an Activity context," "Clear the reference in onDestroy()," "Use a WeakReference").

Code with Potential Leak:
kotlin
// [PASTE THE CODE OF THE SUSPECTED LEAKING Activity/Fragment HERE]
```

**Notes:** Memory leaks are often subtle. This prompt acts as a second pair of eyes, systematically checking for the most frequent culprits that developers might overlook.
