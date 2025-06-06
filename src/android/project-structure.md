# Android Project Structure

Understanding the Android project structure is crucial for maintaining a clean and organized codebase. This chapter explains the standard Android project structure and how it's organized in the MediLink app.

## Standard Android Project Structure

```
app/
├── manifests/
│   └── AndroidManifest.xml
├── java/
│   └── com.example.medilink/
│       ├── MainActivity.kt
│       ├── di/
│       ├── network/
│       ├── ui/
│       ├── utils/
│       └── viewmodel/
├── res/
│   ├── drawable/
│   ├── layout/
│   ├── mipmap/
│   └── values/
└── build.gradle
```

## Key Directories and Files

### 1. manifests/
Contains the `AndroidManifest.xml` file, which defines:
- App permissions
- Activities and components
- App metadata
- Minimum SDK version

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <application
        android:name=".MediLinkApplication"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.MediLink">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

### 2. java/
Contains all Kotlin/Java source files, organized by feature:

#### di/ (Dependency Injection)
```kotlin
// AppModule.kt
@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    @Singleton
    fun provideApiService(): ApiService {
        // Implementation
    }
}
```

#### network/ (API and Network)
```kotlin
// ApiService.kt
interface ApiService {
    suspend fun getGreeting(): GreetingResponse
    suspend fun login(credentials: LoginRequest): LoginResponse
    // Other API endpoints
}
```

#### ui/ (User Interface)
```kotlin
// screens/
├── auth/
│   ├── LoginScreen.kt
│   └── RegisterScreen.kt
├── home/
│   └── HomeScreen.kt
└── appointments/
    └── AppointmentScreen.kt

// components/
├── common/
│   ├── LoadingIndicator.kt
│   └── ErrorMessage.kt
└── appointment/
    └── AppointmentCard.kt
```

#### utils/ (Utility Classes)
```kotlin
// Extensions.kt
fun String.toDate(): Date {
    return SimpleDateFormat("yyyy-MM-dd", Locale.getDefault()).parse(this)
}

// Constants.kt
object Constants {
    const val BASE_URL = "https://api.medilink.com"
    const val TOKEN_KEY = "auth_token"
}
```

#### viewmodel/ (ViewModels)
```kotlin
// AuthViewModel.kt
class AuthViewModel @Inject constructor(
    private val authRepository: AuthRepository
) : ViewModel() {
    // Implementation
}
```

### 3. res/ (Resources)
Contains all app resources:

#### drawable/
- Vector drawables
- Image assets
- Icons

#### values/
```xml
<!-- colors.xml -->
<resources>
    <color name="primary">#FF6200EE</color>
    <color name="secondary">#FF03DAC5</color>
</resources>

<!-- strings.xml -->
<resources>
    <string name="app_name">MediLink</string>
    <string name="login">Login</string>
</resources>

<!-- themes.xml -->
<resources>
    <style name="Theme.MediLink" parent="Theme.MaterialComponents.DayNight">
        <!-- Theme attributes -->
    </style>
</resources>
```

## MediLink App Structure

The MediLink app follows a feature-based architecture:

```
app/
├── features/
│   ├── auth/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   ├── appointments/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   └── profile/
│       ├── data/
│       ├── domain/
│       └── presentation/
├── core/
│   ├── network/
│   ├── di/
│   └── utils/
└── ui/
    ├── theme/
    └── components/
```

### Feature Module Structure

Each feature module contains:

1. **data/**
   - Repository implementations
   - Data sources
   - API interfaces

2. **domain/**
   - Use cases
   - Repository interfaces
   - Domain models

3. **presentation/**
   - ViewModels
   - UI components
   - Screen composables

## Build Configuration

### Project-level build.gradle
```groovy
buildscript {
    ext {
        compose_version = '1.4.0'
        kotlin_version = '1.8.0'
    }
    dependencies {
        classpath "com.android.tools.build:gradle:7.4.2"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
```

### App-level build.gradle
```groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-kapt'
    id 'dagger.hilt.android.plugin'
}

android {
    compileSdk 33
    
    defaultConfig {
        applicationId "com.example.medilink"
        minSdk 24
        targetSdk 33
        versionCode 1
        versionName "1.0"
    }
    
    buildFeatures {
        compose true
    }
    
    composeOptions {
        kotlinCompilerExtensionVersion compose_version
    }
}

dependencies {
    // Core dependencies
    implementation "androidx.core:core-ktx:1.9.0"
    implementation "androidx.lifecycle:lifecycle-runtime-ktx:2.6.1"
    
    // Compose
    implementation "androidx.compose.ui:ui:$compose_version"
    implementation "androidx.compose.material:material:$compose_version"
    
    // Navigation
    implementation "androidx.navigation:navigation-compose:2.5.3"
    
    // Dependency Injection
    implementation "com.google.dagger:hilt-android:2.44"
    kapt "com.google.dagger:hilt-compiler:2.44"
}
```

## Best Practices

1. **Package Organization**
   - Group by feature, not by type
   - Keep related files together
   - Use clear, descriptive names

2. **Resource Management**
   - Use string resources for all text
   - Define colors in colors.xml
   - Use vector drawables when possible

3. **Code Organization**
   - Follow single responsibility principle
   - Keep files focused and small
   - Use meaningful names

4. **Build Configuration**
   - Define versions in ext block
   - Use consistent dependency versions
   - Enable only needed build features

## Next Steps

1. Learn about [Composable Functions](./compose-functions.md)
2. Understand [State Management](./state-management.md)
3. Study [Navigation](./navigation.md)

> Tip: Use Android Studio's "New Package" and "New File" features to maintain the correct project structure.

> Note: The project structure should evolve with your app's needs. Don't be afraid to reorganize as the app grows.
