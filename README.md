# AI Nexus — Android

> A production-ready, multi-provider AI chat application built with the Modern Android Development stack.

---

## ✨ Features

- **Multi-model support** — OpenAI, Anthropic, Google, Mistral, and local Ollama endpoints
- **Real-time streaming** — Server-Sent Events (SSE) with live token rendering
- **Persistent history** — All conversations stored locally via Room
- **Offline-first** — Full conversation history available without a network
- **Secure key storage** — API key persisted in encrypted DataStore (never logged)
- **Edge-to-edge UI** — Material 3, dark-first "deep space" palette
- **Swipe-to-delete** — Conversations dismissible with `SwipeToDismissBox`
- **Configurable** — Temperature, max tokens, system prompt all user-adjustable

---

## 🏗 Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                        Presentation Layer                        │
│  Composables  ←→  ViewModels (StateFlow / SharedFlow)            │
│  Navigation: Compose Navigation, type-safe Screen sealed class   │
└────────────────────────┬─────────────────────────────────────────┘
                         │ Domain models only
┌────────────────────────▼─────────────────────────────────────────┐
│                         Domain Layer                             │
│  Use Cases  ·  Repository Interfaces  ·  Pure Kotlin Models      │
└────────────────────────┬─────────────────────────────────────────┘
                         │ Implementations injected via Hilt
┌────────────────────────▼─────────────────────────────────────────┐
│                          Data Layer                              │
│  ChatRepositoryImpl  ·  SettingsRepositoryImpl                   │
│  RemoteDataSource (Retrofit + OkHttp SSE)                        │
│  LocalDataSource  (Room)  ·  UserPreferencesDataStore            │
└──────────────────────────────────────────────────────────────────┘
```

**Key patterns:**
- **Clean Architecture** — strict layer separation, domain has zero Android deps
- **MVVM** — `ViewModel` + `StateFlow` + `collectAsStateWithLifecycle`
- **Unidirectional Data Flow** — state flows down, events bubble up via `SharedFlow`
- **Repository pattern** — single source of truth per feature
- **Use Cases** — single-responsibility, testable business logic units

---

## 🛠 Tech Stack

| Concern | Library |
|---|---|
| UI | Jetpack Compose + Material 3 |
| Navigation | Compose Navigation |
| DI | Hilt (Dagger) |
| Async | Kotlin Coroutines + Flow |
| Networking | Retrofit 2 + OkHttp 4 + kotlinx.serialization |
| Persistence | Room 2.6 |
| Preferences | DataStore Preferences |
| Image loading | Coil |
| Logging | Timber |
| Testing | JUnit 4, MockK, Turbine, kotlinx-coroutines-test |

---

## 🚀 Getting Started

### Prerequisites
- Android Studio Hedgehog (2023.1.1) or newer
- JDK 17
- Android SDK 26+

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-org/ai-nexus-android.git
   cd ai-nexus-android
   ```

2. **Add your API key** (do NOT commit this)
   - Run the app, open Settings → enter your OpenAI (or other provider) API key
   - Or set a local property: add `OPENAI_API_KEY=sk-...` to `local.properties`

3. **Build and run**
   ```bash
   ./gradlew :app:installDevDebug
   ```

### Build flavors

| Flavor | Purpose |
|---|---|
| `devDebug` | Development, logging on, debug overlay |
| `devRelease` | Release-signed dev build |
| `prodRelease` | Store release build, minified |

---

## 📁 Package Structure

```
com.ainexus
├── AINexusApp.kt              Application class (Hilt entry point)
├── MainActivity.kt            Single Activity, edge-to-edge
├── core/
│   ├── database/              Room DB, DAOs, Entities
│   ├── datastore/             Preferences DataStore
│   ├── di/                    Hilt modules (Network, DB, Repository)
│   ├── network/               Retrofit, OkHttp, NetworkResult<T>
│   └── utils/                 Extensions, Constants
├── domain/
│   ├── model/                 Pure Kotlin domain models
│   ├── repository/            Repository interfaces
│   └── usecase/               Business logic use cases
├── data/
│   └── repository/            Repository implementations
└── presentation/
    ├── chat/                  ChatScreen + ChatViewModel
    ├── home/                  HomeScreen + HomeViewModel
    ├── settings/              SettingsScreen + SettingsViewModel
    ├── components/            Reusable Composables
    ├── navigation/            NavGraph + Screen sealed class
    └── theme/                 Color, Typography, Theme
```

---

## 🧪 Testing

```bash
# Unit tests
./gradlew :app:testDevDebugUnitTest

# Instrumented tests (requires device/emulator)
./gradlew :app:connectedDevDebugAndroidTest
```

Test coverage targets:
- ViewModels: 80%+ via MockK + Turbine
- Repositories: 70%+ via MockK
- Use cases: 90%+ (pure Kotlin, easiest to test)

---

## 🔒 Security

- API keys are stored in `DataStore` (encrypted by default on Android 6+)
- Keys are never written to logs (even in debug)
- `network_security_config.xml` blocks cleartext HTTP in production
- Debug builds allow user-installed certificates for Ollama / local LLMs

---

## 📄 License

```
Copyright 2024 AI Nexus

Licensed under the Apache License, Version 2.0
```
