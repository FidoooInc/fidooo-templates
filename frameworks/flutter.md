# 📱 Flutter

This repository defines a base structure for **Flutter** projects within the Fidooo ecosystem. It's designed to maximize scalability, maintainability, and development velocity using modern Flutter patterns and tools.

## 📋 Table of Contents

- [Directory Structure](#-directory-structure)
- [Technologies and Rationale](#-technologies-and-rationale)
  - [State Management → MobX](#-mobx)
  - [Navigation → Flutter Modular](#-flutter-modular)
  - [Internationalization → l10n](#-l10n)
  - [UI Components → Atomic Design](#-atomic-design)
  - [Data Serialization → Freezed + json_serializable](#-freezed--json_serializable)
  - [Local Database → Isar](#-isar)
  - [HTTP Client → Dio](#-dio)
  - [Dialog Management → SmartDialog](#-smartdialog)
  - [Code Generation → build_runner](#-build_runner)
  - [Testing → Flutter Test](#-flutter-test)

---

## 📁 Directory Structure

```bash
lib/
├── main.dart                          # Application entry point
├── firebase_options.dart              # Firebase configuration
├── app/                               # Main application logic
│   ├── app.dart                       # App configuration
│   ├── app_module.dart                # Main module
│   ├── data/                          # Data layer
│   │   ├── constants/                 # App constants
│   │   ├── data_sources/              # Remote & local data sources
│   │   ├── dtos/                      # Data transfer objects
│   │   ├── entities/                  # Domain entities (Freezed)
│   │   ├── isar_entities/             # Local database entities
│   │   ├── remote/                    # HTTP client (Dio)
│   │   └── repositories/              # Repository implementations
│   ├── modules/                       # Feature modules (Flutter Modular)
│   │   ├── chat_module/               # Chat functionality
│   │   ├── home_module/               # Home screen
│   │   ├── login_module/              # Authentication
│   │   ├── profile_module/            # User profile
│   │   ├── settings_module/           # App settings
│   │   └── splash_module/             # Splash screen
│   ├── stores/                        # Global state (MobX)
│   ├── widgets/                       # UI components (Atomic Design)
│   │   ├── atoms/                     # Basic components
│   │   ├── molecules/                 # Component combinations
│   │   ├── organisms/                 # Complex sections
│   │   └── wrappers/                  # Component wrappers
│   ├── guards/                        # Navigation guards
│   ├── layouts/                       # App layouts
│   ├── styles/                        # Themes and styles
│   └── utils/                         # Utilities and helpers
├── di/                                # Dependency injection
├── view/                              # Main view widgets
├── l10n/                              # Internationalization
└── gen/                               # Auto-generated files
```

### Key Architecture Components

#### 📁 `app/data/` - Data Layer
- **Remote**: Dio HTTP client with interceptors for authentication and logging
- **Local**: Isar database for offline-first functionality
- **Entities**: Freezed models for type safety and immutability
- **Repositories**: Clean architecture pattern with dependency injection

#### 📁 `app/modules/` - Feature Modules
- **Flutter Modular** for navigation and dependency injection
- **MobX controllers** for state management
- **Atomic design** components for UI consistency
- **Guards** for authentication and authorization

#### 📁 `app/stores/` - Global State
- **MobX stores** for reactive state management
- **Network connectivity** monitoring
- **User session** management
- **App-wide** state coordination

### Atomic Design

#### **Component Levels:**

1. **Atoms** - Basic building blocks
   - AppButton, AppTextField, AppText, AppIcon
   - No dependencies on other components
   - Highly reusable across modules

2. **Molecules** - Simple combinations of atoms
   - SearchBar (AppTextField + AppButton)
   - FormField (AppText + AppTextField + AppText)
   - AppCard (AppImage + AppText + AppButton)

3. **Organisms** - Complex sections
   - AppHeader (AppLogo + Navigation + UserMenu)
   - ProductGrid (multiple ProductCard)
   - AppFooter (Links + Social + Newsletter)

4. **Templates** - Page layouts
   - DashboardLayout, AuthLayout
   - Define structure, not content

5. **Pages** - Specific template instances
   - HomePage, UserProfilePage

---

## 🧰 Technologies and Rationale

### ✅ MobX

- **Reactive state management** that makes it easy to connect your app's reactive data to the UI.
- **Automatic synchronization** between state and UI without manual intervention.
- **Observable, Action, Computed** pattern for clean state management.
- **Perfect for Flutter** with excellent integration and performance.
- **Reduces boilerplate** compared to other state management solutions.
- Alternatives: Provider, Riverpod, Bloc.

### ✅ Flutter Modular

- **Modular architecture** for better code organization and scalability.
- **Dependency injection** built-in with automatic disposal.
- **Route management** with type-safe navigation.
- **Lazy loading** of modules for better performance.
- **Perfect for large applications** to avoid monolithic architecture.
- **Reduces technical debt** and improves maintainability.
- Alternatives: GetX, Auto Route, Go Router.

### ✅ l10n (Localization)

- **No-code translation solution** leveraging AI for automatic translations.
- **Type-safe translations** with generated code.
- **Multiple locale support** with fallback mechanisms.
- **Dynamic content translation** for user-generated content.
- **Seamless integration** with Flutter's localization system.
- Alternatives: easy_localization, get_storage.

### ✅ Freezed + json_serializable

- **Immutable data classes** with copyWith, toString, equality.
- **JSON serialization** with automatic code generation.
- **Union types/sealed classes** for better type safety.
- **Perfect for API responses** and local storage.
- **Reduces boilerplate** significantly.
- **Type-safe** with excellent IDE support.
- Alternatives: json_annotation, built_value.

### ✅ Isar

- **Fast NoSQL database** written in Dart.
- **Cross-platform** support for mobile and desktop.
- **Type-safe queries** with excellent performance.
- **Perfect for offline-first** applications.
- **Real-time queries** and reactive data.
- **Small footprint** and efficient memory usage.
- Alternatives: Hive, SQLite, ObjectBox.

### ✅ Dio

- **Powerful HTTP client** with interceptors for authentication, logging, and error handling.
- **Request/response transformers** for automatic JSON serialization.
- **File upload/download** with progress tracking and cancellation.
- **Timeout handling** and retry mechanisms with exponential backoff.
- **Perfect for REST APIs** and Firebase integration with automatic token management.
- **Request/response interceptors** for global error handling and authentication.
- **Type-safe** with excellent error handling and debugging capabilities.
- Alternatives: http, chopper, retrofit.

### ✅ SmartDialog

- **Modern dialog management** with beautiful animations.
- **Customizable dialogs** with rich content support.
- **Loading indicators** and toast messages.
- **Perfect for user feedback** and confirmations.
- **Easy to use** with minimal setup.
- **Consistent design** across the app.
- Alternatives: fluttertoast, rflutter_alert.

### ✅ build_runner

- **Code generation** for various Flutter packages.
- **Automatic file generation** for models, translations, assets.
- **Hot reload friendly** with incremental builds.
- **Perfect for** Freezed, json_serializable, l10n.
- **Reduces manual work** and potential errors.
- **Fast execution** with caching mechanisms.

### ✅ Flutter Test

- **Comprehensive testing framework** for Flutter applications.
- **Unit, widget, and integration tests** in one framework.
- **Perfect for** testing MobX stores and Flutter Modular routes.
- **Fast execution** with excellent debugging capabilities.
- **Golden tests** for visual regression testing.
- **Mocking support** for dependencies.
- Alternatives: Mockito, bloc_test.

---

This setup enables Fidooo to have a solid, modular, and scalable foundation for mobile applications. The architecture promotes clean separation of concerns, testability, and maintainability while leveraging the best Flutter ecosystem tools.

## 🎯 Key Benefits

- **Modular Architecture**: Scalable and maintainable codebase with Flutter Modular
- **Reactive State Management**: Automatic UI updates with MobX
- **Type Safety**: Immutable data models with Freezed
- **Offline-First**: Local database with Isar for better UX
- **Internationalization**: AI-powered translations with l10n
- **Clean Architecture**: Separation of concerns with dependency injection
- **Atomic Design**: Reusable and consistent UI components 