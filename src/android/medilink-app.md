# Building MediLink App

This chapter provides a comprehensive guide to building the MediLink app, covering all major features and implementation details.

## App Overview

MediLink is a healthcare appointment management app that connects patients with doctors. The app features:

1. **Authentication**
   - User registration
   - Login
   - Password recovery

2. **Profile Management**
   - User profiles
   - Doctor profiles
   - Profile editing

3. **Appointment Booking**
   - Doctor search
   - Appointment scheduling
   - Appointment management

4. **Medical Reports**
   - Report upload
   - Report viewing
   - Report sharing

## Project Setup

### 1. Dependencies
```groovy
// build.gradle
dependencies {
    // Core
    implementation "androidx.core:core-ktx:1.9.0"
    implementation "androidx.lifecycle:lifecycle-runtime-ktx:2.6.1"
    
    // Compose
    implementation "androidx.compose.ui:ui:$compose_version"
    implementation "androidx.compose.material:material:$compose_version"
    implementation "androidx.compose.ui:ui-tooling-preview:$compose_version"
    
    // Navigation
    implementation "androidx.navigation:navigation-compose:2.5.3"
    
    // Dependency Injection
    implementation "com.google.dagger:hilt-android:2.44"
    kapt "com.google.dagger:hilt-compiler:2.44"
    
    // Networking
    implementation "io.ktor:ktor-client-android:2.2.4"
    implementation "io.ktor:ktor-client-content-negotiation:2.2.4"
    implementation "io.ktor:ktor-serialization-kotlinx-json:2.2.4"
    
    // Image Loading
    implementation "io.coil-kt:coil-compose:2.2.2"
}
```

### 2. Project Structure
```
app/
├── features/
│   ├── auth/
│   ├── profile/
│   ├── appointments/
│   └── reports/
├── core/
│   ├── network/
│   ├── di/
│   └── utils/
└── ui/
    ├── theme/
    └── components/
```

## Feature Implementation

### 1. Authentication

#### Login Screen
```kotlin
@Composable
fun LoginScreen(
    viewModel: LoginViewModel = hiltViewModel(),
    onLoginSuccess: () -> Unit
) {
    val state by viewModel.state.collectAsState()
    
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        Text(
            text = "Welcome Back",
            style = MaterialTheme.typography.h4
        )
        
        Spacer(modifier = Modifier.height(32.dp))
        
        OutlinedTextField(
            value = state.email,
            onValueChange = { viewModel.onEvent(LoginEvent.EmailChanged(it)) },
            label = { Text("Email") },
            modifier = Modifier.fillMaxWidth()
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        OutlinedTextField(
            value = state.password,
            onValueChange = { viewModel.onEvent(LoginEvent.PasswordChanged(it)) },
            label = { Text("Password") },
            visualTransformation = PasswordVisualTransformation(),
            modifier = Modifier.fillMaxWidth()
        )
        
        Spacer(modifier = Modifier.height(32.dp))
        
        Button(
            onClick = { viewModel.onEvent(LoginEvent.LoginClicked) },
            modifier = Modifier.fillMaxWidth(),
            enabled = !state.isLoading
        ) {
            if (state.isLoading) {
                CircularProgressIndicator(color = MaterialTheme.colors.onPrimary)
            } else {
                Text("Login")
            }
        }
    }
}
```

#### Login ViewModel
```kotlin
@HiltViewModel
class LoginViewModel @Inject constructor(
    private val authRepository: AuthRepository
) : ViewModel() {
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
                authRepository.login(_state.value.email, _state.value.password)
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

### 2. Profile Management

#### Profile Screen
```kotlin
@Composable
fun ProfileScreen(
    viewModel: ProfileViewModel = hiltViewModel(),
    onEditProfile: () -> Unit
) {
    val state by viewModel.state.collectAsState()
    
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        ProfileHeader(
            user = state.user,
            onEditClick = onEditProfile
        )
        
        Spacer(modifier = Modifier.height(24.dp))
        
        ProfileDetails(user = state.user)
        
        Spacer(modifier = Modifier.height(24.dp))
        
        MedicalHistory(history = state.medicalHistory)
    }
}
```

### 3. Appointment Booking

#### Appointment List
```kotlin
@Composable
fun AppointmentList(
    appointments: List<Appointment>,
    onAppointmentClick: (String) -> Unit
) {
    LazyColumn {
        items(appointments) { appointment ->
            AppointmentCard(
                appointment = appointment,
                onClick = { onAppointmentClick(appointment.id) }
            )
        }
    }
}

