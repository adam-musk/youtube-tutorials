---
layout: "../../layouts/BlogPost.astro"
title: "CSS Grid Layout: A Crash Course for Beginners"
description: ""
pubDate: "2025-02-27"
youtubeVideoID: "p4Ith5qRM1g"
channel: ""
index: 14
---

# CSS Grid Layout: A Crash Course for Beginners

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/p4Ith5qRM1g" frameborder="0" allowfullscreen></iframe>


## Introduction to CSS Grid

Welcome to this crash course on CSS Grid, a powerful layout tool for web design. This chapter is designed for complete beginners who are new to CSS Grid or those who want to solidify their understanding. If you are already an expert in CSS Grid, this might not be the best use of your time.

This chapter builds upon the knowledge gained in HTML and CSS fundamentals, as well as concepts from Flexbox. While familiarity with Flexbox is not strictly required, understanding Flexbox will make learning CSS Grid significantly easier.  It's highly recommended to follow along with the examples provided throughout this chapter to maximize your learning.

By the end of this chapter, you will have a solid foundation in creating various webpage layouts using CSS Grid.

### What is CSS Grid?

The **CSS Grid Layout Module**, often referred to as **CSS Grid** or simply **Grid**, is a two-dimensional layout system for the web. It allows you to arrange elements in rows and columns, making it ideal for designing complex and responsive webpage layouts.

> **CSS Grid Layout Module (CSS Grid or Grid):** A powerful CSS module that enables two-dimensional layouts on web pages using a grid system of rows and columns. This allows for precise control over element placement and spacing in both horizontal and vertical directions.

While Flexbox excels at one-dimensional layouts (either rows or columns), CSS Grid truly shines when you need to control element placement in two dimensions simultaneously.  It simplifies the creation of intricate layouts that might be challenging to achieve with other CSS layout techniques. If you're already comfortable with HTML, CSS, and Flexbox, CSS Grid is the natural next step in mastering web layout design.

## Understanding CSS Grid Terminology

Before we dive into the properties of CSS Grid, it's crucial to understand the terminology. Grasping these terms will make learning and applying CSS Grid properties much easier.

### Key Terminology

*   **Grid Container:** The parent element on which CSS Grid is applied. It becomes the grid, and its direct children become grid items.

    > **Grid Container:** The HTML element to which the `display: grid` or `display: inline-grid` property is applied, making it the parent of all grid items and defining the grid layout.

    In HTML, this is typically a `div` element that wraps around other elements you want to arrange in a grid.

*   **Grid Items:** The direct child elements of the grid container. These are the elements that are positioned and sized within the grid.

    > **Grid Items:** The direct children of a grid container. These elements are placed and arranged within the grid according to the grid layout rules and properties.

    In the example structure, each of the child `div` elements within the parent container is a grid item.

*   **Grid Line:** The horizontal or vertical dividing lines in the grid. These lines define the boundaries of rows and columns.

    > **Grid Line:** The horizontal or vertical lines that form the structure of the CSS Grid, defining the boundaries of rows and columns. Grid lines are numbered starting from 1, and can be referenced when positioning grid items.

    Grid lines are numbered, starting from 1. Vertical grid lines are column grid lines, and horizontal grid lines are row grid lines.

*   **Grid Cell:** The smallest unit in a CSS Grid. It is the space created by the intersection of four grid lines (two horizontal and two vertical).

    > **Grid Cell:** The smallest rectangular unit of space in a CSS Grid, formed by the intersection of row and column grid lines. It is the basic building block within which grid items are placed.

*   **Grid Track:** The space between two adjacent grid lines. Tracks can be either columns (vertical) or rows (horizontal).

    > **Grid Track:** The space between two adjacent grid lines, either horizontally (row track) or vertically (column track). It represents a single row or column in the grid layout.

*   **Grid Area:** The total space surrounded by four grid lines. It can be composed of one or more grid cells.

    > **Grid Area:** A rectangular area on the grid defined by four grid lines, and can consist of one or more grid cells. Grid items can be placed and sized to occupy specific grid areas.

