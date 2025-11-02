Optimistic UI Demonstration in Flutter

  This repository contains a simple Flutter application built to demonstrate the "Optimistic UI" pattern. The example features a 'Subscribe' button that provides immediate
  feedback to the user, creating a more responsive and seamless user experience, even when the underlying network request fails.

  

  What is Optimistic UI?

  Optimistic UI is a pattern where you update the user interface immediately after a user performs an action, assuming the operation (like a network request) will be successful.
  This avoids showing loading indicators and makes the application feel significantly faster.

   - The "Happy Path": The UI updates instantly, and the network request succeeds in the background. The user perceives the action as instantaneous.
   - The "Unhappy Path": The UI updates instantly, but the network request fails. The application then "rolls back" the UI to its previous state and notifies the user of the error.

  This approach dramatically improves the perceived performance and overall user experience.

  How It Works in This Project

  The pattern is implemented in the lib/subscribe_button.dart file.

   1. User Action: The user taps the Subscribe button.
   2. Optimistic Update: The SubscribeButtonViewModel immediately sets its state to subscribed = true and notifies the UI to rebuild. The button's appearance changes instantly.
   3. API Call: After updating the UI, it calls the SubscriptionRepository, which simulates a network request that is designed to fail after a 1-second delay.
   4. Rollback on Failure: When the failure is caught in a try-catch block, the ViewModel reverts the state to subscribed = false and uses a listener to trigger a SnackBar in the UI,
       informing the user of the failure.

  Here is the core logic from the SubscribeButtonViewModel:

    1 Future<void> subscribe() async {
    2   // Ignore taps when already subscribed
    3   if (subscribed) {
    4     return;
    5   }
    6 
    7   // 1. Optimistic state update
    8   subscribed = true;
    9   notifyListeners(); // Update the UI immediately
   10 
   11   try {
   12     // 2. Perform the actual operation
   13     await subscriptionRepository.subscribe();
   14   } catch (e) {
   15     // 3. If it fails, roll back the state
   16     subscribed = false;
   17     error = true; // Trigger an error message
   18   } finally {
   19     // 4. Notify listeners again to reflect the final state
   20     notifyListeners();
   21   }
   22 }

   - lib/main.dart: The entry point of the application, which sets up the main screen.
   - lib/subscribe_button.dart: Contains the core logic and widgets for this demonstration:
       - SubscribeButton: The StatefulWidget that displays the button.
       - SubscribeButtonViewModel: The ChangeNotifier that manages the state.
       - SubscriptionRepository: A mock repository to simulate API calls.
       - SubscribeButtonStyle: A helper class for button styling.
