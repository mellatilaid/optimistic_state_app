# Gemini Project Context: optimistic_state_app

## Project Overview

This is a Flutter project that demonstrates the "Optimistic UI" pattern. The core feature is a `SubscribeButton` that immediately updates its state to "Subscribed" upon being tapped, without waiting for confirmation from a simulated network request. If the request fails, the UI reverts to its original state and displays an error message.

The project is structured with a clear separation of concerns:

*   **Widget (`SubscribeButton`):** The UI component.
*   **ViewModel (`SubscribeButtonViewModel`):** Manages the state and business logic for the widget using `ChangeNotifier`.
*   **Repository (`SubscriptionRepository`):** Simulates the data layer, in this case, a network request that always fails after a delay.

The main technologies used are Flutter and Dart.

## Building and Running

### 1. Get Dependencies

First, ensure all project dependencies are downloaded and up-to-date.

```sh
flutter pub get
```

### 2. Run the Application

Run the app on a connected device or simulator.

```sh
flutter run
```

### 3. Run Tests

Execute the widget tests to ensure the UI behaves as expected.

```sh
flutter test
```

## Development Conventions

*   **State Management:** The project uses `ChangeNotifier` and `ListenableBuilder` for simple, local state management. This is a lightweight approach suitable for the current scale.
*   **Architecture:** The code follows a basic MVVM (Model-View-ViewModel) pattern, with the `SubscribeButtonViewModel` acting as the ViewModel.
*   **Styling:** Widget styles are encapsulated in a separate utility class (`SubscribeButtonStyle`) to keep the widget build methods clean.
*   **Linting:** The project uses the recommended lints from the `flutter_lints` package to enforce good coding practices. The configuration is in `analysis_options.yaml`.
*   **Testing:** The project includes a basic widget test in `test/widget_test.dart` that verifies the default counter functionality.