While memorizing these terms immediately isn't essential, understanding them is crucial for effectively using CSS Grid properties and referring to documentation.  The most fundamental concepts to grasp initially are **grid container** and **grid items**.

## Grid Container Properties

Working with CSS Grid primarily involves understanding the properties associated with the grid container and grid items. By mastering these properties, you can create sophisticated and flexible layouts.

This section will focus on the properties applied to the **grid container**. There are a total of 18 grid container properties, and this chapter will cover 16 of the most essential ones for beginners. The remaining two, while powerful, can be more complex for beginners and are recommended for later exploration.

### Essential Grid Container Properties

Here is a list of the grid container properties we will explore:

*   `display`
*   `grid-template-columns`
*   `grid-template-rows`
*   `grid-template`
*   `column-gap`
*   `row-gap`
*   `gap`
*   `justify-items`
*   `align-items`
*   `place-items`
*   `justify-content`
*   `align-content`
*   `place-content`
*   `grid-auto-flow`
*   `grid-auto-columns`
*   `grid-auto-rows`

Let's delve into each of these properties with practical examples.

### 1. `display` Property

The `display` property is fundamental and **mandatory** for creating a grid container. It defines an element as a grid container and enables the use of other CSS Grid properties on its children (grid items).

*   **`display: grid;`**:  Creates a **block-level grid container**. This means the grid container behaves like a block element, taking up the full width available in its parent container and starting on a new line.

    By default, when you set `display: grid;`, grid items are arranged in a single column and span the full width of the grid container.

*   **`display: inline-grid;`**: Creates an **inline-level grid container**. This makes the grid container behave like an inline element, only taking up the space necessary to contain its content. The width of the container will shrink to fit its children.

### 2. `grid-template-columns` Property

The `grid-template-columns` property specifies the number and width of columns in your grid layout.  You define column widths as a space-separated list of values.

*   **Fixed Width Columns:** You can define column widths using fixed units like pixels (`px`), points (`pt`), or centimeters (`cm`).

    ```css
    grid-template-columns: 100px 200px 300px;
    ```

    This creates three columns with widths of 100px, 200px, and 300px respectively. If you have more grid items than defined columns, they will wrap to the next row, maintaining the same column widths for subsequent rows.

*   **Equal Width Columns with `repeat()` function:** For creating multiple columns of the same width, the `repeat()` function is highly efficient.

    ```css
    grid-template-columns: repeat(3, 200px);
    ```

    This is equivalent to `grid-template-columns: 200px 200px 200px;` and creates three columns, each 200px wide. You can easily change the number of columns by modifying the first value in the `repeat()` function.

*   **Fractional Units (`fr`):** The `fr` unit represents a fraction of the available free space in the grid container. It's a flexible way to create responsive grid layouts.

    ```css
    grid-template-columns: 1fr 2fr 1fr;
    ```

    In this example, the available space is divided into four fractions (1 + 2 + 1). The first and third columns will each take up 1/4 of the space, while the second column will take up 2/4 (or 1/2) of the space.

*   **`minmax()` function:** The `minmax()` function allows you to set a minimum and maximum size for a grid track. This is useful for creating columns that are responsive within a certain range.

    ```css
    grid-template-columns: repeat(3, minmax(200px, 1fr));
    ```

    This creates three columns. Each column will be at least 200px wide, but will grow to take up an equal fraction of the available space if there's more space than needed for the minimum width. If the content requires more than the minimum width, the column will expand up to the fractional unit.

The `grid-template-columns` property provides a versatile way to define the column structure of your grid layout using various length units and functions.

### 3. `grid-template-rows` Property

The `grid-template-rows` property is analogous to `grid-template-columns`, but it defines the number and height of rows in your grid layout. The values you can use are similar to those for `grid-template-columns`.

*   **Fixed Height Rows:** Define row heights using fixed units.

    ```css
    grid-template-rows: 100px 150px 200px;
    ```

    This creates three rows with heights of 100px, 150px, and 200px respectively.

