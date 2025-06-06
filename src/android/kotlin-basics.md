# Kotlin Basics

Kotlin is a modern programming language that's fully interoperable with Java and is the preferred language for Android development. This chapter covers the essential Kotlin concepts you'll need for Android development.

## Variables and Data Types

### Variable Declaration

```kotlin
// Mutable variable (can be changed)
var count = 0

// Immutable variable (cannot be changed)
val name = "John"

// Type inference
var age = 25  // Int
var height = 1.75  // Double
var isActive = true  // Boolean
```

### Basic Data Types

```kotlin
// Numbers
val intNumber: Int = 42
val longNumber: Long = 42L
val floatNumber: Float = 42.0f
val doubleNumber: Double = 42.0

// Strings
val message: String = "Hello, World!"
val multilineString = """
    This is a multiline
    string in Kotlin
""".trimIndent()

// Boolean
val isTrue: Boolean = true
```

## Functions

### Basic Function

```kotlin
fun greet(name: String): String {
    return "Hello, $name!"
}

// Single-expression function
fun square(x: Int) = x * x

// Function with default parameters
fun greetUser(name: String, greeting: String = "Hello") = "$greeting, $name!"
```

### Lambda Functions

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// Lambda function
val doubled = numbers.map { it * 2 }

// Function type
val sum: (Int, Int) -> Int = { a, b -> a + b }
```

## Control Flow

### If Expression

```kotlin
val max = if (a > b) a else b

// If-else blocks
val result = if (score >= 90) {
    "A"
} else if (score >= 80) {
    "B"
} else {
    "C"
}
```

### When Expression (Switch)

```kotlin
val grade = when (score) {
    in 90..100 -> "A"
    in 80..89 -> "B"
    in 70..79 -> "C"
    else -> "F"
}
```

## Collections

### Lists

```kotlin
// Immutable list
val numbers = listOf(1, 2, 3, 4, 5)

// Mutable list
val mutableNumbers = mutableListOf(1, 2, 3)
mutableNumbers.add(4)

// List operations
val doubled = numbers.map { it * 2 }
val evenNumbers = numbers.filter { it % 2 == 0 }
val sum = numbers.reduce { acc, num -> acc + num }
```

### Maps

```kotlin
// Immutable map
val userMap = mapOf(
    "name" to "John",
    "age" to 25
)

// Mutable map
val mutableMap = mutableMapOf<String, Any>()
mutableMap["name"] = "John"
mutableMap["age"] = 25
```

## Classes and Objects

### Basic Class

```kotlin
class User(
    val name: String,
    var age: Int
) {
    fun greet() = "Hello, I'm $name"
}

// Usage
val user = User("John", 25)
println(user.greet())
```

### Data Class

```kotlin
data class Patient(
    val id: String,
    val name: String,
    var age: Int,
    var medicalHistory: List<String> = emptyList()
)

// Usage
val patient = Patient("P001", "John", 30)
val (id, name, age) = patient  // Destructuring
```

## Null Safety

### Nullable Types

```kotlin
// Nullable type
var nullableName: String? = null

// Safe call operator
val length = nullableName?.length

// Elvis operator
val nameLength = nullableName?.length ?: 0

// Not-null assertion
val forcedLength = nullableName!!.length
```

## Coroutines

### Basic Coroutine

```kotlin
import kotlinx.coroutines.*

// Launch a coroutine
GlobalScope.launch {
    delay(1000L)
    println("World!")
}

// Async coroutine
val result = GlobalScope.async {
    delay(1000L)
    "Hello"
}.await()
```

## Practical Example: User Authentication

Here's a practical example combining several Kotlin concepts:

```kotlin
data class User(
    val id: String,
    val email: String,
    val name: String
)

class AuthManager {
    private val users = mutableMapOf<String, User>()
    
    suspend fun login(email: String, password: String): Result<User> {
        return try {
            // Simulate network delay
            delay(1000)
            
            // Find user
            val user = users[email] ?: throw Exception("User not found")
            
            // In real app, verify password here
            Result.success(user)
        } catch (e: Exception) {
            Result.failure(e)
        }
    }
    
    fun register(email: String, name: String): User {
        val user = User(
            id = UUID.randomUUID().toString(),
            email = email,
            name = name
        )
        users[email] = user
        return user
    }
}
```

## Next Steps

1. Learn about [Android Project Structure](./project-structure.md)
2. Understand [Jetpack Compose](./compose-fundamentals.md)
3. Study [MVVM Architecture](./mvvm-architecture.md)

> Tip: Practice these concepts by implementing small features in the MediLink app. Start with simple UI components and gradually move to more complex features.

> Note: Kotlin's null safety features help prevent many common programming errors. Always use nullable types when a value might be null.
