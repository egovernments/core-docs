# Best Practices and Tips

### Flutter's coding conventions and style guidelines

Coding conventions and style guidelines help ensure that the codebase follows a consistent and readable structure. Consistency improves code collaboration, readability, and maintainability.

#### Naming Conventions

* Use camelCase for variable and function names. Start with a lowercase letter.
* Use PascalCase for class and enum names. Start with an uppercase letter.
* Use lowercase\_with\_underscores for constant names and file names.
* Use kebab-case for folder names
* Avoid using acronyms or abbreviations in names unless they are widely known.

#### Formatting and Indentation

* Use the Dart formatter (`dartfmt`) to automatically format code according to the Flutter style guide.
* Indent code with 2 spaces.
* Place a single space before and after binary operators.
* Use a single blank line to separate logical sections of code.

#### Testing and Unit Tests

* Write tests for critical functionality and complex logic using the Flutter testing framework.
* Organize tests into separate files following the same package structure as the production code.
* Name test files with the `component_test.dart` suffix.
* Use descriptive names for test cases and individual tests.

#### Comments and Documentation

* Use descriptive variable, function, and class names instead of relying heavily on comments.
* Write clear and concise comments that explain the intent and purpose of the code.
* Use comments sparingly and only when necessary to clarify complex or non-obvious logic.
* Document public APIs, classes, and functions using Dartdoc-style comments

#### Handling Assets and Resources

* Place assets, such as images and fonts, in the `assets` directory and specify them in the `pubspec.yaml` file.
* Use relative paths for referencing assets within the code.