*   **Equal Height Rows with `repeat()` function:** Use `repeat()` for multiple rows of the same height.

    ```css
    grid-template-rows: repeat(3, 100px);
    ```

    This creates three rows, each 100px tall.

*   **Fractional Units (`fr`):**  Use `fr` units to make rows take up a fraction of the available vertical space within the grid container. This is particularly useful when the grid container has a defined height.

    ```css
    grid-template-rows: repeat(3, 1fr);
    height: 400px; /* Ensure grid container has a height */
    ```

    With a container height of 400px, this will create three rows that equally divide the 400px height.

The `grid-template-rows` property offers the same flexibility as `grid-template-columns` for defining the row structure of your grid.

### 4. `grid-template` Property

The `grid-template` property is a shorthand for setting both `grid-template-rows` and `grid-template-columns` in a single declaration.

The syntax is:

```css
grid-template: <grid-template-rows> / <grid-template-columns>;
```

*   **Defining Rows and Columns Together:**

    ```css
    grid-template: repeat(3, 1fr) / repeat(3, minmax(200px, 1fr));
    ```

    This sets `grid-template-rows` to `repeat(3, 1fr)` (three rows, each taking an equal fraction of vertical space) and `grid-template-columns` to `repeat(3, minmax(200px, 1fr))` (three columns, each at least 200px wide and growing to fill available space).

Using `grid-template` can streamline your CSS and make it easier to define both row and column structures in one place.

### 5. `column-gap` Property

The `column-gap` property specifies the size of the gap (gutter) between columns in the grid.

*   **Setting Column Gaps:**

    ```css
    column-gap: 20px;
    ```

    This creates a 20-pixel gap between all columns in the grid.

### 6. `row-gap` Property

The `row-gap` property specifies the size of the gap between rows in the grid.

*   **Setting Row Gaps:**

    ```css
    row-gap: 30px;
    ```

    This creates a 30-pixel gap between all rows in the grid.

### 7. `gap` Property

The `gap` property is a shorthand for setting both `row-gap` and `column-gap` in a single declaration.

The syntax is:

```css
gap: <row-gap> <column-gap>;
```

If you provide only one value, it applies to both row and column gaps.

*   **Setting Both Row and Column Gaps:**

    ```css
    gap: 40px 20px; /* row-gap: 40px; column-gap: 20px; */
    ```

    This sets a 40-pixel gap between rows and a 20-pixel gap between columns.

    ```css
    gap: 30px; /* row-gap: 30px; column-gap: 30px; */
    ```

    This sets a 30-pixel gap for both rows and columns.

The `gap` shorthand provides a convenient way to manage spacing between grid tracks.

### 8. `justify-items` Property

The `justify-items` property controls the alignment of grid items along the **row axis** (horizontally) within their grid cells. This property is applied to the grid container and affects all grid items within it.

Possible values for `justify-items`:

*   **`stretch` (default):** Grid items stretch to fill the entire width of their grid cell.
*   **`start`:** Grid items align to the start edge of their grid cell (left side in left-to-right languages).
*   **`end`:** Grid items align to the end edge of their grid cell (right side in left-to-right languages).
*   **`center`:** Grid items are centered horizontally within their grid cell.

### 9. `align-items` Property

The `align-items` property controls the alignment of grid items along the **column axis** (vertically) within their grid cells. This property is also applied to the grid container and affects all grid items.

Possible values for `align-items`:

*   **`stretch` (default):** Grid items stretch to fill the entire height of their grid cell.
*   **`start`:** Grid items align to the start edge of their grid cell (top side).
*   **`end`:** Grid items align to the end edge of their grid cell (bottom side).
*   **`center`:** Grid items are centered vertically within their grid cell.

### 10. `place-items` Property

The `place-items` property is a shorthand for setting both `align-items` and `justify-items` in a single declaration.

The syntax is:

```css
place-items: <align-items> <justify-items>;
```

If you provide only one value, it applies to both `align-items` and `justify-items`.

