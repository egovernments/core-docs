# Button

## Overview

DIGIT UI components provide a variety of buttons with optional suffix and prefix icons, contributing to a cohesive and visually appealing UI.

### Properties

**Button Type**

* Primary: Represents the primary action. It features a prominent colour, and its appearance can change on hover or click.
* Secondary: Offers a secondary action. It has a different colour scheme than the primary button.
* Tertiary: Provides a tertiary action with a distinct visual style.
* Link: Resembles a hyperlink, suitable for navigation or linking to other parts of the application. It typically includes an underline.

**Hover and Disabled State**

The DigitButton widget handles hover effects and a disabled state. When the button is hovered over, it can exhibit visual changes depending on its type. The disabled state prevents interaction and adjusts the button's appearance accordingly.

**Icon Placement**

The widget supports the placement of icons both before and after the label text. This allows for flexibility in button design.

**Properties**

It contains the following **required** Parameters:

```
Name                         Description
```

```
label(string)                text displayed on the button
```

```
onPressed(voidCallBack)     A callback function, when button is pressed
```

```
type                        specify the type of button(primary or secondary)
```

These are some optional parameters:

```
PrefixIcon                  Icon to be displayed before the label text
```

```
SuffixIcon                  Icon to be displayed after the label text
```

```
isDisabled                  indicates where the button is in a disabled state
```

## Configuration <a href="#id-9cct4ogihm4j" id="id-9cct4ogihm4j"></a>

### Primary Button <a href="#id-9cct4ogihm4j" id="id-9cct4ogihm4j"></a>

To use the primary button add the below lines of code:

```
Button(
  label: 'Primary Button',
  onPressed: () {},
  type: ButtonType.primary,
);
```

With suffix Icon:

```
Button(
  suffixIcon: Icons.add,
  label: 'Primary Button',
  onPressed: () {},
  type: ButtonType.primary,
);
```

With prefix Icon:

<pre><code>Button(
<strong>  prefixIcon: Icons.add,
</strong>  label: 'Primary Button',
  onPressed: () {},
  type: ButtonType.primary,
);
</code></pre>

### Secondary Button <a href="#t80p74rmzb20" id="t80p74rmzb20"></a>

To use the secondary button add the following lines of code:

```
Button(
  label: 'secondary Button',
  onPressed: () {},
  type: ButtonType.secondary,
);
```

Prefix and Suffix icons can be added to the secondary button using the same code as given for the primary button.

### Tertiary Button <a href="#j0zgnhqlc248" id="j0zgnhqlc248"></a>

To use the tertiary button add the below lines of code:

```
Button(
  label: 'tertiary Button',
  onPressed: () {},
  type: ButtonType.tertiary,
);
```

### Link <a href="#q13cttcv5ilz" id="q13cttcv5ilz"></a>

To use a link, add the following lines of code:

<pre><code>Button(
  label: 'link',
<strong>  onPressed: () {},
</strong>  type: ButtonType.link,
);
</code></pre>