@Composable
fun AppointmentCard(
    appointment: Appointment,
    onClick: () -> Unit
) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(8.dp)
            .clickable(onClick = onClick),
        elevation = 4.dp
    ) {
        Column(
            modifier = Modifier.padding(16.dp)
        ) {
            Text(
                text = appointment.doctorName,
                style = MaterialTheme.typography.h6
            )
            
            Spacer(modifier = Modifier.height(8.dp))
            
            Text(
                text = appointment.date,
                style = MaterialTheme.typography.body2
            )
            
            Spacer(modifier = Modifier.height(8.dp))
            
            Text(
                text = appointment.status.name,
                color = when (appointment.status) {
                    AppointmentStatus.CONFIRMED -> MaterialTheme.colors.primary
                    AppointmentStatus.PENDING -> MaterialTheme.colors.secondary
                    AppointmentStatus.CANCELLED -> MaterialTheme.colors.error
                }
            )
        }
    }
}
```

### 4. Medical Reports

#### Report Upload
```kotlin
@Composable
fun ReportUploadScreen(
    viewModel: ReportViewModel = hiltViewModel(),
    onUploadComplete: () -> Unit
) {
    val state by viewModel.state.collectAsState()
    
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        Text(
            text = "Upload Medical Report",
            style = MaterialTheme.typography.h5
        )
        
        Spacer(modifier = Modifier.height(24.dp))
        
        FilePicker(
            onFileSelected = { file ->
                viewModel.onEvent(ReportEvent.FileSelected(file))
            }
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        OutlinedTextField(
            value = state.description,
            onValueChange = { viewModel.onEvent(ReportEvent.DescriptionChanged(it)) },
            label = { Text("Description") },
            modifier = Modifier.fillMaxWidth()
        )
        
        Spacer(modifier = Modifier.height(32.dp))
        
        Button(
            onClick = { viewModel.onEvent(ReportEvent.UploadClicked) },
            modifier = Modifier.fillMaxWidth(),
            enabled = !state.isUploading
        ) {
            if (state.isUploading) {
                CircularProgressIndicator(color = MaterialTheme.colors.onPrimary)
            } else {
                Text("Upload Report")
            }
        }
    }
}
```

## Best Practices

### 1. Error Handling
```kotlin
sealed class Result<out T> {
    data class Success<T>(val data: T) : Result<T>()
    data class Error(val exception: Exception) : Result<Nothing>()
    object Loading : Result<Nothing>()
}

class Repository @Inject constructor(
    private val api: ApiService
) {
    suspend fun getData(): Result<Data> {
        return try {
            val response = api.getData()
            Result.Success(response)
        } catch (e: Exception) {
            Result.Error(e)
        }
    }
}
```

### 2. Dependency Injection
```kotlin
@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    @Singleton
    fun provideApiService(): ApiService {
        return KtorClient.create()
    }
    
    @Provides
    @Singleton
    fun provideAuthRepository(
        apiService: ApiService
    ): AuthRepository {
        return AuthRepositoryImpl(apiService)
    }
}
```

### 3. Testing
```kotlin
@HiltAndroidTest
class LoginScreenTest {
    @get:Rule
    val composeTestRule = createComposeRule()
    
    @Test
    fun loginScreen_displaysCorrectly() {
        composeTestRule.setContent {
            MediLinkTheme {
                LoginScreen()
            }
        }
        
        composeTestRule.onNodeWithText("Welcome Back").assertExists()
        composeTestRule.onNodeWithText("Email").assertExists()
        composeTestRule.onNodeWithText("Password").assertExists()
        composeTestRule.onNodeWithText("Login").assertExists()
    }
}
```

## Next Steps

1. Implement [Authentication](./medilink-auth.md)
2. Add [Profile Management](./medilink-profile.md)
3. Create [Appointment Booking](./medilink-appointments.md)
4. Add [Medical Reports](./medilink-reports.md)

> Tip: Use the Android Studio Layout Inspector to debug UI issues.

> Note: Follow Material Design guidelines for a consistent user experience.
