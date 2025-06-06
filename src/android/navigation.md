# Navigation

Navigation is a crucial part of any Android application. This chapter explains how to implement navigation in the MediLink app using Jetpack Compose Navigation.

## Navigation Components

### 1. NavHost
The container for navigation graph.

```kotlin
@Composable
fun MediLinkNavigation() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = "greeting"
    ) {
        composable("greeting") {
            GreetingScreen(
                onGreetingComplete = {
                    navController.navigate("login") {
                        popUpTo("greeting") { inclusive = true }
                    }
                }
            )
        }
        
        composable("login") {
            LoginScreen(
                onLoginSuccess = {
                    navController.navigate("home") {
                        popUpTo("login") { inclusive = true }
                    }
                }
            )
        }
        
        composable("home") {
            HomeScreen()
        }
    }
}
```

### 2. Navigation Routes
Define routes as constants to avoid typos.

```kotlin
object Routes {
    const val GREETING = "greeting"
    const val LOGIN = "login"
    const val REGISTER = "register"
    const val HOME = "home"
    const val APPOINTMENTS = "appointments"
    const val PROFILE = "profile"
    
    // Nested routes
    const val APPOINTMENT_DETAILS = "appointment/{appointmentId}"
    
    // Helper function for parameterized routes
    fun appointmentDetails(appointmentId: String) = "appointment/$appointmentId"
}
```

## Navigation Patterns

### 1. Basic Navigation
```kotlin
@Composable
fun BasicNavigation() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = Routes.GREETING
    ) {
        composable(Routes.GREETING) {
            GreetingScreen(
                onGreetingComplete = {
                    navController.navigate(Routes.LOGIN)
                }
            )
        }
        
        composable(Routes.LOGIN) {
            LoginScreen(
                onLoginSuccess = {
                    navController.navigate(Routes.HOME)
                }
            )
        }
    }
}
```

### 2. Navigation with Arguments
```kotlin
@Composable
fun NavigationWithArgs() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = Routes.HOME
    ) {
        composable(Routes.HOME) {
            HomeScreen(
                onAppointmentClick = { appointmentId ->
                    navController.navigate(Routes.appointmentDetails(appointmentId))
                }
            )
        }
        
        composable(
            route = Routes.APPOINTMENT_DETAILS,
            arguments = listOf(
                navArgument("appointmentId") { type = NavType.StringType }
            )
        ) { backStackEntry ->
            val appointmentId = backStackEntry.arguments?.getString("appointmentId")
            AppointmentDetailsScreen(appointmentId = appointmentId)
        }
    }
}
```

### 3. Nested Navigation
```kotlin
@Composable
fun NestedNavigation() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = Routes.HOME
    ) {
        composable(Routes.HOME) {
            HomeScreen()
        }
        
        navigation(
            startDestination = "appointments_list",
            route = "appointments"
        ) {
            composable("appointments_list") {
                AppointmentsListScreen(
                    onAppointmentClick = { id ->
                        navController.navigate("appointment/$id")
                    }
                )
            }
            
            composable(
                route = "appointment/{appointmentId}",
                arguments = listOf(
                    navArgument("appointmentId") { type = NavType.StringType }
                )
            ) { backStackEntry ->
                val appointmentId = backStackEntry.arguments?.getString("appointmentId")
                AppointmentDetailsScreen(appointmentId = appointmentId)
            }
        }
    }
}
```

## Navigation Actions

### 1. Basic Navigation Actions
```kotlin
@Composable
fun NavigationActions() {
    val navController = rememberNavController()
    
    // Navigate to a destination
    navController.navigate(Routes.HOME)
    
    // Navigate and clear back stack
    navController.navigate(Routes.HOME) {
        popUpTo(0) { inclusive = true }
    }
    
    // Navigate with options
    navController.navigate(Routes.HOME) {
        popUpTo(Routes.LOGIN) { inclusive = true }
        launchSingleTop = true
    }
}
```

### 2. Navigation with Results
```kotlin
@Composable
fun NavigationWithResults() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = Routes.HOME
    ) {
        composable(Routes.HOME) {
            HomeScreen(
                onEditProfile = {
                    navController.navigate(Routes.PROFILE)
                }
            )
        }
        
        composable(Routes.PROFILE) {
            ProfileScreen(
                onProfileUpdated = { updatedProfile ->
                    // Handle profile update
                    navController.previousBackStackEntry
                        ?.savedStateHandle
                        ?.set("profile_update", updatedProfile)
                    navController.popBackStack()
                }
            )
        }
    }
}
```

