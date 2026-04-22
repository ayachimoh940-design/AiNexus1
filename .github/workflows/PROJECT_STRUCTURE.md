# AI Nexus — Android Project Structure

```
AINexus/
├── app/
│   ├── build.gradle.kts
│   └── src/
│       ├── main/
│       │   ├── AndroidManifest.xml
│       │   ├── kotlin/com/ainexus/
│       │   │   ├── AINexusApp.kt                         # Application class
│       │   │   ├── MainActivity.kt                        # Single Activity host
│       │   │   │
│       │   │   ├── core/
│       │   │   │   ├── di/
│       │   │   │   │   ├── AppModule.kt
│       │   │   │   │   ├── NetworkModule.kt
│       │   │   │   │   ├── DatabaseModule.kt
│       │   │   │   │   └── RepositoryModule.kt
│       │   │   │   ├── network/
│       │   │   │   │   ├── ApiService.kt
│       │   │   │   │   ├── NetworkInterceptor.kt
│       │   │   │   │   └── NetworkResult.kt
│       │   │   │   ├── database/
│       │   │   │   │   ├── AINexusDatabase.kt
│       │   │   │   │   ├── dao/
│       │   │   │   │   │   ├── ConversationDao.kt
│       │   │   │   │   │   └── MessageDao.kt
│       │   │   │   │   └── entities/
│       │   │   │   │       ├── ConversationEntity.kt
│       │   │   │   │       └── MessageEntity.kt
│       │   │   │   ├── datastore/
│       │   │   │   │   └── UserPreferencesDataStore.kt
│       │   │   │   └── utils/
│       │   │   │       ├── Extensions.kt
│       │   │   │       └── Constants.kt
│       │   │   │
│       │   │   ├── domain/
│       │   │   │   ├── model/
│       │   │   │   │   ├── Conversation.kt
│       │   │   │   │   ├── Message.kt
│       │   │   │   │   ├── AIModel.kt
│       │   │   │   │   └── UserPreferences.kt
│       │   │   │   ├── repository/
│       │   │   │   │   ├── ChatRepository.kt
│       │   │   │   │   └── SettingsRepository.kt
│       │   │   │   └── usecase/
│       │   │   │       ├── SendMessageUseCase.kt
│       │   │   │       ├── GetConversationsUseCase.kt
│       │   │   │       ├── StreamResponseUseCase.kt
│       │   │   │       └── ManageModelsUseCase.kt
│       │   │   │
│       │   │   ├── data/
│       │   │   │   ├── repository/
│       │   │   │   │   ├── ChatRepositoryImpl.kt
│       │   │   │   │   └── SettingsRepositoryImpl.kt
│       │   │   │   ├── remote/
│       │   │   │   │   ├── dto/
│       │   │   │   │   │   ├── ChatRequestDto.kt
│       │   │   │   │   │   └── ChatResponseDto.kt
│       │   │   │   │   └── RemoteDataSource.kt
│       │   │   │   └── local/
│       │   │   │       └── LocalDataSource.kt
│       │   │   │
│       │   │   └── presentation/
│       │   │       ├── navigation/
│       │   │       │   ├── NavGraph.kt
│       │   │       │   └── Screen.kt
│       │   │       ├── theme/
│       │   │       │   ├── Color.kt
│       │   │       │   ├── Theme.kt
│       │   │       │   └── Type.kt
│       │   │       ├── components/
│       │   │       │   ├── MessageBubble.kt
│       │   │       │   ├── TypingIndicator.kt
│       │   │       │   ├── ModelSelector.kt
│       │   │       │   └── NexusTopBar.kt
│       │   │       ├── chat/
│       │   │       │   ├── ChatScreen.kt
│       │   │       │   ├── ChatViewModel.kt
│       │   │       │   └── ChatUiState.kt
│       │   │       ├── home/
│       │   │       │   ├── HomeScreen.kt
│       │   │       │   └── HomeViewModel.kt
│       │   │       └── settings/
│       │   │           ├── SettingsScreen.kt
│       │   │           └── SettingsViewModel.kt
│       │   │
│       │   └── res/
│       │       ├── values/strings.xml
│       │       └── xml/network_security_config.xml
│       │
│       └── test/ & androidTest/
│
├── build.gradle.kts             # Root build file
├── settings.gradle.kts
└── gradle/libs.versions.toml    # Version catalog
```
