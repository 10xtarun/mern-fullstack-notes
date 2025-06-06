# State Management

State management is a crucial aspect of building robust Android applications with Jetpack Compose. This chapter explains different approaches to state management in the MediLink app.

## What is State?

State in Compose is any data that can change over time and affect the UI. Examples include:
- User input
- Network responses
- UI state (loading, error, success)
- App settings

## Types of State

### 1. UI State
```kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }
    
    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

### 2. Application State
```kotlin
data class AppState(
    val isLoggedIn: Boolean = false,
    val currentUser: User? = null,
    val theme: Theme = Theme.LIGHT
)
```

## State Management Approaches

### 1. State Hoisting

Lifting state up to make components more reusable and testable.

```kotlin
@Composable
fun Counter(
    count: Int,
    onIncrement: () -> Unit
) {
    Column {
        Text("Count: $count")
        Button(onClick = onIncrement) {
            Text("Increment")
        }
    }
}

@Composable
fun CounterScreen() {
    var count by remember { mutableStateOf(0) }
    
    Counter(
        count = count,
        onIncrement = { count++ }
    )
}
```

### 2. StateFlow in ViewModel

Using StateFlow for reactive state management.

```kotlin
class AppointmentViewModel : ViewModel() {
    private val _appointments = MutableStateFlow<List<Appointment>>(emptyList())
    val appointments: StateFlow<List<Appointment>> = _appointments.asStateFlow()
    
    private val _isLoading = MutableStateFlow(false)
    val isLoading: StateFlow<Boolean> = _isLoading.asStateFlow()
    
    fun loadAppointments() {
        viewModelScope.launch {
            _isLoading.value = true
            try {
                val result = appointmentRepository.getAppointments()
                _appointments.value = result
            } catch (e: Exception) {
                // Handle error
            } finally {
                _isLoading.value = false
            }
        }
    }
}
```

### 3. State Restoration

Preserving state across configuration changes.

```kotlin
@Composable
fun RememberStateExample() {
    var count by rememberSaveable { mutableStateOf(0) }
    
    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

## State Management Patterns

### 1. Unidirectional Data Flow

```kotlin
// State
data class LoginState(
    val email: String = "",
    val password: String = "",
    val isLoading: Boolean = false,
    val error: String? = null
)

// Events
sealed class LoginEvent {
    data class EmailChanged(val email: String) : LoginEvent()
    data class PasswordChanged(val password: String) : LoginEvent()
    object LoginClicked : LoginEvent()
}

// ViewModel
class LoginViewModel : ViewModel() {
    private val _state = MutableStateFlow(LoginState())
    val state: StateFlow<LoginState> = _state.asStateFlow()
    
    fun onEvent(event: LoginEvent) {
        when (event) {
            is LoginEvent.EmailChanged -> {
                _state.update { it.copy(email = event.email) }
            }
            is LoginEvent.PasswordChanged -> {
                _state.update { it.copy(password = event.password) }
            }
            is LoginEvent.LoginClicked -> {
                login()
            }
        }
    }
    
    private fun login() {
        viewModelScope.launch {
            _state.update { it.copy(isLoading = true) }
            try {
                // Perform login
                _state.update { it.copy(isLoading = false) }
            } catch (e: Exception) {
                _state.update { 
                    it.copy(
                        isLoading = false,
                        error = e.message
                    )
                }
            }
        }
    }
}
```

### 2. State Holder Pattern

```kotlin
class AppointmentStateHolder(
    private val appointmentRepository: AppointmentRepository
) {
    private val _appointments = MutableStateFlow<List<Appointment>>(emptyList())
    val appointments: StateFlow<List<Appointment>> = _appointments.asStateFlow()
    
    fun loadAppointments() {
        viewModelScope.launch {
            _appointments.value = appointmentRepository.getAppointments()
        }
    }
}

@Composable
fun AppointmentScreen(
    stateHolder: AppointmentStateHolder = remember { AppointmentStateHolder() }
) {
    val appointments by stateHolder.appointments.collectAsState()
    
    LaunchedEffect(Unit) {
        stateHolder.loadAppointments()
    }
    
    AppointmentList(appointments = appointments)
}
```

## Best Practices

### 1. State Immutability
```kotlin
// Good
data class UserState(
    val name: String,
    val age: Int
)

// Bad
class MutableUserState {
    var name: String = ""
    var age: Int = 0
}
```

### 2. State Updates
```kotlin
// Good
_state.update { it.copy(isLoading = true) }

// Bad
_state.value = _state.value.copy(isLoading = true)
```

### 3. State Scope
```kotlin
// Good - State scoped to component
@Composable
fun LocalStateExample() {
    var localState by remember { mutableStateOf(0) }
    // Use localState
}

// Good - State shared across components
class SharedViewModel : ViewModel() {
    private val _sharedState = MutableStateFlow(0)
    val sharedState: StateFlow<Int> = _sharedState.asStateFlow()
}
```

## Common Pitfalls

### 1. State Loss
```kotlin
// Bad - State lost on recomposition
@Composable
fun BadExample() {
    var count = 0
    Button(onClick = { count++ }) {
        Text("Count: $count")
    }
}

// Good - State preserved
@Composable
fun GoodExample() {
    var count by remember { mutableStateOf(0) }
    Button(onClick = { count++ }) {
        Text("Count: $count")
    }
}
```

### 2. Unnecessary Recomposition
```kotlin
// Bad - Causes unnecessary recomposition
@Composable
fun BadExample() {
    val expensiveValue = expensiveCalculation()
    Text(text = expensiveValue.toString())
}

// Good - Value remembered
@Composable
fun GoodExample() {
    val expensiveValue = remember {
        expensiveCalculation()
    }
    Text(text = expensiveValue.toString())
}
```

## Next Steps

1. Learn about [Navigation](./navigation.md)
2. Explore [MediLink App](./medilink-app.md)
3. Study [MVVM Architecture](./mvvm-architecture.md)

> Tip: Use `remember` and `rememberSaveable` appropriately based on whether you need to preserve state across configuration changes.

> Note: Keep state as close as possible to where it's used, but lift it up when needed for sharing between components.