## Best Practices

### 1. Route Management
```kotlin
sealed class Screen(val route: String) {
    object Greeting : Screen("greeting")
    object Login : Screen("login")
    object Home : Screen("home")
    object AppointmentDetails : Screen("appointment/{appointmentId}") {
        fun createRoute(appointmentId: String) = "appointment/$appointmentId"
    }
}
```

### 2. Navigation Arguments
```kotlin
@Composable
fun NavigationWithTypeSafeArgs() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = Screen.Home.route
    ) {
        composable(
            route = Screen.AppointmentDetails.route,
            arguments = listOf(
                navArgument("appointmentId") {
                    type = NavType.StringType
                    nullable = false
                }
            )
        ) { backStackEntry ->
            val appointmentId = backStackEntry.arguments?.getString("appointmentId")
            AppointmentDetailsScreen(appointmentId = appointmentId)
        }
    }
}
```

### 3. Deep Links
```kotlin
@Composable
fun NavigationWithDeepLinks() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = Screen.Home.route
    ) {
        composable(
            route = Screen.AppointmentDetails.route,
            arguments = listOf(
                navArgument("appointmentId") { type = NavType.StringType }
            ),
            deepLinks = listOf(
                navDeepLink {
                    uriPattern = "medilink://appointment/{appointmentId}"
                }
            )
        ) { backStackEntry ->
            val appointmentId = backStackEntry.arguments?.getString("appointmentId")
            AppointmentDetailsScreen(appointmentId = appointmentId)
        }
    }
}
```

## Common Pitfalls

### 1. Navigation Stack Management
```kotlin
// Bad - Creates multiple instances
navController.navigate(Routes.HOME)

// Good - Prevents multiple instances
navController.navigate(Routes.HOME) {
    launchSingleTop = true
}
```

### 2. Back Stack Handling
```kotlin
// Bad - Unclear back stack behavior
navController.navigate(Routes.HOME)

// Good - Clear back stack behavior
navController.navigate(Routes.HOME) {
    popUpTo(Routes.LOGIN) { inclusive = true }
}
```

## Bottom Navigation Implementation

### 1. Screen Definitions
```kotlin
sealed class Screen(val route: String, val title: String) {
    object Reports : Screen("reports", "Reports")
    object Appointments : Screen("appointments", "Appointments")
    object Profile : Screen("profile", "Profile")
}
```

The `Screen` sealed class defines the navigation destinations in the app:
- Uses sealed class for type safety
- Each screen has a unique route and title
- Makes it impossible to create new screen types outside this class
- Helps with exhaustive when expressions

### 2. Main Navigation
```kotlin
@Composable
fun MainNavigation() {
    var selectedScreen by remember { mutableStateOf<Screen>(Screen.Reports) }

    val items = listOf(
        Triple(Screen.Reports, Icons.Default.Warning, "Reports"),
        Triple(Screen.Appointments, Icons.Default.DateRange, "Appointments"),
        Triple(Screen.Profile, Icons.Default.Person, "Profile")
    )

    Scaffold(
        bottomBar = {
            NavigationBar {
                items.forEach { (screen, icon, label) ->
                    NavigationBarItem(
                        icon = { Icon(icon, contentDescription = label) },
                        label = { Text(label) },
                        selected = selectedScreen == screen,
                        onClick = { selectedScreen = screen }
                    )
                }
            }
        }
    ) { paddingValues ->
        when (selectedScreen) {
            Screen.Reports -> ReportsScreen()
            Screen.Appointments -> AppointmentsScreen()
            Screen.Profile -> ProfileScreen()
        }
    }
}
```

The `MainNavigation` composable:
- Manages navigation state using `remember` and `mutableStateOf`
- Uses `Scaffold` for proper Material Design layout
- Implements bottom navigation using `NavigationBar`
- Handles screen switching based on selection

## Screen Implementations

### 1. Reports Screen
```kotlin
@Composable
fun ReportsScreen() {
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Text(text = "Reports Screen")
    }
}
```

The `ReportsScreen` composable:
- Displays medical reports and test results
- Uses `Box` for centering content
- Currently shows placeholder text
- Can be expanded to show actual reports

