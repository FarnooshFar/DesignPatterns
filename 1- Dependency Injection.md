# Dependency Injection in Kotlin Multiplatform (KMP)

## Introduction
Dependency Injection (DI) is a design pattern that promotes loose coupling by injecting dependencies from outside rather than creating them within a class. This enhances flexibility, testability, and maintainability.

## Why Use Dependency Injection?
- **Loose Coupling** – Reduces dependencies between classes.
- **Easier Testing** – Allows injecting mocks for unit testing.
- **Improved Maintainability** – Changes in dependencies don’t require modifications in dependent classes.
- **Increases Modularity** – Components can be replaced or modified easily.
- **Better Code Reusability** – Components can be used independently.

---
## Problem Solved by Dependency Injection
Without DI:
```kotlin
class UserRepository {
    private val apiService = ApiService() // Tight coupling
    fun getUserData() {
        apiService.fetchData()
    }
}
```
With DI:
```kotlin
class UserRepository(private val apiService: ApiService) {
    fun getUserData() {
        apiService.fetchData()
    }
}
```
---
## Types of Dependency Injection
### **1. Constructor Injection**
Dependencies are passed via the constructor.
```kotlin
class UserService(private val repository: UserRepository) {
    fun fetchUser() = repository.getUserData()
}
```
### **2. Property Injection**
Dependencies are injected as class properties.
```kotlin
class UserViewModel {
    lateinit var repository: UserRepository
}
```
### **3. Method Injection**
Dependencies are passed as method parameters.
```kotlin
class Logger {
    fun log(message: String, writer: Writer) {
        writer.write(message)
    }
}
```

---
## Comparison of DI Types
| DI Type              | Advantages                            | Disadvantages                     |
|----------------------|------------------------------------|----------------------------------|
| Constructor         | Strongly enforced, easy to test   | Can become complex for many dependencies |
| Property           | Flexible, reduces boilerplate     | Harder to test, less encapsulation |
| Method            | Best for temporary dependencies  | More boilerplate for frequent dependencies |

---
## Using Koin for Dependency Injection in KMP
### **1. Setup Koin in Gradle**
```kotlin
dependencies {
    implementation("io.insert-koin:koin-core:3.2.0")
}
```
### **2. Define Koin Module**
```kotlin
val appModule = module {
    single { ApiService() }
    single { UserRepository(get()) }
}
```
### **3. Start Koin and Inject Dependencies**
```kotlin
fun main() {
    startKoin {
        modules(appModule)
    }
    val userRepository: UserRepository = get()
}
```
---
## Alternative to Dependency Injection
If you don’t want to use a DI framework:
- **Service Locator** – A singleton provides dependencies.
- **Factory Pattern** – Objects are created using a factory.

---
## Pros and Cons of Dependency Injection
### **Pros**
- Loosely coupled code
- Easier testing with mocks
- Better maintainability and scalability
- Adheres to SOLID principles

### **Cons**
- Increased complexity
- More boilerplate code
- Overhead with DI frameworks

---
