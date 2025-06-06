# Android Studio Setup

This guide will help you set up your Android development environment. We'll install Android Studio and configure it for the MediLink project.

## Installing Android Studio

1. **Download Android Studio**
   - Visit [developer.android.com/studio](https://developer.android.com/studio)
   - Click "Download Android Studio"
   - Choose the appropriate version for your operating system

2. **Install Android Studio**
   - **Windows**: Run the downloaded `.exe` file
   - **macOS**: Open the `.dmg` file and drag Android Studio to Applications
   - **Linux**: Extract the downloaded file and run `studio.sh`

> Note: Make sure you have at least 8GB of RAM and 8GB of free disk space.

## First Launch Setup

1. **Welcome Screen**
   - Click "Next" to start the setup wizard
   - Choose "Standard" installation type
   - Select your UI theme (Light or Dark)

2. **SDK Components**
   - Android SDK
   - Android SDK Platform
   - Android Virtual Device (AVD)

> Tip: The download might take some time depending on your internet connection.

## Creating Your First Project

1. **New Project**
   - Click "New Project"
   - Select "Empty Activity"
   - Click "Next"

2. **Configure Project**
   ```kotlin
   Name: MediLink
   Package name: com.example.medilink
   Save location: Choose your preferred location
   Language: Kotlin
   Minimum SDK: API 24 (Android 7.0)
   ```

3. **Project Structure**
   ```
   app/
   ├── manifests/
   ├── java/
   │   └── com.example.medilink/
   │       ├── MainActivity.kt
   │       └── ui/
   └── res/
       ├── drawable/
       ├── layout/
       ├── mipmap/
       └── values/
   ```

## Configuring Gradle

1. **Project-level build.gradle**
   ```groovy
   buildscript {
       ext {
           compose_version = '1.4.0'
           kotlin_version = '1.8.0'
       }
   }
   ```

2. **App-level build.gradle**
   ```groovy
   plugins {
       id 'com.android.application'
       id 'kotlin-android'
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
   }

   dependencies {
       implementation "androidx.compose.ui:ui:$compose_version"
       implementation "androidx.compose.material:material:$compose_version"
       implementation "androidx.compose.ui:ui-tooling-preview:$compose_version"
       implementation "androidx.lifecycle:lifecycle-viewmodel-compose:2.6.1"
       implementation "androidx.navigation:navigation-compose:2.5.3"
   }
   ```

## Setting Up Git

1. **Initialize Git Repository**
   ```bash
   git init
   ```

2. **Create .gitignore**
   ```
   *.iml
   .gradle
   /local.properties
   /.idea
   /build
   /captures
   .externalNativeBuild
   .cxx
   ```

3. **Initial Commit**
   ```bash
   git add .
   git commit -m "Initial commit: Project setup"
   ```

## Testing Your Setup

1. **Create an Android Virtual Device (AVD)**
   - Click "Tools" > "Device Manager"
   - Click "Create Virtual Device"
   - Select a phone definition (e.g., Pixel 4)
   - Download and select a system image (e.g., API 33)
   - Complete the AVD creation

2. **Run the App**
   - Click the "Run" button (green play icon)
   - Select your AVD
   - Wait for the app to build and launch

> Warning: The first build might take several minutes as Gradle downloads dependencies.

## Next Steps

1. Learn [Kotlin Basics](./kotlin-basics.md)
2. Understand [Android Project Structure](./project-structure.md)
3. Start with [Jetpack Compose](./compose-fundamentals.md)

## Troubleshooting

Common issues and solutions:

1. **Gradle Sync Failed**
   - Check internet connection
   - Update Android Studio
   - Invalidate caches (File > Invalidate Caches)

2. **Emulator Not Starting**
   - Enable virtualization in BIOS
   - Update graphics drivers
   - Try a different system image

3. **Build Errors**
   - Clean project (Build > Clean Project)
   - Rebuild project (Build > Rebuild Project)
   - Check SDK installation

> Tip: Keep Android Studio and SDK tools updated for the best development experience.
