---
description: BLoC State Management with Bloc Consumer, Bloc Provider, and Bloc Listener
---

# BloC State Management

**BLoC (Business Logic Component)** is a state management pattern in Flutter that helps separate the business logic from the UI.&#x20;

It follows a unidirectional data flow, where the UI interacts with the BLoC to trigger **events**, and the BLoC emits new **states** that the UI can react to. In addition to the core BLoC pattern, the Flutter BLoC library provides useful widgets such as **Bloc Consumer**, **Bloc Provider**, and **Bloc Listener** to simplify the integration of BLoC in Flutter applications.

#### Key Concepts

* **BLoC**: The Business Logic Component represents the core logic of your application. It manages the state and exposes streams or methods to interact with that state.
* **Event**: An event is a user action or an external trigger that is passed to the BLoC. It can trigger state changes or other operations in the BLoC.
* **State**: The state represents the current condition of the application. It is emitted by the BLoC in response to events and reflects the data that the UI needs to display or react to.

#### Using Bloc Consumer

The `BlocConsumer` widget is a powerful tool for consuming the state emitted by a BLoC and rebuilding specific parts of the UI when the state changes.

1. Wrap the portion of your widget tree that depends on the BLoC state with the `BlocConsumer` widget.
2. Provide the BLoC instance and a builder function to define how the UI should be rebuilt based on the emitted state.
3. Inside the builder function, access the state and return the corresponding widget or widgets.

```
BlocConsumer<BlocType, StateType>(
  bloc: blocInstance,
  listener: (BuildContext context, StateType state) {
    // Perform side effects based on the emitted state
  },
  builder: (BuildContext context, StateType state) {
    // Build and return the widgets based on the emitted state
    return YourWidget();
  },
)
```

The `listener` parameter can be used to perform side effects and function calls based on the emitted state, such as showing a toast message or navigating to a different screen.

#### Using Bloc Provider

The `BlocProvider` widget is responsible for providing the BLoC instance to the widget tree and ensuring that it's accessible to all descendant widgets.

1. Wrap the root of your widget tree with `BlocProvider`.
2. Specify the BLoC type using the `create` parameter to create a new instance of the BLoC.
3. Access the BLoC instance using `BlocProvider.of<BlocType>(context)` within descendant widgets.

```
BlocProvider<BlocType>(
  create: (BuildContext context) => BlocInstance(),
  child: YourApp(),
)
```

#### Using Bloc Listener

The `BlocListener` widget is useful for listening to state changes emitted by the BLoC and performing side effects without rebuilding the UI.

1. Wrap the `BlocListener` widget around the portion of the widget tree that needs to listen to state changes.
2. Provide the BLoC instance and a listener function to handle state changes.

```
BlocListener<BlocType, StateType>(
  bloc: blocInstance,
  listener: (BuildContext context, StateType state) {
    // Perform side effects based on the state
```

For more information, Go through the reference links of Bloc Pattern

[Bloc State Management](https://blog.logrocket.com/state-management-flutter-bloc-pattern/)

[BloC State Management - Event, State , Bloc](https://www.youtube.com/watch?v=drkvsBh2ru8\&t=30s)

