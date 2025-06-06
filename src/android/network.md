# Network Layer

This chapter explains the network layer implementation in the MediLink app, covering the API service, HTTP client setup, and request handling.

## API Service Implementation

```kotlin
class AuthService {
    private val client = HttpClient(Android) {
        install(ContentNegotiation) {
            json(Json {
                ignoreUnknownKeys = true
                isLenient = true
            })
        }
    }

    private val baseUrl = "https://bd16-150-107-16-195.ngrok-free.app/v1"

    suspend fun signup(request: SignupRequest): ApiResponse<User> {
        return client.post("$baseUrl/auth/signup") {
            contentType(ContentType.Application.Json)
            setBody(request)
        }.body()
    }

    suspend fun login(request: LoginRequest): ApiResponse<User> {
        return client.post("$baseUrl/auth/login") {
            contentType(ContentType.Application.Json)
            setBody(request)
        }.body()
    }

    companion object {
        fun create(): AuthService {
            return AuthService()
        }
    }
}
```

## HTTP Client Configuration

### 1. Ktor Client Setup
```kotlin
HttpClient(Android) {
    install(ContentNegotiation) {
        json(Json {
            ignoreUnknownKeys = true
            isLenient = true
        })
    }
}
```

The Ktor client configuration:
- Uses Android engine for HTTP requests
- Installs content negotiation for JSON handling
- Configures JSON serialization options

### 2. Request Configuration
```kotlin
client.post("$baseUrl/auth/signup") {
    contentType(ContentType.Application.Json)
    setBody(request)
}
```

Request configuration includes:
- Setting content type
- Adding request body
- Configuring headers
- Handling response

## Best Practices

1. **API Organization**
   - Group related endpoints
   - Use clear naming conventions
   - Document API contracts
   - Handle versioning

2. **Error Handling**
   - Implement proper error responses
   - Handle network errors
   - Provide meaningful error messages
   - Log errors for debugging

3. **Security**
   - Use HTTPS
   - Implement proper authentication
   - Handle sensitive data
   - Validate responses

4. **Performance**
   - Use connection pooling
   - Implement caching
   - Handle timeouts
   - Optimize payload size

## Next Steps

1. Learn about [Data Models](./data-models.md)
2. Study [Authentication](./authentication.md)
3. Implement [Error Handling](./error-handling.md)

> Tip: Use Postman or similar tools to test API endpoints before implementation.

> Note: Always handle network errors gracefully and provide offline support when possible. 