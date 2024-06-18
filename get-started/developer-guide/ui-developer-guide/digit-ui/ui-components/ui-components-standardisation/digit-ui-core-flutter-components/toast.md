# Toast

## Overview

The Toast widget provides a customizable toast notification for Flutter applications. It is designed to display short-lived messages, alerts, or notifications to users in a visually appealing and informative manner.

The **ToastType** enumeration defines different types of toasts, including:

* success: Indicates a successful operation.
* error: Indicates an error or failure.
* warning: Indicates a warning or caution.

### **Properties**

The Toast widget provides a static method for displaying toasts. This method includes the following parameters:

```
Name                                Description
```

```
context(required)                  the build context for the widget
```

```
options(required)                  configuration options for the toast, such as the
                                   message and type
```

```
duration                           how long the toast message will be shown
                                   (default: 5 sec)
```

## **Configuration**

**Usage**

**Success Toast**

```
Toast.show(context,
options: DigitToastOptions(
"Your Success message", ToastType.success));
```

**Error Toast**

```
Toast.show(context,
options: DigitToastOptions(
"Your Error message", ToastType.error));
```

**Warning Toast**

```
Toast.show(context,
options: DigitToastOptions(
"Your Warning message", ToastType.warning));
```
