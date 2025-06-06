# Composable Functions

Composable functions are the building blocks of Jetpack Compose UI. This chapter explains how to create and use composable functions effectively in the MediLink app.

## What are Composable Functions?

Composable functions are Kotlin functions annotated with `@Composable` that describe a piece of UI. They can:
- Take parameters
- Maintain state
- Emit UI elements
- Be composed together

## Basic Composable Function

```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello, $name!")
}
```

## Composable Function Rules

1. **Function Parameters**
   - Can take any number of parameters
   - Should be immutable
   - Can include other composables as parameters

```kotlin
@Composable
fun UserProfile(
    name: String,
    age: Int,
    onEditClick: () -> Unit
) {
    Column {
        Text(text = name)
        Text(text = "Age: $age")
        Button(onClick = onEditClick) {
            Text("Edit Profile")
        }
    }
}
```

2. **Function Naming**
   - Use PascalCase
   - Be descriptive
   - Start with a noun

```kotlin
// Good
@Composable
fun ProfileCard() { ... }

// Bad
@Composable
fun profile() { ... }
```

3. **Function Organization**
   - Keep functions small and focused
   - Extract reusable parts
   - Use meaningful names

```kotlin
@Composable
fun AppointmentCard(
    appointment: Appointment,
    onCancel: () -> Unit
) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
    ) {
        Column(
            modifier = Modifier.padding(16.dp)
        ) {
            AppointmentHeader(appointment)
            AppointmentDetails(appointment)
            AppointmentActions(onCancel)
        }
    }
}

@Composable
private fun AppointmentHeader(appointment: Appointment) {
    Row(
        modifier = Modifier.fillMaxWidth(),
        horizontalArrangement = Arrangement.SpaceBetween
    ) {
        Text(
            text = appointment.doctorName,
            style = MaterialTheme.typography.h6
        )
        Text(
            text = appointment.date,
            style = MaterialTheme.typography.body2
        )
    }
}
```

## Composable Function Types

### 1. Stateless Composables
```kotlin
@Composable
fun StatelessButton(
    text: String,
    onClick: () -> Unit
) {
    Button(onClick = onClick) {
        Text(text)
    }
}
```

### 2. Stateful Composables
```kotlin
@Composable
fun StatefulCounter() {
    var count by remember { mutableStateOf(0) }
    
    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

### 3. Layout Composables
```kotlin
@Composable
fun LayoutExample() {
    Column(
        modifier = Modifier.fillMaxSize(),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text("Top")
        Spacer(modifier = Modifier.height(16.dp))
        Text("Middle")
        Spacer(modifier = Modifier.height(16.dp))
        Text("Bottom")
    }
}
```

## Common Composable Patterns

### 1. Conditional Rendering
```kotlin
@Composable
fun ConditionalContent(isLoading: Boolean) {
    if (isLoading) {
        CircularProgressIndicator()
    } else {
        Content()
    }
}
```

### 2. List Rendering
```kotlin
@Composable
fun AppointmentList(appointments: List<Appointment>) {
    LazyColumn {
        items(appointments) { appointment ->
            AppointmentCard(appointment = appointment)
        }
    }
}
```

### 3. Reusable Components
```kotlin
@Composable
fun MediLinkButton(
    text: String,
    onClick: () -> Unit,
    modifier: Modifier = Modifier,
    enabled: Boolean = true
) {
    Button(
        onClick = onClick,
        modifier = modifier,
        enabled = enabled,
        colors = ButtonDefaults.buttonColors(
            backgroundColor = MaterialTheme.colors.primary
        )
    ) {
        Text(text)
    }
}
```

## Best Practices

1. **Composition Over Inheritance**
   - Compose functions together
   - Avoid deep inheritance hierarchies
   - Use composition for reuse

2. **State Hoisting**
   - Lift state up to the caller
   - Make composables more reusable
   - Follow unidirectional data flow

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
```

3. **Side Effects**
   - Use `LaunchedEffect` for coroutines
   - Use `DisposableEffect` for cleanup
   - Handle side effects properly

```kotlin
@Composable
fun DataFetcher(
    onDataLoaded: (Data) -> Unit
) {
    LaunchedEffect(Unit) {
        val data = fetchData()
        onDataLoaded(data)
    }
}
```

4. **Performance Optimization**
   - Use `remember` for expensive calculations
   - Use `derivedStateOf` for derived state
   - Avoid unnecessary recompositions

```kotlin
@Composable
fun OptimizedList(items: List<Item>) {
    val sortedItems = remember(items) {
        items.sortedBy { it.name }
    }
    
    LazyColumn {
        items(sortedItems) { item ->
            ItemRow(item)
        }
    }
}
```

## Common Pitfalls

1. **Unnecessary Recomposition**
```kotlin
// Bad
@Composable
fun BadExample() {
    val expensiveValue = expensiveCalculation() // Recalculated on every recomposition
    
    Text(text = expensiveValue.toString())
}

// Good
@Composable
fun GoodExample() {
    val expensiveValue = remember {
        expensiveCalculation() // Calculated once and remembered
    }
    
    Text(text = expensiveValue.toString())
}
```

2. **State Management**
```kotlin
// Bad
@Composable
fun BadStateExample() {
    var count = 0 // State lost on recomposition
    
    Button(onClick = { count++ }) {
        Text("Count: $count")
    }
}

// Good
@Composable
fun GoodStateExample() {
    var count by remember { mutableStateOf(0) } // State preserved
    
    Button(onClick = { count++ }) {
        Text("Count: $count")
    }
}
```

## Next Steps

1. Learn about [State Management](./state-management.md)
2. Study [Navigation](./navigation.md)
3. Explore [MediLink App](./medilink-app.md)

> Tip: Use Android Studio's Compose Preview to visualize your composables while developing.

> Note: Composable functions should be pure and predictable. Avoid side effects and maintain immutability.
