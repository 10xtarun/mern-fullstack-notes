# MediLink Implementation

This section covers the practical implementation of the MediLink app, focusing on the initial greeting screen and network communication setup.

## Greeting Screen Implementation

The greeting screen is the first screen users see when launching the app. It displays a welcome message for 2 seconds before transitioning to the main content.

### UI Layer (GreetingScreen.kt)

```kotlin
@Composable
fun GreetingScreen(
    viewModel: GreetingViewModel,
    onGreetingComplete: () -> Unit
) {
    // Collect the greeting message from ViewModel
    val greeting by viewModel.greeting.collectAsState()

    // Launch a coroutine to handle the 2-second delay
    LaunchedEffect(key1 = true) {
        delay(2000) // Show for 2 seconds
        onGreetingComplete() // Notify parent that greeting is complete
    }

    // Center the greeting message on screen
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Text(
            text = greeting,
            fontSize = 24.sp,
            textAlign = TextAlign.Center
        )
    }
}
```

Key components of the greeting screen:

1. **State Collection**
   - Uses `collectAsState()` to observe the greeting message from ViewModel
   - Automatically updates UI when greeting changes

2. **Timed Transition**
   - Uses `LaunchedEffect` to handle the 2-second delay
   - Calls `onGreetingComplete` callback after delay

3. **Layout**
   - Uses `Box` with `Alignment.Center` for centered content
   - Applies `fillMaxSize()` modifier to use full screen space

## Network Layer (GreetingService.kt)

The network layer handles API communication using Ktor client.

```kotlin
class GreetingService {
    private val client = HttpClient(Android) {
        install(ContentNegotiation) {
            json(Json {
                ignoreUnknownKeys = true
                isLenient = true
            })
        }
    }

    private val baseUrl = "https://bd16-150-107-16-195.ngrok-free.app"

    suspend fun getGreeting(): GreetingResponse {
        return client.get("$baseUrl/greeting").body()
    }
}
```

Key features of the network layer:

1. **Ktor Client Setup**
   - Uses Android engine for HTTP requests
   - Configures JSON serialization with lenient parsing

2. **API Response Model**
   ```kotlin
   @Serializable
   data class GreetingResponse(
       val message: String
   )
   ```
   - Uses Kotlin serialization for JSON parsing
   - Simple data class to represent API response

3. **API Call**
   - Suspend function for asynchronous network call
   - Returns deserialized response object

## ViewModel Layer (GreetingViewModel.kt)

The ViewModel manages the greeting screen's state and data operations.

```kotlin
class GreetingViewModel : ViewModel() {
    private val greetingService = GreetingService.create()
    
    private val _greeting = MutableStateFlow<String>("")
    val greeting: StateFlow<String> = _greeting

    init {
        fetchGreeting()
    }

    private fun fetchGreeting() {
        viewModelScope.launch {
            try {
                val response = greetingService.getGreeting()
                _greeting.value = response.message
            } catch (e: Exception) {
                _greeting.value = "Welcome to MediLink!"
            }
        }
    }
}
```

Key aspects of the ViewModel:

1. **State Management**
   - Uses `MutableStateFlow` for internal state
   - Exposes immutable `StateFlow` to UI

2. **Error Handling**
   - Provides fallback message if API call fails
   - Uses try-catch for graceful error handling

3. **Coroutine Scope**
   - Uses `viewModelScope` for coroutine management
   - Automatically cancels coroutines when ViewModel is cleared

## Implementation Flow

1. **App Launch**
   - `GreetingViewModel` is created
   - `init` block triggers `fetchGreeting()`

2. **Network Request**
   - `GreetingService` makes API call
   - Response is deserialized to `GreetingResponse`

3. **State Update**
   - ViewModel updates greeting state
   - UI automatically updates via `collectAsState()`

4. **Screen Transition**
   - `LaunchedEffect` waits 2 seconds
   - Calls `onGreetingComplete` to trigger navigation

## Best Practices Demonstrated

1. **Separation of Concerns**
   - UI logic in Composable
   - Network logic in Service
   - State management in ViewModel

2. **Error Handling**
   - Graceful fallback for network errors
   - User-friendly error messages

3. **State Management**
   - Unidirectional data flow
   - Immutable state exposure

4. **Coroutine Usage**
   - Proper scope management
   - Structured concurrency

## Next Steps

1. Implement [Authentication](./medilink-auth.md)
2. Add [Profile Management](./medilink-profile.md)
3. Create [Appointment Booking](./medilink-appointments.md)

> Tip: Use this greeting screen implementation as a template for other screens in the app. The pattern of ViewModel + Service + UI can be reused for different features.

> Note: The network layer uses Ktor client, which is a modern and efficient HTTP client for Kotlin. Consider using it for all network operations in the app. 