*   **Setting Both Vertical and Horizontal Alignment within Cells:**

    ```css
    place-items: start end; /* align-items: start; justify-items: end; */
    ```

    This aligns grid items to the top (start of column axis) and right (end of row axis) of their cells.

    ```css
    place-items: center; /* align-items: center; justify-items: center; */
    ```

    This centers grid items both vertically and horizontally within their cells.

The `place-items` shorthand simplifies the process of controlling item alignment within grid cells.

### 11. `justify-content` Property

The `justify-content` property controls the alignment of the **entire grid** along the **row axis** (horizontally) within the grid container when the total size of the grid is less than the size of the container along this axis.

Possible values for `justify-content`:

*   **`start` (default):** The grid is aligned to the start edge of the grid container (left side).
*   **`end`:** The grid is aligned to the end edge of the grid container (right side).
*   **`center`:** The grid is centered horizontally within the grid container.
*   **`stretch`:**  Grid tracks are resized to fill the width of the grid container. (Note: This may not always be visually apparent if tracks are already flexible).
*   **`space-between`:** Extra space is distributed evenly between grid columns. The first column is at the start edge, and the last column is at the end edge.
*   **`space-around`:** Extra space is distributed evenly around each grid column, including space before the first and after the last column. The space before the first and after the last column is half the size of the space between columns.
*   **`space-evenly`:** Extra space is distributed evenly between grid columns, and also before the first and after the last column. All spaces are of equal size.

### 12. `align-content` Property

The `align-content` property controls the alignment of the **entire grid** along the **column axis** (vertically) within the grid container when the total size of the grid is less than the size of the container along this axis.

Possible values for `align-content`: These are the same as `justify-content`:

*   **`start` (default):** The grid is aligned to the start edge of the grid container (top side).
*   **`end`:** The grid is aligned to the end edge of the grid container (bottom side).
*   **`center`:** The grid is centered vertically within the grid container.
*   **`stretch`:** Grid tracks are resized to fill the height of the grid container.
*   **`space-between`:** Extra space is distributed evenly between grid rows. The first row is at the start edge, and the last row is at the end edge.
*   **`space-around`:** Extra space is distributed evenly around each grid row.
*   **`space-evenly`:** Extra space is distributed evenly between grid rows, and also before the first and after the last row.

### 13. `place-content` Property

The `place-content` property is a shorthand for setting both `align-content` and `justify-content` in a single declaration.

The syntax is:

```css
place-content: <align-content> <justify-content>;
```

If you provide only one value, it applies to both `align-content` and `justify-content`.

*   **Setting Both Vertical and Horizontal Alignment of the Grid within the Container:**

    ```css
    place-content: start end; /* align-content: start; justify-content: end; */
    ```

    This aligns the grid to the top (start of column axis) and right (end of row axis) of the grid container.

    ```css
    place-content: center; /* align-content: center; justify-content: center; */
    ```

    This centers the grid both vertically and horizontally within the grid container.

`place-content` offers a concise way to manage the overall alignment of the grid within its container.

### 14. `grid-auto-flow` Property

The `grid-auto-flow` property controls how auto-placed grid items are inserted into the grid. Auto-placement happens when you haven't explicitly placed all grid items using grid item properties.

Possible values for `grid-auto-flow`:

*   **`row` (default):** Auto-placed items are inserted row by row. The grid fills in each row completely before moving to the next row.
*   **`column`:** Auto-placed items are inserted column by column. The grid fills in each column completely before moving to the next column.
*   **`row dense`:**  Uses the "row" auto-placement algorithm but attempts to fill in holes earlier in the grid if smaller items become available later. This can lead to items appearing out of order but can make the grid denser.
*   **`column dense`:** Uses the "column" auto-placement algorithm with the same "dense" packing behavior as `row dense`, but fills columns first.

For basic grid layouts, `row` and `column` are the most commonly used values. The `dense` values are more relevant for complex layouts where you need to optimize space utilization, potentially at the cost of visual order.

