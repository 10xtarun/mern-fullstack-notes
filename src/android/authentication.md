# Authentication

This chapter explains the authentication implementation in the MediLink app, covering the ViewModel, UI, and authentication flow.

## Authentication ViewModel

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

## Best Practices

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

1. Learn about [Network Layer](./network.md)
2. Study [Data Models](./data-models.md)
3. Implement [Token Management](./token-management.md)

> Tip: Use Android Studio's Network Inspector to debug API calls.

> Note: Always handle authentication errors gracefully and provide clear feedback to users. 