### 2. Appointments Screen
```kotlin
@Composable
fun AppointmentsScreen() {
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Text(text = "Appointments Screen")
    }
}
```

The `AppointmentsScreen` composable:
- Manages and displays medical appointments
- Uses `Box` for centering content
- Currently shows placeholder text
- Can be expanded to show appointment list/calendar

### 3. Profile Screen
```kotlin
@Composable
fun ProfileScreen() {
    val viewModel: AuthViewModel = viewModel()
    val showSignup by viewModel.showSignup.collectAsState()
    val selectedRole by viewModel.selectedRole.collectAsState()
    val error by viewModel.error.collectAsState()
    val authResult by viewModel.authResult.collectAsState()
    val hasToken by viewModel.hasToken.collectAsState()

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        // Error display
        error?.let {
            Text(
                text = it,
                color = MaterialTheme.colorScheme.error,
                modifier = Modifier.padding(bottom = 16.dp)
            )
        }

        // Authentication result display
        authResult?.let {
            Column(
                horizontalAlignment = Alignment.CenterHorizontally,
                modifier = Modifier.padding(bottom = 16.dp)
            ) {
                Text(
                    text = "Welcome, ${it.name}!",
                    style = MaterialTheme.typography.headlineMedium
                )
                Text(
                    text = "Email: ${it.email}",
                    style = MaterialTheme.typography.bodyLarge
                )
                Text(
                    text = "Role: ${it.role}",
                    style = MaterialTheme.typography.bodyLarge
                )
                if (!it.verifiedEmail) {
                    Text(
                        text = "Please verify your email",
                        color = MaterialTheme.colorScheme.error,
                        style = MaterialTheme.typography.bodyMedium
                    )
                }
            }
        }

        if (hasToken) {
            // Logout button
            Button(
                onClick = { viewModel.logout() },
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(vertical = 8.dp)
            ) {
                Text("Logout")
            }
        } else {
            // Authentication forms
            // Role selection
            Row(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(bottom = 16.dp),
                horizontalArrangement = Arrangement.SpaceEvenly
            ) {
                UserRole.values().forEach { role ->
                    Row(
                        verticalAlignment = Alignment.CenterVertically
                    ) {
                        RadioButton(
                            selected = selectedRole == role,
                            onClick = { viewModel.updateRole(role) }
                        )
                        Text(role.value.capitalize())
                    }
                }
            }

            // Form fields
            OutlinedTextField(
                value = email,
                onValueChange = { email = it },
                label = { Text("Email") },
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(bottom = 8.dp),
                keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Email)
            )

            OutlinedTextField(
                value = password,
                onValueChange = { password = it },
                label = { Text("Password") },
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(bottom = 8.dp),
                visualTransformation = PasswordVisualTransformation(),
                keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Password)
            )

            // Name field for signup
            if (showSignup) {
                OutlinedTextField(
                    value = name,
                    onValueChange = { name = it },
                    label = { Text("Name") },
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(bottom = 8.dp)
                )
            }

            // Action buttons
            Button(
                onClick = {
                    if (showSignup) {
                        viewModel.signup(email, password, name)
                    } else {
                        viewModel.login(email, password)
                    }
                },
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(vertical = 8.dp)
            ) {
                Text(if (showSignup) "Sign Up" else "Login")
            }

            // Toggle between login and signup
            TextButton(
                onClick = { viewModel.toggleSignup() }
            ) {
                Text(
                    if (showSignup) "Already have an account? Login"
                    else "New user? Sign up"
                )
            }
        }
    }
}
```

The `ProfileScreen` composable:
- Handles user authentication and profile management
- Provides login and signup functionality
- Allows user role selection
- Shows authentication status
- Manages token-based visibility
- Uses Material Design 3 components
- Implements form validation and error handling

## Best Practices for Screen Implementation

1. **State Management**
   - Use ViewModel for business logic
   - Collect state using `collectAsState()`
   - Handle loading and error states

2. **UI Organization**
   - Use appropriate layout composables
   - Follow Material Design guidelines
   - Implement proper spacing and padding

3. **Form Handling**
   - Validate user input
   - Show appropriate error messages
   - Use proper keyboard types
   - Implement password masking

4. **Navigation**
   - Use type-safe navigation
   - Handle back stack properly
   - Implement deep linking