### 15. `grid-auto-columns` Property

The `grid-auto-columns` property specifies the default width of **implicitly created columns**. Implicit columns are created when you place a grid item outside of the explicitly defined grid (e.g., using `grid-column-start` or `grid-column-end` to place an item in a column that hasn't been defined by `grid-template-columns`).

If you don't set `grid-auto-columns`, the width of implicit columns is determined by the content of the grid items within them.

*   **Setting a Default Column Width:**

    ```css
    grid-auto-columns: 100px;
    ```

    This sets the default width of any implicitly created columns to 100px. This value will be overridden if you have explicitly defined column widths using `grid-template-columns`.

### 16. `grid-auto-rows` Property

The `grid-auto-rows` property is similar to `grid-auto-columns`, but it specifies the default height of **implicitly created rows**. Implicit rows are created when you place a grid item outside of the explicitly defined grid rows.

If you don't set `grid-auto-rows`, the height of implicit rows is determined by the content of the grid items within them.

*   **Setting a Default Row Height:**

    ```css
    grid-auto-rows: 200px;
    ```

    This sets the default height of any implicitly created rows to 200px. This value is overridden by explicitly defined row heights in `grid-template-rows`.

These `grid-auto-columns` and `grid-auto-rows` properties are useful for controlling the size of tracks created implicitly by item placement.

### Further Exploration: `grid-template-areas` and `grid` Properties

Once you are comfortable with the 16 properties discussed above, you can explore two more advanced grid container properties:

*   **`grid-template-areas`**: This property allows you to define grid areas by name and then assign grid items to those areas. It provides a more visual and semantic way to define grid layouts.
*   **`grid`**: This is a very comprehensive shorthand property that can set `grid-template-rows`, `grid-template-columns`, `grid-template-areas`, `grid-auto-rows`, `grid-auto-columns`, and `grid-auto-flow` in a single declaration. While powerful, it can be complex for beginners.

Understanding these 16 properties provides a strong foundation for working with CSS Grid and creating a wide range of layouts.

## Grid Item Properties

Now, let's shift our focus to the properties that are applied to **grid items**. These properties allow you to control the placement and alignment of individual grid items within the grid container.

### Essential Grid Item Properties

Here's a list of the grid item properties we will cover:

*   `grid-column-start`
*   `grid-column-end`
*   `grid-row-start`
*   `grid-row-end`
*   `grid-column`
*   `grid-row`
*   `justify-self`
*   `align-self`
*   `place-self`

Let's examine each of these properties in detail.

### 1. `grid-column-start` and `grid-column-end` Properties

These properties control the starting and ending column grid lines for a grid item, determining its horizontal placement and span within the grid.

*   **`grid-column-start`**: Specifies the column grid line where the grid item starts.
*   **`grid-column-end`**: Specifies the column grid line where the grid item ends.

You can use grid line numbers to specify these values. Grid lines are numbered starting from 1.

*   **Example:**

    ```css
    .item1 {
      grid-column-start: 1;
      grid-column-end: 3;
    }
    ```

    This makes `item1` start at column line 1 and end at column line 3, effectively spanning two columns.

You can also use the `span` keyword to indicate how many columns an item should span from its starting line:

*   **Using `span`:**

    ```css
    .item1 {
      grid-column-start: 1;
      grid-column-end: span 2; /* Spans 2 columns from line 1 */
    }
    ```

    This achieves the same result as the previous example, making `item1` span two columns starting from column line 1.

### 2. `grid-row-start` and `grid-row-end` Properties

These properties are analogous to `grid-column-start` and `grid-column-end`, but they control the starting and ending **row** grid lines for a grid item, determining its vertical placement and span.

*   **`grid-row-start`**: Specifies the row grid line where the grid item starts.
*   **`grid-row-end`**: Specifies the row grid line where the grid item ends.

Similar to column properties, you can use grid line numbers or the `span` keyword.

*   **Example:**

    ```css
    .item1 {
      grid-row-start: 1;
      grid-row-end: 3;
    }
    ```

    This makes `item1` start at row line 1 and end at row line 3, spanning two rows.

*   **Using `span`:**

    ```css
    .item1 {
      grid-row-start: 1;
      grid-row-end: span 2; /* Spans 2 rows from line 1 */
    }
    ```

    This also makes `item1` span two rows starting from row line 1.

### 3. `grid-column` Property

The `grid-column` property is a shorthand for setting both `grid-column-start` and `grid-column-end` in a single declaration.

The syntax is:

```css
grid-column: <grid-column-start> / <grid-column-end>;
```

*   **Setting Column Start and End in Shorthand:**

    ```css
    .item1 {
      grid-column: 1 / span 2; /* grid-column-start: 1; grid-column-end: span 2; */
    }
    ```

    This is equivalent to setting `grid-column-start: 1;` and `grid-column-end: span 2;`.

### 4. `grid-row` Property

The `grid-row` property is a shorthand for setting both `grid-row-start` and `grid-row-end` in a single declaration.

The syntax is:

```css
grid-row: <grid-row-start> / <grid-row-end>;
```

*   **Setting Row Start and End in Shorthand:**

    ```css
    .item1 {
      grid-row: 1 / span 2; /* grid-row-start: 1; grid-row-end: span 2; */
    }
    ```

    This is equivalent to setting `grid-row-start: 1;` and `grid-row-end: span 2;`.

The `grid-column` and `grid-row` shorthands provide a more concise way to control the placement and span of grid items.

### 5. `justify-self` Property

The `justify-self` property overrides the `justify-items` property for a **specific grid item**. It controls the alignment of a single grid item along the **row axis** (horizontally) within its grid cell.

Possible values for `justify-self`:

*   **`stretch` (default):** The grid item stretches to fill the width of its grid cell.
*   **`start`:** The grid item aligns to the start edge of its grid cell.
*   **`end`:** The grid item aligns to the end edge of its grid cell.
*   **`center`:** The grid item is centered horizontally within its grid cell.

*   **Example:**

    ```css
    .item2 {
      justify-self: end; /* Aligns item2 to the right of its cell */
    }
    ```

### 6. `align-self` Property

The `align-self` property overrides the `align-items` property for a **specific grid item**. It controls the alignment of a single grid item along the **column axis** (vertically) within its grid cell.

Possible values for `align-self`:

*   **`stretch` (default):** The grid item stretches to fill the height of its grid cell.
*   **`start`:** The grid item aligns to the start edge of its grid cell.
*   **`end`:** The grid item aligns to the end edge of its grid cell.
*   **`center`:** The grid item is centered vertically within its grid cell.

*   **Example:**

    ```css
    .item2 {
      align-self: start; /* Aligns item2 to the top of its cell */
    }
    ```

### 7. `place-self` Property

The `place-self` property is a shorthand for setting both `align-self` and `justify-self` for a specific grid item.

The syntax is:

```css
place-self: <align-self> <justify-self>;
```

If you provide only one value, it applies to both `align-self` and `justify-self`.

*   **Setting Both Vertical and Horizontal Self-Alignment:**

    ```css
    .item2 {
      place-self: start end; /* align-self: start; justify-self: end; */
    }
    ```

    This aligns `item2` to the top (start of column axis) and right (end of row axis) of its cell.

    ```css
    .item2 {
      place-self: center; /* align-self: center; justify-self: center; */
    }
    ```

    This centers `item2` both vertically and horizontally within its cell.

The `place-self` shorthand offers a convenient way to customize the alignment of individual grid items within their cells, overriding the container-level alignment properties.

## Conclusion

This crash course has provided a comprehensive introduction to CSS Grid layout. By understanding the terminology and mastering the properties discussed for both grid containers and grid items, you are now equipped to create a wide variety of web layouts with precision and flexibility.

Continue practicing and experimenting with these properties to solidify your understanding and unlock the full potential of CSS Grid in your web development projects. This knowledge serves as a strong foundation for further exploration into more advanced CSS Grid concepts and techniques.
