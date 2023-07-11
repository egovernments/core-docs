---
description: 'Provider: a simplified state management solution'
---

# Provider State Management

Provider is a Flutter package that simplifies state management by offering a straightforward approach based on the InheritedWidget mechanism. It allows data to be passed down the widget tree efficiently and notifies dependent widgets when the data changes.

#### Key Concepts

* **ChangeNotifier**: A class that extends `ChangeNotifier` and represents the state. It provides the `notifyListeners()` method to notify listeners about state changes.
* **Provider**: An InheritedWidget that provides the state to its descendants. It listens to `ChangeNotifier` updates and rebuilds widgets that depend on the state.

#### Implementing Provider in Flutter

1. Add the `provider` package to your Flutter project's dependencies.
2. Create a class that extends `ChangeNotifier` to represent the state.
3. Wrap the root widget of your application with the `MultiProvider` widget to establish the provider hierarchy.
4. Within the widget tree, use `Provider.of<T>(context)` to access the state and rebuild widgets when the state changes.
5. Use `Consumer<T>` to consume the state and rebuild specific widgets when the state changes.

#### Working with ChangeNotifier

ChangeNotifier classes are responsible for holding the application state and notifying listeners about state changes. To update the state, modify the properties of the ChangeNotifier subclass and call `notifyListeners()`.

#### Consuming Provider using Provider.of and Consumer

* Use `Provider.of<T>(context)` to obtain the current state within a widget. It rebuilds the widget whenever the state changes.
* Use `Consumer<T>` to listen to changes in the state and rebuild only the specific subtree wrapped by the `Consumer` widget.

For more information , Go through the reference links of Provider :&#x20;

[Provider Tutorial](https://www.youtube.com/watch?v=L\_QMsE2v6dw)

[Provider State management in Flutter](https://medium.com/codechai/provider-state-management-in-flutter-d453e73537c5)