## Authentication Implementation

### 1. Data Models
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

enum class UserRole(val value: String) {
    PATIENT("patient"),
    DOCTOR("doctor")
}
```

The data models:
- Use Kotlin serialization for JSON conversion
- Define clear contracts for API communication
- Ensure type safety in data exchange
- Provide structured user role management

### 2. Network Service
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

The `AuthService`:
- Uses Ktor client for HTTP requests
- Handles JSON serialization/deserialization
- Provides centralized authentication API calls
- Manages request/response handling

### 3. ViewModel
```kotlin
class AuthViewModel(application: Application) : AndroidViewModel(application) {
    private val authService = AuthService.create()
    private val tokenManager = TokenManager(application)

    // State management
    private val _showSignup = MutableStateFlow(false)
    val showSignup: StateFlow<Boolean> = _showSignup

    private val _selectedRole = MutableStateFlow(UserRole.PATIENT)
    val selectedRole: StateFlow<UserRole> = _selectedRole

    private val _authResult = MutableStateFlow<User?>(null)
    val authResult: StateFlow<User?> = _authResult

    private val _error = MutableStateFlow<String?>(null)
    val error: StateFlow<String?> = _error

    private val _hasToken = MutableStateFlow(false)
    val hasToken: StateFlow<Boolean> = _hasToken

    init {
        viewModelScope.launch {
            val token = tokenManager.accessToken.first()
            _hasToken.value = token != null
        }
    }

    fun toggleSignup() {
        _showSignup.value = !_showSignup.value
        _error.value = null
    }

    fun updateRole(role: UserRole) {
        _selectedRole.value = role
    }

    fun login(email: String, password: String) {
        viewModelScope.launch {
            try {
                _error.value = null
                val response = authService.login(
                    LoginRequest(
                        email = email,
                        password = password,
                        role = _selectedRole.value.value
                    )
                )
                if (response.error == null) {
                    _authResult.value = response.data
                    response.data.accessToken?.let { token ->
                        tokenManager.saveToken(token)
                        _hasToken.value = true
                    }
                } else {
                    _error.value = response.error
                }
            } catch (e: Exception) {
                _error.value = e.message ?: "Login failed"
            }
        }
    }

    fun signup(email: String, password: String, name: String) {
        viewModelScope.launch {
            try {
                _error.value = null
                val response = authService.signup(
                    SignupRequest(
                        email = email,
                        password = password,
                        name = name
                    )
                )
                if (response.error == null) {
                    _authResult.value = response.data
                } else {
                    _error.value = response.error
                }
            } catch (e: Exception) {
                _error.value = e.message ?: "Signup failed"
            }
        }
    }

    fun logout() {
        viewModelScope.launch {
            tokenManager.clearToken()
            _hasToken.value = false
            _authResult.value = null
        }
    }
}
```

The `AuthViewModel`:
- Manages authentication state using StateFlow
- Handles user authentication flow
- Provides error handling
- Manages token storage
- Implements login, signup, and logout operations

## Authentication Flow

1. **Initial State**
   - Check for existing token
   - Show login form by default
   - Set default user role

2. **Login Process**
   - Validate input
   - Send login request
   - Handle response
   - Store token if successful
   - Show error if failed

3. **Signup Process**
   - Validate input
   - Send signup request
   - Handle response
   - Show success/error message

4. **Logout Process**
   - Clear stored token
   - Reset authentication state
   - Show login form

## Best Practices for Authentication

1. **State Management**
   - Use StateFlow for reactive state
   - Handle loading states
   - Provide clear error messages
   - Maintain token state

2. **Security**
   - Use HTTPS for API calls
   - Store tokens securely
   - Implement proper password handling
   - Validate user input

3. **Error Handling**
   - Catch network errors
   - Handle API errors
   - Show user-friendly messages
   - Log errors for debugging

4. **User Experience**
   - Show loading indicators
   - Provide clear feedback
   - Handle edge cases
   - Maintain session state

## Next Steps

1. Implement [Token Management](./medilink-token.md)
2. Add [User Profile](./medilink-profile.md)
3. Enhance [Error Handling](./medilink-errors.md)

> Tip: Use Android Studio's Network Inspector to debug API calls.

> Note: Always handle authentication errors gracefully and provide clear feedback to users.
