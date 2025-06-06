# MVVM Architecture

MVVM (Model-View-ViewModel) is a software architectural pattern that separates the UI (View) from the business logic (ViewModel) and data (Model). This pattern is particularly well-suited for Android development with Jetpack Compose.

## MVVM Components

### 1. Model
The Model represents the data and business logic of the application.

```kotlin
// Data class representing a patient
data class Patient(
    val id: String,
    val name: String,
    val age: Int,
    val medicalHistory: List<String>
)

// Repository interface
interface PatientRepository {
    suspend fun getPatient(id: String): Patient
    suspend fun updatePatient(patient: Patient)
    suspend fun getAppointments(patientId: String): List<Appointment>
}

// Repository implementation
class PatientRepositoryImpl(
    private val api: ApiService,
    private val database: PatientDatabase
) : PatientRepository {
    override suspend fun getPatient(id: String): Patient {
        return api.getPatient(id)
    }
    
    override suspend fun updatePatient(patient: Patient) {
        api.updatePatient(patient)
        database.patientDao().updatePatient(patient)
    }
    
    override suspend fun getAppointments(patientId: String): List<Appointment> {
        return api.getAppointments(patientId)
    }
}
```

### 2. ViewModel
The ViewModel manages UI-related data and handles business logic.

```kotlin
class PatientViewModel(
    private val repository: PatientRepository
) : ViewModel() {
    private val _patient = MutableStateFlow<Patient?>(null)
    val patient: StateFlow<Patient?> = _patient.asStateFlow()
    
    private val _appointments = MutableStateFlow<List<Appointment>>(emptyList())
    val appointments: StateFlow<List<Appointment>> = _appointments.asStateFlow()
    
    private val _isLoading = MutableStateFlow(false)
    val isLoading: StateFlow<Boolean> = _isLoading.asStateFlow()
    
    fun loadPatient(id: String) {
        viewModelScope.launch {
            _isLoading.value = true
            try {
                _patient.value = repository.getPatient(id)
                _appointments.value = repository.getAppointments(id)
            } catch (e: Exception) {
                // Handle error
            } finally {
                _isLoading.value = false
            }
        }
    }
    
    fun updatePatient(patient: Patient) {
        viewModelScope.launch {
            try {
                repository.updatePatient(patient)
                _patient.value = patient
            } catch (e: Exception) {
                // Handle error
            }
        }
    }
}
```

### 3. View (Compose UI)
The View is responsible for displaying the UI and handling user interactions.

```kotlin
@Composable
fun PatientScreen(
    viewModel: PatientViewModel = viewModel()
) {
    val patient by viewModel.patient.collectAsState()
    val appointments by viewModel.appointments.collectAsState()
    val isLoading by viewModel.isLoading.collectAsState()
    
    if (isLoading) {
        LoadingIndicator()
    } else {
        patient?.let { currentPatient ->
            PatientProfile(
                patient = currentPatient,
                appointments = appointments,
                onUpdatePatient = { viewModel.updatePatient(it) }
            )
        }
    }
}

@Composable
fun PatientProfile(
    patient: Patient,
    appointments: List<Appointment>,
    onUpdatePatient: (Patient) -> Unit
) {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        Text(
            text = patient.name,
            style = MaterialTheme.typography.h5
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Patient details
        PatientDetails(patient)
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Appointments list
        AppointmentsList(appointments)
    }
}
```

## Dependency Injection

Using Hilt for dependency injection:

```kotlin
@HiltViewModel
class PatientViewModel @Inject constructor(
    private val repository: PatientRepository
) : ViewModel() {
    // ... ViewModel implementation
}

@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    @Singleton
    fun providePatientRepository(
        api: ApiService,
        database: PatientDatabase
    ): PatientRepository {
        return PatientRepositoryImpl(api, database)
    }
}
```

## Practical Example: Appointment Booking

Here's a complete example of MVVM implementation for appointment booking:

### Model

```kotlin
data class Appointment(
    val id: String,
    val patientId: String,
    val doctorId: String,
    val dateTime: LocalDateTime,
    val status: AppointmentStatus
)

enum class AppointmentStatus {
    PENDING, CONFIRMED, CANCELLED
}

interface AppointmentRepository {
    suspend fun bookAppointment(appointment: Appointment): Result<Appointment>
    suspend fun getAvailableSlots(doctorId: String, date: LocalDate): List<LocalDateTime>
    suspend fun cancelAppointment(appointmentId: String): Result<Unit>
}
```

