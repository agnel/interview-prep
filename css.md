# CSS

[CSS Interview Questions](https://www.goskills.com/Development/Resources/CSS-interview-questions-answers#8)

## Specificity – knowledge about the concept and the strength of the CSS selectors

### Understanding CSS Specificity

**CSS specificity** is a system used by browsers to determine which CSS rules to apply when multiple rules could apply to the same element. It helps resolve conflicts and ensures that styles are applied in a predictable manner.

**Specificity** is calculated based on the types of selectors used in a CSS rule. The more specific a rule is, the higher its specificity score. Here’s how specificity is determined:

### Specificity Calculation

Specificity is calculated using a point system, which can be broken down into four categories:

1. **Inline Styles**: These have the highest specificity and override any styles defined in external or internal stylesheets. Inline styles are written directly within an element's `style` attribute.
   - Example: `<div style="color: red;">`

2. **IDs**: Selectors that use ID attributes are very specific and have high priority.
   - Specificity: `0, 1, 0, 0`
   - Example: `#header { color: blue; }`

3. **Classes, Attributes, and Pseudo-Classes**: These selectors are less specific than IDs but more specific than elements and pseudo-elements.
   - Specificity: `0, 0, 1, 0` for a class selector (e.g., `.menu { color: green; }`)
   - Specificity: `0, 0, 1, 0` for an attribute selector (e.g., `[type="text"] { color: purple; }`)
   - Specificity: `0, 0, 1, 0` for pseudo-classes (e.g., `:hover { color: orange; }`)

4. **Elements and Pseudo-Elements**: These selectors have the lowest specificity and are used to target HTML elements directly.
   - Specificity: `0, 0, 0, 1` for element selectors (e.g., `p { color: black; }`)
   - Specificity: `0, 0, 0, 1` for pseudo-elements (e.g., `::first-line { font-weight: bold; }`)

### Specificity Hierarchy

To determine which rule applies when multiple rules match an element, follow these steps:

1. **Calculate Specificity**: Each rule is assigned a specificity score based on the number of inline styles, IDs, classes/attributes/pseudo-classes, and element/pseudo-elements used.

2. **Compare Scores**: The rule with the highest specificity score wins. If two rules have the same specificity, the latter rule in the CSS (i.e., the one written last) will be applied.

### Example

Consider the following CSS:

```css
/* Rule A */
p { color: black; }

/* Rule B */
p.intro { color: blue; }

/* Rule C */
#special { color: red; }

/* Rule D */
p.intro#special { color: green; }
```

If you have an HTML element like this:

```html
<p id="special" class="intro">Hello World</p>
```

Here's how specificity applies:

1. **Rule A**: Specificity is `0, 0, 0, 1` (element selector).
2. **Rule B**: Specificity is `0, 0, 1, 1` (class selector + element selector).
3. **Rule C**: Specificity is `0, 1, 0, 0` (ID selector).
4. **Rule D**: Specificity is `0, 1, 1, 1` (ID selector + class selector + element selector).

**Rule D** has the highest specificity score of `0, 1, 1, 1`, so the text color of the `<p>` element will be green.

### Special Cases

- **Important Declarations**: Any CSS property marked with `!important` will override other declarations regardless of specificity. Use this sparingly as it can make debugging and maintaining CSS more challenging.
  ```css
  p { color: black !important; }
  ```

- **Specificity in Practice**: Sometimes, you might use a combination of selectors to achieve the desired level of specificity, such as `body .header h1` or using attribute selectors to increase specificity without adding IDs or inline styles.

Understanding CSS specificity helps in managing styles more effectively and avoiding conflicts or unexpected results in your web design.


## Box-model – what is it and how to manipulate it. Difference between inline and block elements.

### The CSS Box Model

The CSS Box Model is a fundamental concept in web design that describes the rectangular boxes generated for elements in the document tree. Each element is represented as a box that consists of several layers or components:

1. **Content**: This is the actual content of the element, such as text or an image.

2. **Padding**: Space between the content and the border. Padding is inside the element's box and can be used to create space between the content and the element’s border.

3. **Border**: Surrounds the padding (if any) and the content. Borders have width, style, and color, and can be used to create a visible line around the element.

4. **Margin**: Space outside the border, separating the element from other elements. Margins are used to create space between elements and can collapse in certain situations (e.g., vertical margins).

#### Diagram of the Box Model

```
+--------------------+
|      Margin        |
|  +--------------+  |
|  |   Border      |  |
|  |  +--------+  |  |
|  |  | Padding |  |  |
|  |  | +----+ |  |  |
|  |  | |    | |  |  |
|  |  | |Content| |  |
|  |  | +----+ |  |  |
|  |  +--------+  |  |
|  +--------------+  |
+--------------------+
```

### Manipulating the Box Model

You can manipulate the box model using various CSS properties:

- **Width and Height**: Define the size of the content area.
  ```css
  .box {
    width: 200px;
    height: 100px;
  }
  ```

- **Padding**: Set padding inside the element.
  ```css
  .box {
    padding: 10px; /* all sides */
    padding-top: 5px; /* specific side */
  }
  ```

- **Border**: Set the border around the element.
  ```css
  .box {
    border: 2px solid black; /* width style color */
  }
  ```

- **Margin**: Set the space outside the border.
  ```css
  .box {
    margin: 20px; /* all sides */
    margin-top: 10px; /* specific side */
  }
  ```

- **Box-Sizing**: Control how the width and height of an element are calculated (whether to include padding and border).
  ```css
  .box {
    box-sizing: border-box; /* includes padding and border in the width and height */
  }
  ```

  By default, the `box-sizing` property is set to `content-box`, meaning the width and height apply only to the content area, and padding and border are added to it.

### Inline vs. Block Elements

CSS elements are categorized into two primary display types: **inline** and **block**. These types determine how elements are laid out and how they interact with surrounding elements.

#### **Block Elements**

- **Characteristics**:
  - **Start on a New Line**: Block elements take up the full width available and start on a new line, pushing subsequent elements to the next line.
  - **Width and Height**: You can set the width and height of block elements.
  - **Examples**: `<div>`, `<p>`, `<h1>`, `<section>`, `<header>`, `<footer>`, `<form>`

- **Usage**: Typically used for structuring and layout purposes.

- **CSS Example**:
  ```css
  div {
    display: block;
    width: 100%;
    height: 50px;
  }
  ```

#### **Inline Elements**

- **Characteristics**:
  - **Do Not Start on a New Line**: Inline elements only take up as much width as necessary and flow within the line of surrounding text.
  - **Cannot Set Width/Height**: You cannot set width or height directly on inline elements; instead, they will adjust to their content.
  - **Examples**: `<span>`, `<a>`, `<strong>`, `<img>`, `<b>`

- **Usage**: Typically used for styling parts of text or small elements within a block.

- **CSS Example**:
  ```css
  span {
    display: inline;
    color: red;
  }
  ```

### **Differences Between Inline and Block Elements**

1. **Layout Behavior**:
   - **Block Elements**: Start on a new line and occupy the full width available.
   - **Inline Elements**: Flow within the content and do not break lines.

2. **Size Control**:
   - **Block Elements**: Allow width and height adjustments.
   - **Inline Elements**: Width and height are dictated by content.

3. **Margin and Padding**:
   - **Block Elements**: Margins and padding affect the element’s size and layout.
   - **Inline Elements**: Margins and padding are applied but affect only the horizontal spacing and do not influence the line height.

4. **Default Behavior**:
   - **Block Elements**: Typically used for structural purposes.
   - **Inline Elements**: Used for formatting within a line of text.

Understanding these differences helps in designing layouts and positioning elements effectively on a webpage.


## FlexBox – fluent using flex-box for positioning elements.

**Flexbox** (Flexible Box Layout) is a CSS layout module designed to help create flexible and responsive layouts. It simplifies the alignment and distribution of space among items in a container, even when their size is unknown or dynamic. Flexbox is particularly useful for creating complex layouts with ease.

### Basic Concepts of Flexbox

1. **Flex Container**: The element with `display: flex` or `display: inline-flex` applied to it. This container’s children become flex items.

2. **Flex Items**: The children of a flex container. They are laid out according to flexbox rules.

3. **Main Axis and Cross Axis**:
   - **Main Axis**: The primary axis along which flex items are laid out (e.g., horizontally if `flex-direction` is `row`).
   - **Cross Axis**: Perpendicular to the main axis (e.g., vertically if the main axis is horizontal).

### Key Properties for the Flex Container

1. **`display`**:
   ```css
   .container {
     display: flex; /* or inline-flex */
   }
   ```

2. **`flex-direction`**: Defines the direction flex items are placed in the flex container.
   ```css
   .container {
     flex-direction: row; /* default: horizontal left-to-right */
     /* row-reverse: horizontal right-to-left */
     /* column: vertical top-to-bottom */
     /* column-reverse: vertical bottom-to-top */
   }
   ```

3. **`flex-wrap`**: Controls whether flex items should wrap onto multiple lines.
   ```css
   .container {
     flex-wrap: nowrap; /* default: no wrapping */
     /* wrap: wrap onto multiple lines */
     /* wrap-reverse: wrap in reverse order */
   }
   ```

4. **`flex-flow`**: A shorthand for `flex-direction` and `flex-wrap`.
   ```css
   .container {
     flex-flow: row wrap; /* combines flex-direction and flex-wrap */
   }
   ```

5. **`justify-content`**: Aligns flex items along the main axis.
   ```css
   .container {
     justify-content: flex-start; /* default: items align at the start */
     /* center: items align at the center */
     /* flex-end: items align at the end */
     /* space-between: items with space between */
     /* space-around: items with space around them */
     /* space-evenly: equal space around items */
   }
   ```

6. **`align-items`**: Aligns flex items along the cross axis.
   ```css
   .container {
     align-items: stretch; /* default: items stretch to fill container */
     /* flex-start: items align at the start */
     /* center: items align at the center */
     /* flex-end: items align at the end */
     /* baseline: items align along their text baseline */
   }
   ```

7. **`align-content`**: Aligns flex lines within the flex container.
   ```css
   .container {
     align-content: stretch; /* default: lines stretch to fill container */
     /* flex-start: lines align at the start */
     /* center: lines align at the center */
     /* flex-end: lines align at the end */
     /* space-between: space between lines */
     /* space-around: space around lines */
   }
   ```

8. **`align-items`**: Aligns flex items on the cross axis.
   ```css
   .container {
     align-items: stretch; /* default: items stretch to fill container */
     /* flex-start: items align at the start of the cross axis */
     /* center: items align at the center of the cross axis */
     /* flex-end: items align at the end of the cross axis */
     /* baseline: items align along their text baseline */
   }
   ```

### Key Properties for Flex Items

1. **`flex-grow`**: Defines the ability for a flex item to grow if necessary.
   ```css
   .item {
     flex-grow: 1; /* item will grow to fill the container */
   }
   ```

2. **`flex-shrink`**: Defines the ability for a flex item to shrink if necessary.
   ```css
   .item {
     flex-shrink: 1; /* item will shrink if needed */
   }
   ```

3. **`flex-basis`**: Defines the default size of a flex item before any space distribution occurs.
   ```css
   .item {
     flex-basis: 200px; /* item starts at 200px */
   }
   ```

4. **`flex`**: A shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`.
   ```css
   .item {
     flex: 1 1 200px; /* grow, shrink, basis */
   }
   ```

5. **`align-self`**: Allows the default alignment (from `align-items`) to be overridden for individual flex items.
   ```css
   .item {
     align-self: center; /* item aligns to the center of the cross axis */
   }
   ```

### Examples of Flexbox Layouts

1. **Centering Items**:
   ```css
   .container {
     display: flex;
     justify-content: center; /* horizontally center items */
     align-items: center; /* vertically center items */
     height: 100vh; /* full viewport height */
   }
   ```

2. **Creating a Flex Row**:
   ```css
   .container {
     display: flex;
     flex-direction: row; /* default: items in a row */
     justify-content: space-between; /* space between items */
   }
   ```

3. **Creating a Flex Column**:
   ```css
   .container {
     display: flex;
     flex-direction: column; /* items in a column */
     justify-content: space-around; /* space around items */
   }
   ```

4. **Flex Wrapping**:
   ```css
   .container {
     display: flex;
     flex-wrap: wrap; /* items wrap onto multiple lines */
   }
   ```

### Conclusion

Flexbox simplifies the process of aligning and distributing space among items in a container. By understanding and applying the various flex properties, you can create flexible, responsive layouts that adjust to different screen sizes and content dynamically.

## Methodologies – basic knowledge about CSS methodologies and differences between them (ITCSS, SMACSS, BEM).


CSS methodologies provide structured approaches to writing and organizing CSS to improve maintainability, scalability, and readability. Each methodology has its own principles and practices to manage styles effectively, especially in larger projects. Here’s a basic overview of three popular CSS methodologies: ITCSS, SMACSS, and BEM.

### ITCSS (Inverted Triangle CSS)

**ITCSS** stands for **Inverted Triangle CSS**, and it's a methodology designed to help you structure your CSS in a scalable and maintainable way.

#### Key Concepts:

1. **Layered Structure**: ITCSS organizes CSS into layers, each representing a different level of specificity and scope. This inverted triangle structure helps in managing CSS in a scalable manner.

2. **Layers in ITCSS**:
   - **Settings**: Variables and configuration settings (e.g., color palettes, fonts).
   - **Tools**: Mixins and functions (often Sass or Less tools).
   - **Generic**: Base resets and global styles (e.g., `normalize.css` or `reset.css`).
   - **Elements**: Basic element styles (e.g., styling all `h1`, `p`, etc.).
   - **Objects**: Design patterns that are more reusable (e.g., grids, buttons).
   - **Components**: Specific UI components (e.g., card, modal).
   - **Trumps**: Utilities and helpers for overriding other styles (e.g., `.hidden`, `.text-center`).

3. **Purpose**: ITCSS helps to keep CSS organized, minimizes specificity conflicts, and improves maintainability by separating concerns and layering styles.

#### Example ITCSS Structure:
```css
/* 1. Settings */
$primary-color: #333;

/* 2. Tools */
@mixin border-radius($radius) {
  border-radius: $radius;
}

/* 3. Generic */
html, body {
  margin: 0;
  padding: 0;
}

/* 4. Elements */
h1 {
  font-size: 2em;
}

/* 5. Objects */
.grid {
  display: flex;
}

/* 6. Components */
.card {
  @include border-radius(8px);
  background-color: $primary-color;
}

/* 7. Trumps */
.hidden {
  display: none;
}
```

### SMACSS (Scalable and Modular Architecture for CSS)

**SMACSS** is a methodology that focuses on organizing CSS in a modular and scalable way, with an emphasis on categorizing styles into different types.

#### Key Concepts:

1. **Categories**:
   - **Base**: Default styles for elements (e.g., `body`, `h1`, `p`).
   - **Layout**: Styles for layout and structure (e.g., `header`, `footer`, `main`).
   - **Module**: Reusable components (e.g., `button`, `card`, `form`).
   - **State**: Styles for different states of modules (e.g., `.is-active`, `.has-error`).
   - **Theme**: Styles for different themes or variations (optional).

2. **Purpose**: SMACSS aims to make CSS more maintainable by dividing styles into categories and encouraging modular design. It helps in managing complex stylesheets by isolating changes.

#### Example SMACSS Structure:
```css
/* Base */
body {
  font-family: Arial, sans-serif;
}

/* Layout */
.header {
  background-color: #f8f8f8;
}

/* Module */
.button {
  padding: 10px 20px;
  border: none;
  background-color: #007bff;
  color: white;
}

/* State */
.button.is-active {
  background-color: #0056b3;
}

/* Theme (if used) */
.theme-dark .button {
  background-color: #333;
}
```

### BEM (Block Element Modifier)

**BEM** stands for **Block Element Modifier**, and it's a methodology for creating component-based CSS that is easy to read and maintain.

#### Key Concepts:

1. **Blocks**: Independent components or sections of a page (e.g., `menu`, `card`).
   ```css
   .menu {
     /* Block styles */
   }
   ```

2. **Elements**: Parts of a block that are dependent on it (e.g., `menu__item`, `card__title`).
   ```css
   .menu__item {
     /* Element styles */
   }
   ```

3. **Modifiers**: Variations of a block or element (e.g., `menu--large`, `card__title--highlighted`).
   ```css
   .menu--large {
     /* Modifier styles */
   }

   .card__title--highlighted {
     /* Modifier styles */
   }
   ```

4. **Purpose**: BEM aims to make CSS more modular and reusable by creating a clear structure for class names and separating styles into distinct components. It helps in avoiding conflicts and making styles more maintainable.

#### Example BEM Structure:
```css
/* Block */
.card {
  border: 1px solid #ddd;
  padding: 20px;
}

/* Element */
.card__title {
  font-size: 1.5em;
  color: #333;
}

/* Modifier */
.card--highlighted {
  border-color: #007bff;
}

.card__title--bold {
  font-weight: bold;
}
```

### Differences Between ITCSS, SMACSS, and BEM

1. **Structure**:
   - **ITCSS**: Focuses on a layered approach to CSS organization, aiming to manage specificity and maintainability.
   - **SMACSS**: Categorizes styles into different types, focusing on modularity and scalability.
   - **BEM**: Uses a naming convention to define components, elements, and modifiers, focusing on clarity and reusability.

2. **Approach**:
   - **ITCSS**: Emphasizes a structured hierarchy and separation of concerns.
   - **SMACSS**: Provides a flexible approach to organizing CSS, categorizing styles based on their purpose.
   - **BEM**: Focuses on a naming convention to make CSS more modular and understandable.

3. **Flexibility**:
   - **ITCSS**: More rigid in terms of structure, promoting a clear separation of styles.
   - **SMACSS**: Offers flexibility in categorizing styles, allowing for a variety of organizational strategies.
   - **BEM**: Strictly defines a naming convention that promotes consistency and avoids conflicts.

Choosing the right methodology depends on the specific needs of your project, team preferences, and the complexity of the styles you're managing. Each methodology has its own strengths and can be adapted or combined to fit different workflows.

