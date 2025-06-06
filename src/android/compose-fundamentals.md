# Jetpack Compose Fundamentals

Jetpack Compose is Android's modern toolkit for building native UI. It simplifies and accelerates UI development with less code, powerful tools, and intuitive Kotlin APIs.

## What is Jetpack Compose?

Jetpack Compose is a declarative UI framework that allows you to build user interfaces by describing what you want to display, rather than how to display it. It's built on top of Kotlin and follows modern UI development patterns.

## Basic Composable Functions

### Simple Text Composable

```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello, $name!")
}

// Usage
@Composable
fun App() {
    Greeting("Android")
}
```

### Layout Composables

```kotlin
@Composable
fun ProfileCard(name: String, role: String) {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
    ) {
        Text(
            text = name,
            style = MaterialTheme.typography.h5
        )
        Spacer(modifier = Modifier.height(8.dp))
        Text(
            text = role,
            style = MaterialTheme.typography.body1
        )
    }
}
```

## Modifiers

Modifiers are used to modify the appearance and behavior of composables:

```kotlin
@Composable
fun ModifierExample() {
    Box(
        modifier = Modifier
            .size(200.dp)
            .background(Color.Gray)
            .padding(16.dp)
            .border(2.dp, Color.Black)
            .clickable { /* Handle click */ }
    ) {
        Text("Click me!")
    }
}
```

## State Management

### Remember and MutableState

```kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }
    
    Column(
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

### State Hoisting

```kotlin
@Composable
fun CounterScreen() {
    var count by remember { mutableStateOf(0) }
    
    Counter(
        count = count,
        onIncrement = { count++ },
        onDecrement = { count-- }
    )
}

@Composable
fun Counter(
    count: Int,
    onIncrement: () -> Unit,
    onDecrement: () -> Unit
) {
    Column {
        Text("Count: $count")
        Row {
            Button(onClick = onDecrement) {
                Text("-")
            }
            Button(onClick = onIncrement) {
                Text("+")
            }
        }
    }
}
```

## Lists and Grids

### LazyColumn (Vertical List)

```kotlin
@Composable
fun PatientList(patients: List<Patient>) {
    LazyColumn {
        items(patients) { patient ->
            PatientItem(patient)
        }
    }
}

@Composable
fun PatientItem(patient: Patient) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(8.dp)
    ) {
        Column(
            modifier = Modifier.padding(16.dp)
        ) {
            Text(patient.name)
            Text(patient.age.toString())
        }
    }
}
```

### LazyRow (Horizontal List)

```kotlin
@Composable
fun AppointmentTimeSlots(times: List<String>) {
    LazyRow {
        items(times) { time ->
            TimeSlot(time)
        }
    }
}
```

## Navigation

### Basic Navigation Setup

```kotlin
@Composable
fun MediLinkApp() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = "login"
    ) {
        composable("login") {
            LoginScreen(navController)
        }
        composable("home") {
            HomeScreen(navController)
        }
        composable("appointments") {
            AppointmentsScreen(navController)
        }
    }
}

@Composable
fun LoginScreen(navController: NavController) {
    // Login UI
    Button(
        onClick = { navController.navigate("home") }
    ) {
        Text("Login")
    }
}
```

## Practical Example: Appointment Booking Screen

Here's a practical example combining several Compose concepts:

```kotlin
@Composable
fun AppointmentBookingScreen(
    viewModel: AppointmentViewModel = viewModel()
) {
    var selectedDate by remember { mutableStateOf<LocalDate?>(null) }
    var selectedTime by remember { mutableStateOf<String?>(null) }
    
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        // Date Selection
        DatePicker(
            selectedDate = selectedDate,
            onDateSelected = { selectedDate = it }
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Time Slots
        LazyRow {
            items(viewModel.availableTimeSlots) { timeSlot ->
                TimeSlotItem(
                    timeSlot = timeSlot,
                    isSelected = timeSlot == selectedTime,
                    onTimeSelected = { selectedTime = timeSlot }
                )
            }
        }
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Book Button
        Button(
            onClick = {
                selectedDate?.let { date ->
                    selectedTime?.let { time ->
                        viewModel.bookAppointment(date, time)
                    }
                }
            },
            enabled = selectedDate != null && selectedTime != null
        ) {
            Text("Book Appointment")
        }
    }
}

@Composable
fun TimeSlotItem(
    timeSlot: String,
    isSelected: Boolean,
    onTimeSelected: () -> Unit
) {
    Card(
        modifier = Modifier
            .padding(4.dp)
            .clickable(onClick = onTimeSelected),
        backgroundColor = if (isSelected) MaterialTheme.colors.primary 
                         else MaterialTheme.colors.surface
    ) {
        Text(
            text = timeSlot,
            modifier = Modifier.padding(8.dp),
            color = if (isSelected) Color.White 
                   else MaterialTheme.colors.onSurface
        )
    }
}
```

## Best Practices

1. **Composable Organization**
   - Break down large composables into smaller, reusable components
   - Keep composables focused on a single responsibility
   - Use meaningful names for composables

2. **State Management**
   - Hoist state to the appropriate level
   - Use `remember` and `mutableStateOf` for UI state
   - Use ViewModel for business logic and data

3. **Performance**
   - Use `remember` to prevent unnecessary recompositions
   - Implement `key` for lists to optimize recomposition
   - Avoid expensive operations in composables

## Next Steps

1. Learn about [Composable Functions](./compose-functions.md)
2. Understand [State Management](./state-management.md)
3. Study [Navigation](./navigation.md)

> Tip: Start with simple UI components and gradually build more complex screens. Use the Android Studio preview to see your changes in real-time.

> Note: Jetpack Compose is still evolving. Keep an eye on the [official documentation](https://developer.android.com/jetpack/compose) for updates and best practices.
