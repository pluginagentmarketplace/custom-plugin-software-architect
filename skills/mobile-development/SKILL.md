---
name: mobile-development
description: Build mobile applications for iOS, Android, and cross-platform with React Native and Flutter. Learn native development, responsive UI design, performance optimization, and mobile-specific patterns. Use when developing mobile apps, learning iOS/Android, or cross-platform frameworks.
sasmp_version: "1.3.0"
bonded_agent: 01-frontend-development
bond_type: PRIMARY_BOND
---

# Mobile Development Skill

## Quick Start

Create mobile applications that work across iOS, Android, and web platforms.

### Path: Choose Platform → Learn Framework → Master Patterns

```kotlin
// Kotlin Android Development with Jetpack Compose
import androidx.compose.foundation.layout.Column
import androidx.compose.material.Button
import androidx.compose.material.Text
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember

@Composable
fun CounterApp() {
    var count by remember { mutableStateOf(0) }

    Column {
        Text(text = "Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

## What You'll Learn

### Foundation Level (Weeks 1-12)
- **Choose Path:** Native (iOS/Android) or Cross-platform (React Native/Flutter)
- **Mobile Basics:** Screen sizes, touch events, lifecycle, permissions
- **UI Design:** Mobile-first approach, responsive layouts
- **Testing:** Device testing, emulators, debug tools

### Intermediate Level (Weeks 13-32)
- **Framework Deep Dive:** React Native, Flutter, SwiftUI, Jetpack Compose
- **Data Persistence:** Local storage, databases, user preferences
- **Networking:** HTTP requests, APIs, real-time data
- **State Management:** Provider, Redux, Riverpod, BLoC

### Advanced Level (Weeks 33-52+)
- **Performance:** Memory optimization, battery, smooth animations
- **Native Integration:** Platform-specific features, sensors
- **App Store:** Submission process, store optimization
- **Advanced Patterns:** Dependency injection, architecture patterns

## Mobile Development Platforms

**Cross-Platform:**
- **React Native** - JavaScript, code sharing (iOS, Android, Web)
- **Flutter** - Dart, fast performance, beautiful UI
- **Capacitor** - Web-to-native bridge

**Native Development:**
- **iOS:** Swift, SwiftUI, UIKit, Xcode
- **Android:** Kotlin, Jetpack, Android Studio
- **Game Development:** Unity, Unreal Engine

## State Management Solutions

```dart
// Flutter Provider Pattern
final counterProvider = StateNotifier<int>((ref) => 0);

class Counter extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final count = ref.watch(counterProvider);

    return Scaffold(
      body: Center(
        child: Column(
          children: [
            Text('Count: $count'),
            ElevatedButton(
              onPressed: () => ref.read(counterProvider.notifier).state++,
              child: Text('Increment'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Learning Outcomes

After completing this skill:

✅ Build native iOS apps with Swift
✅ Build native Android apps with Kotlin
✅ Master React Native for cross-platform
✅ Master Flutter for cross-platform
✅ Design responsive mobile UIs
✅ Implement local data persistence
✅ Integrate with backend APIs
✅ Optimize mobile performance
✅ Deploy to App Store and Google Play
✅ Handle platform-specific requirements

## Project Examples

1. **To-Do List App** - Basic CRUD, local storage
2. **Weather App** - API integration, real-time data
3. **Social Media Feed** - Complex UI, infinite scroll
4. **Navigation App** - Maps integration, geolocation
5. **Game with Leaderboard** - Game engine, backend integration

## Performance Optimization

```typescript
// React Native Performance Tips
import React, { memo, useCallback } from 'react';
import { FlatList } from 'react-native';

// Memoize components
const ListItem = memo(({ item, onPress }) => (
  <TouchableOpacity onPress={onPress}>
    <Text>{item.name}</Text>
  </TouchableOpacity>
));

// Use useCallback for stable references
const handleItemPress = useCallback((id) => {
  navigation.navigate('Detail', { id });
}, [navigation]);

// Use FlatList key extractors
<FlatList
  data={items}
  keyExtractor={(item) => item.id}
  renderItem={({ item }) => (
    <ListItem item={item} onPress={handleItemPress} />
  )}
  removeClippedSubviews={true}
  initialNumToRender={10}
/>
```

## Platform-Specific Features

**iOS:**
- Notch/Safe Area handling
- App Clips, Widgets, HealthKit
- ARKit, VisionKit
- HomeKit, HealthKit
- Siri integration

**Android:**
- Material Design 3
- Jetpack Compose
- Health Connect API
- NFC/Biometric
- Google Play Services

## When to Use This Skill

- Building iOS applications
- Building Android applications
- Cross-platform mobile development
- Mobile game development
- Learning reactive programming
- Integrating with native features
- App Store/Google Play submission
- Mobile performance optimization

## Related Agents

- **Frontend Agent** - React Native web patterns
- **Backend Agent** - API design for mobile
- **Infrastructure Agent** - Mobile deployment and CDN

## Resources

**Official Documentation:**
- React Native: https://reactnative.dev
- Flutter: https://flutter.dev
- iOS/Swift: https://developer.apple.com/swift
- Android/Kotlin: https://developer.android.com/kotlin

**Books:**
- *Flutter in Action* (Eric Windmill)
- *React Native in Action* (Nader Dabit)
- *Kotlin in Action* (Dmitry Jemerov)

**Courses:**
- Google Play Academy
- Apple Developer Training
- Udemy Mobile Courses
- freeCodeCamp Mobile
- Pluralsight

---

**Status:** Comprehensive mobile skill covering 7 roles and all major platforms