### ViewModel

```kotlin
@HiltViewModel
class AppointmentViewModel @Inject constructor(
    private val repository: AppointmentRepository
) : ViewModel() {
    private val _availableSlots = MutableStateFlow<List<LocalDateTime>>(emptyList())
    val availableSlots: StateFlow<List<LocalDateTime>> = _availableSlots.asStateFlow()
    
    private val _bookingStatus = MutableStateFlow<BookingStatus>(BookingStatus.Idle)
    val bookingStatus: StateFlow<BookingStatus> = _bookingStatus.asStateFlow()
    
    fun loadAvailableSlots(doctorId: String, date: LocalDate) {
        viewModelScope.launch {
            try {
                _availableSlots.value = repository.getAvailableSlots(doctorId, date)
            } catch (e: Exception) {
                _bookingStatus.value = BookingStatus.Error(e.message ?: "Unknown error")
            }
        }
    }
    
    fun bookAppointment(appointment: Appointment) {
        viewModelScope.launch {
            _bookingStatus.value = BookingStatus.Loading
            try {
                repository.bookAppointment(appointment)
                    .onSuccess { _bookingStatus.value = BookingStatus.Success(it) }
                    .onFailure { _bookingStatus.value = BookingStatus.Error(it.message ?: "Booking failed") }
            } catch (e: Exception) {
                _bookingStatus.value = BookingStatus.Error(e.message ?: "Unknown error")
            }
        }
    }
}

sealed class BookingStatus {
    object Idle : BookingStatus()
    object Loading : BookingStatus()
    data class Success(val appointment: Appointment) : BookingStatus()
    data class Error(val message: String) : BookingStatus()
}
```

### View

```kotlin
@Composable
fun AppointmentBookingScreen(
    viewModel: AppointmentViewModel = hiltViewModel()
) {
    val availableSlots by viewModel.availableSlots.collectAsState()
    val bookingStatus by viewModel.bookingStatus.collectAsState()
    
    var selectedDate by remember { mutableStateOf<LocalDate?>(null) }
    var selectedTime by remember { mutableStateOf<LocalDateTime?>(null) }
    
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        // Date picker
        DatePicker(
            selectedDate = selectedDate,
            onDateSelected = { date ->
                selectedDate = date
                date?.let { viewModel.loadAvailableSlots(doctorId, it) }
            }
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Time slots
        LazyRow {
            items(availableSlots) { slot ->
                TimeSlotItem(
                    timeSlot = slot,
                    isSelected = slot == selectedTime,
                    onTimeSelected = { selectedTime = slot }
                )
            }
        }
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Book button
        Button(
            onClick = {
                selectedTime?.let { time ->
                    val appointment = Appointment(
                        id = UUID.randomUUID().toString(),
                        patientId = currentPatientId,
                        doctorId = doctorId,
                        dateTime = time,
                        status = AppointmentStatus.PENDING
                    )
                    viewModel.bookAppointment(appointment)
                }
            },
            enabled = selectedTime != null
        ) {
            Text("Book Appointment")
        }
        
        // Status handling
        when (bookingStatus) {
            is BookingStatus.Loading -> LoadingIndicator()
            is BookingStatus.Success -> BookingSuccess()
            is BookingStatus.Error -> ErrorMessage((bookingStatus as BookingStatus.Error).message)
            else -> Unit
        }
    }
}
```

## Best Practices

1. **Separation of Concerns**
   - Keep business logic in ViewModel
   - UI logic in Composable functions
   - Data operations in Repository

2. **State Management**
   - Use StateFlow for observable state
   - Handle loading and error states
   - Use sealed classes for state representation

3. **Error Handling**
   - Implement proper error handling in Repository
   - Show user-friendly error messages
   - Handle network errors gracefully

4. **Testing**
   - Write unit tests for ViewModel
   - Test Repository implementations
   - UI tests for Composable functions

## Next Steps

1. Learn about [State Management](./state-management.md)
2. Understand [Navigation](./navigation.md)
3. Study [Building MediLink App](./medilink-app.md)

> Tip: Start with a clear understanding of the data flow in your app. Draw diagrams to visualize the MVVM architecture before implementation.

> Note: MVVM works best when combined with other Android Architecture Components like LiveData, Room, and Hilt.
