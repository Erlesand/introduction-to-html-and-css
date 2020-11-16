# Exercise: Layout using Flexbox

The goal of this exercise is to recreate a design, using Flexbox.

## Solution

- [HTML](layout-using-flexbox.html)
- [CSS](layout-using-flexbox.css)

## Explanation (HTML)

For the HTML we want to keep the markup as clean as possible, without adding a lot of extra elements. We also want to make use of the semantic elements, to make it easier to look at the HTML and understand what each section is used for.

In this exercise, we have got three different sections:

### Header

```html
<header>
  <div>Logo</div>

  <nav>
    <a href="#">Home</a>
    <a href="#">Products</a>
  </nav>

  <div>Profile</div>
</header>
```

The header contains three columns; a logo, navigation and a profile section. We use `<header>` to encapsulate the entire content, and then we use `<nav>` for the navigation section.

### Main (Category menu + Products)

```html
<section>
  <aside>
    <div>Category A</div>
    <div>Category B</div>
    <div>Category C</div>
  </aside>

  <main>
    <article>
      <div>Product A</div>
      <div>Product B</div>
      <!-- ... -->
    </article>
  </main>
</section>
```

The main section of the page contains two subsections: the category menu, and the page where the products are listed.

We wrap these two sections in a `<section>`, since we want to set the flex direction of the flex items to a row, instead of a column (which we use on `<body>`, since we want to stretch the main section to cover all of the available space that is left).

### Footer

```html
<footer>Footer</footer>
```

Finally, for the footer we use `<footer>` and just include a text.

## Explanation (CSS)

### Variables

In CSS we can create variables, and these can be either global or local. To create a global variable, which we can use in all our CSS rules, we define them on the `:root` element:

```css
:root {
  --spacing: 10px;
}
```

If we then want to use this value in our CSS file, we simply type: `var(--spacing)`, and it will replace this with `10px`. This is a nice little addition to CSS, which helps you making your code cleaner and easier to understand and modify. You can try changing the value from `10px` to `20px`, and watch the entire design get updated.

### Body

```css
body {
  display: flex;
  flex-direction: column;

  background: #ccc;
  min-height: calc(100vh - 2 * var(--spacing));
  margin: var(--spacing);
}

body * {
  background: white;
}
```

We make the `<body>` element a flex container, and set the flex direction to use columns (instead of rows which is the default value). We do this because we want a header on top, a footer at the bottom, another another section which should stretch and fill the space between the header and footer.

We need to set an explicit height of the body element in order for the flex container to fill the entire page even when there is not enough content. We do this by setting `min-height` to `calc(100vh - 2 * var(--spacing))`, where `100vh` means 100% of the view height, and we remove the space the margin will occupy (`2 * var(--spacing)`).

`body *` is used to set the background to white of all children of the body element.

### Header

```css
header {
  display: flex;
  justify-content: space-between;
  align-items: center;

  border: 1px solid black;
  padding: var(--spacing);
  margin-bottom: var(--spacing);
  height: 100px;
}

header > div {
  border: 1px solid black;
  padding: var(--spacing);
  line-height: 80px;
  width: 80px;
  text-align: center;
}
```

We also need to turn `<header>` to a flex container with `display: flex`, since it contains three flex items. We justify the content of these items with `justify-content: space-between`, since we want to place the logo and profile sections at the far ends. Finally we center the flex items vertically with `align-items: center`.

Note that since we want the flex items arranged in a row, we do not need to type `flex-direction: row` since this is the default value.

All of the direct `<div>` children of `<header>` we style via the selector `header > div`. We use `>` because we do not want to style any potential `<div>` which is used further down along the DOM tree branch.

### Expanding section

The expanding section contains two items, `<aside>` and `<main>`, where `<aside>` contains our side menu with the categories, and `<main>` contains the products belonging to a category.

### Aside

```css
aside {
  display: flex;
  flex-direction: column;

  border: 1px solid black;
  width: 200px;
  margin-right: var(--spacing);
  text-align: center;
}

aside > div {
  border: 1px solid black;
  margin: var(--spacing);
}
```

### Main

```css
main {
  display: flex;
  flex: 1;
  align-items: flex-start;

  border: 1px solid black;
}

main > article {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;

  width: 100%;
  padding: var(--spacing);
}

main > article > div {
  border: 1px solid black;
  width: calc(50% - var(--spacing) / 1.5);
  text-align: center;
  margin-bottom: var(--spacing);
}
```

For `<main>`, we turn this into a flex container and align all of our items at the top via `align-items: flex-start`.

We then have `<article>` which we use in order to set a wrap value via `flex-wrap: wrap`, so we only display two products on each row before wrapping.

Finally we have a rule for the products, here I set the width to `width: calc(50% - var(--spacing) / 1.5)`. The only reason I divide with 1.5 is to make the spacing look somewhat OK even if I increase the `--spacing` to e.g. 40px. For small values this is not needed though.

### Footer

```css
footer {
  display: flex;
  justify-content: center;
  align-items: center;

  margin-top: var(--spacing);
  border: 1px solid black;
  padding: var(--spacing);
  height: 100px;
}
```

Finally, for `<footer>`, I align the text both horizontally and vertically using `justify-content: center` and `align-items: center`.
