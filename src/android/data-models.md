# Data Models

This chapter explains the data models used in the MediLink app, covering request/response models, serialization, and type safety.

## Authentication Models

### 1. Request Models
```kotlin
@Serializable
data class SignupRequest(
    val email: String,
    val password: String,
    val name: String
)

@Serializable
data class LoginRequest(
    val email: String,
    val password: String,
    val role: String
)
```

The request models:
- Use Kotlin serialization for JSON conversion
- Define clear contracts for API requests
- Ensure type safety in data exchange
- Follow naming conventions

### 2. Response Models
```kotlin
@Serializable
data class ApiResponse<T>(
    val message: String,
    val error: String?,
    val data: T
)

@Serializable
data class User(
    val _id: String,
    val name: String,
    val email: String,
    val verifiedEmail: Boolean,
    val role: String,
    val __v: Int,
    val accessToken: String? = null
)
```

The response models:
- Use generic type for flexible data handling
- Include error handling
- Provide clear data structure
- Support optional fields

### 3. Enum Models
```kotlin
enum class UserRole(val value: String) {
    PATIENT("patient"),
    DOCTOR("doctor")
}
```

The enum models:
- Provide type-safe role handling
- Prevent typos in role strings
- Make role management maintainable
- Support string conversion

## Best Practices

1. **Model Design**
   - Use data classes for immutability
   - Implement proper serialization
   - Follow naming conventions
   - Document model purposes

2. **Type Safety**
   - Use sealed classes when appropriate
   - Implement proper validation
   - Handle nullable types
   - Use enums for constants

3. **Serialization**
   - Configure JSON options
   - Handle unknown fields
   - Validate data
   - Provide default values

4. **Documentation**
   - Document model purposes
   - Explain field meanings
   - Provide usage examples
   - Include validation rules

## Next Steps

1. Learn about [Network Layer](./network.md)
2. Study [Authentication](./authentication.md)
3. Implement [Data Validation](./data-validation.md)

> Tip: Use Kotlin's data class features for clean model implementation.

> Note: Always validate data before sending it to the API. 