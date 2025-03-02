# Singleton and Factory Design Patterns in Kotlin Multiplatform (KMP)

## Singleton Pattern
The **Singleton Pattern** ensures a class has only one instance and provides a global access point to that instance. 

### Why Use Singleton?
- Prevents multiple instances of a class.
- Useful for shared resources (e.g., database, network clients, logging, config settings).
- Reduces memory usage and maintains a consistent state.

### Singleton in Kotlin Multiplatform
```kotlin
object AppConfig {
    val apiBaseUrl: String = "https://api.example.com"
}
```
This ensures **only one instance** of `AppConfig` exists across platforms.

### Alternatives to Singleton
- **Dependency Injection (DI)** – Inject instances instead of making them globally accessible.
- **Static Methods** – Use a class with static methods instead of a singleton.

---
## Factory Pattern
The **Factory Pattern** provides an interface for creating objects **without exposing the instantiation logic**.

### Why Use Factory?
- Encapsulates object creation logic.
- Reduces code duplication when creating similar objects.
- Improves scalability and maintainability.

### Factory in Kotlin Multiplatform
```kotlin
interface Car {
    fun drive()
}

class Sedan : Car {
    override fun drive() = println("Driving a Sedan")
}

class SUV : Car {
    override fun drive() = println("Driving an SUV")
}

object CarFactory {
    fun createCar(type: String): Car = when (type) {
        "Sedan" -> Sedan()
        "SUV" -> SUV()
        else -> throw IllegalArgumentException("Unknown car type")
    }
}
```
### Alternatives to Factory
- **Constructor Injection** – Inject dependencies directly instead of using a factory.
- **Polymorphism** – Use subclassing and inheritance instead of a factory.

---
## Conclusion
- **Use Singleton** when you need a single instance shared across the app.
- **Use Factory** when you need a flexible way to create objects dynamically.
- Both patterns help maintain a shared codebase across platforms in Kotlin Multiplatform (KMP).
