# Design Patterns in Kotlin Multiplatform (KMP)

## Introduction
Design patterns provide reusable solutions to common software design problems. In Kotlin Multiplatform (KMP), patterns must be adaptable across platforms while ensuring platform-specific concerns are handled properly.

## Types of Design Patterns
1. **Creational Patterns** - Manage object creation.
2. **Structural Patterns** - Define object composition.
3. **Behavioral Patterns** - Manage object interactions.
4. **Concurrency Patterns** - Handle async and multi-threading.
5. **Dependency Injection** - Manage dependencies efficiently.

---
## 1. Creational Patterns
### **Singleton Pattern**
Ensures a single instance across platforms.
```kotlin
object AppConfig {
    val baseUrl: String = "https://api.example.com"
}
```
### **Factory Method Pattern**
Encapsulates object creation logic.
```kotlin
interface Logger {
    fun log(message: String)
}

expect class LoggerFactory() {
    fun createLogger(): Logger
}
```
### **Builder Pattern**
Used for constructing complex objects step by step.
```kotlin
class User private constructor(val name: String, val age: Int) {
    class Builder {
        private var name: String = ""
        private var age: Int = 0

        fun setName(name: String) = apply { this.name = name }
        fun setAge(age: Int) = apply { this.age = age }
        fun build() = User(name, age)
    }
}
```

---
## 2. Structural Patterns
### **Adapter Pattern**
Bridges incompatible interfaces.
```kotlin
interface JsonParser {
    fun parse(json: String): Map<String, Any>
}

class JsonAdapter : JsonParser {
    override fun parse(json: String): Map<String, Any> {
        return mapOf("example" to "data")
    }
}
```
### **Facade Pattern**
Provides a simplified interface to a complex system.
```kotlin
class PaymentFacade {
    fun processPayment(amount: Double) {
        println("Processing payment of $$amount")
    }
}
```

---
## 3. Behavioral Patterns
### **Observer Pattern**
Implements event-driven programming.
```kotlin
class EventManager {
    private val listeners = mutableListOf<(String) -> Unit>()
    
    fun subscribe(listener: (String) -> Unit) {
        listeners.add(listener)
    }
    
    fun notify(event: String) {
        listeners.forEach { it(event) }
    }
}
```
### **State Pattern**
Manages object behavior based on state.
```kotlin
class TrafficLight {
    var state: String = "Red"
    fun changeState(newState: String) {
        state = newState
    }
}
```

---
## 4. Concurrency Patterns
### **Coroutines for Concurrency**
Kotlin Coroutines for async programming.
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    launch {
        delay(1000)
        println("Task completed")
    }
    println("Waiting...")
}
```

---
## 5. Dependency Injection in KMP
### **Manual DI (Constructor Injection)**
```kotlin
class Repository(val apiService: ApiService)
```
### **Using Expect/Actual for Platform-Specific DI**
```kotlin
expect class PlatformService() {
    fun getPlatformName(): String
}
```
### **Using Koin for DI**
```kotlin
import org.koin.core.context.startKoin
import org.koin.dsl.module

val appModule = module {
    single { ApiService() }
}

fun main() {
    startKoin {
        modules(appModule)
    }
}
```

---
## Conclusion
- Design patterns enhance code quality in KMP.
- Use `expect/actual`, coroutines, and DI frameworks like Koin for scalable cross-platform development.

---

