# Info Card

This widget is a versatile and customizable information card designed inside a digit ui widget. It provides a visually appealing way to display information, with options for different types of information.

The Info Card supports different types of information, each with its distinct visual style:

* Info: Default information card with a blue background and an information icon.
* Success: Represents a successful operation, featuring a green background and a check-circle icon.
* Error: Indicates an error or unsuccessful operation with a red background and an error icon.
* Warning: Represents a warning or caution, featuring a yellow background and a warning icon.

Developers can include additional widgets beneath the description for extra information or interactive elements. The inline property controls whether these widgets are displayed horizontally or vertically.

**Properties:**

Info card have following **required** parameters:

```
Name                             Description
```

```
title                           title displayed on the top of the card
```

```
description                     detailed content associated with the card
```

```
type                             specify the type of information
```

There are some additional customisation parameters:

```
icon                             optional icon to display on card
```

```
additionalWidgets               a list of widget to display below description
```

```
inline                          determine whether additional widgets displayed inline
```

**Usages:**

**Info Card:**

<pre><code>InfoCard(
  title: 'Info',
  type: InfoType.info,
<strong>  Description: 'description'
</strong>);
</code></pre>

**Success Card:**

<pre><code>InfoCard(
  title: 'Success',
<strong>  type: InfoType.success,
</strong>  Description: 'description'
);
</code></pre>

**Error Card:**

```
InfoCard(
  title: 'Error',
  type: InfoType.error,
  Description: 'description'
);
```

**Warning Card:**

```
InfoCard(
  title: 'Warning',
  type: InfoType.warning,
  Description: 'description'
);
```
