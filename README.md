# CSS Grid

[Wes Bos](https://wesbos.com/) [CSS Grid Course](https://cssgrid.io/)

1. [Starter Files and Tooling Setup](#starter-files-and-tooling-setup)
1. [CSS Grid Fundamentals](#css-grid-fundamentals)
1. [CSS Grid Dev Tools](#css-grid-dev-tools)
1. [CSS Grid Implicit vs Explicit Tracks](#css-grid-implicit-vs-explicit-tracks)
1. [CSS grid-auto-flow](#css-grid-auto-flow)
1. [Sizing Tracks](#sizing-tracks)
1. [CSS Grid repeat function](#css-grid-repeat-function)
1. [Sizing Grid Items](#sizing-grid-items)
1. [Placing Grid Items](#placing-grid-items)
1. [Spanning and Placing Cardio](#spanning-and-placing-cardio)
1. [auto-fit and auto-fill](#auto-fit-and-auto-fill)
1. [Using minmax() for responsive grids](#using-minmax-for-responsive-grids)
1. [Grid Template Areas](#grid-template-areas)
1. [Area Line Names](#area-line-names)
1. [Naming Lines in CSS Grid](#naming-lines-in-css-grid)
1. [grid-auto-flow dense Block Fitting](#grid-auto-flow-dense-block-fitting)
1. [CSS Grid Alignment and Centering](#css-grid-alignment-and-centering)
1. [Reordering Grid Items](#reordering-grid-items)
1. [Nesting Grid with Album Layouts](#nesting-grid-with-album-layouts)
1. [CSS Grid Image Gallery](#css-grid-image-gallery)
1. [Flexbox vs CSS Grid](#flexbox-vs-css-grid)
1. [Recreating Codepen](#recreating-codepen)
1. [Bootstrappy Grid with CSS Variables](#bootstrappy-grid-with-css-variables)
1. [Responsive Website](#responsive-website)
1. [Full Bleed Blog Layout](#full-bleed-blog-layout)

## Starter Files and Tooling Setup

[See Live](https://sajakhtar.github.io/wesbos_css_grid/00-starter-files)

[Start files](https://github.com/wesbos/css-grid) available on Github.

Node.js is required in order to install the dependancies in the `package.json` file.

The dependancy we're installing is `browser-sync`, which allows us to run a local server, port 7777 in our case, and show the html file update in real time as we save changes to our files (saves us having to refresh the browser)

Within the `package.json` file, update the script section from Firefox Developer Edition to Firefox and/or update the file path to the `firefox.exe` file.

To install the dependancies, open terminal in the project folder and run:

```
npm i
```

To start `browser-sync`, run the following within the project folder within the terminal

```
npm start
```

## CSS Grid Fundamentals

[See Live](https://sajakhtar.github.io/wesbos_css_grid/02-css-grid-fundamentals)

`display: grid`on a `div` opens up the ability to slide and dice that `div` in to a grid, where we can place any child items anywhere on that grid within the columns and rows, collectively known as tracks.

For the grid to take effect, we need to define the columsns and rows using `grid-template-columns` and `grid-template-rows`. These can take `px`, percentages, `rem`, `auto` and the `fr` unit which will replace the need for percentages.

`auto` makes the column responsive to take up the remaining width of the container.

`grid-gap` is like margin, which we go inbetween the tracks (rows and cols).

## CSS Grid Dev Tools

[See Live](https://sajakhtar.github.io/wesbos_css_grid/03-dev-tools)

CSS Grid is difficult to visualize.

Using Firefox dev tools, we can inspect element and the layout tab will show all the grids we have. By checking the box on a grid container or a grid item, Firefox will outline the grid to make all the tracks (columns and rows) visual.

There are grid settings, where we can toggle on

- line numbers, helpful when placing items
- are names
- extend lines indefinitely

You can change the color of the grid overlay, and black is usually stands out well.

Tracks are numbered not by the column itself, but by the lines that start and stop them.

The solid line is the start and stop of the explicit grid.

The dashed diagonal lines are for the `grid-gap`.

The dashed lines are an explicit track i.e. from explicitly created columns/ rows.

The dotted lines are the implicit track i.e. implied part of the grid in the cases we've not specified columns/ rows.

## CSS Grid Implicit vs Explicit Tracks

[See Live](https://sajakhtar.github.io/wesbos_css_grid/04-implicit-vs-explicit-tracks)

Defining the columns means they're on explicit tracks, then CSS grid will wrap elements on to row if it runs out of space. In this case the rows are not defined and so the rows are on implicit tracks.

Sold line shows where the explicit grid has been started.

Dashed lines shows where the explicit columns/ rows have been created.

Dotted lines shows where the implicit columns/ rows have been created.

`grid-auto-rows` will define how big the rows are when they're been implicitly added i.e. wrapped. However, these rows will still be on implicit tracks.

There is also `grid-auto-columns`, though we will use `grid-auto-flow` to manage columns.

## CSS grid-auto-flow

[See Live](https://sajakhtar.github.io/wesbos_css_grid/05-grid-auto-flow)

`grid-auto-flow` determines if your new elements are added a rows or as columns. It's not something that would be used much.

`grid-auto-flow: column` adds extra items as columns rather than wrapping them on to new rows.

`grid-auto-flow: row` and `grid-auto-flow: dense` are options as well. For `dense` we first need to learn more about sizing items.

By specifying `grid-auto-colmns: ###px`, the extra elements will be set to the desired width i.e. any columns that have been implicitly created will be of the desired width. This will cause a horizontal scroll bar to appear, if the elements exceed the screen width.

There's not much of a use case for horizontal scrolling typically.

In Flexbox we can achieve a similar thing using `flex-direction` to be left to right, top to bottom or reverse of that. Though there is not reverse in CSS Grid.

## Sizing Tracks

[See Live](https://sajakhtar.github.io/wesbos_css_grid/06-sizing-tracks)

So far we've used `px` to size columns using `grid-template-columns` and we can also use percentages `%`.

It's better to use `fr` fractional unit instead of percentages or pixels.

Fractional units represent the amount of space left after all the elements are laid out. You can think of `fr` as free space.

CSS Grid will first layout all the of colums (rows) that have an explicit width (height), then use the use the fractional unit to size the remaining elements into columns (rows), taking up however much room is left.

This works similar to `flex-grow` and `flex-shrink` in Flexbox.

By using `fr` you would't need to use `px` or `%` at all.

Since the height of the elements depends on it's contents, `grid-template-rows: 1fr 1fr` would not work unless we gave the grid container a height for the elements to fill.

`grid-template-columns: auto 1fr` here `auto` will adjust to the maximum size of the contents across all the items, and the second column could take up the free space that remains.

## CSS Grid repeat function

[See Live](https://sajakhtar.github.io/wesbos_css_grid/07-repeat-function)

The repeat function takes 2 inputs:

1. how many times you'd like to repeat
2. what dimension to repeat

For example: `grid-template-columns: repeat(4, 1fr 2fr)` would repeat `1fr 2fr` four times to become `1fr 2fr 1fr 2fr 1fr 2fr 1fr 2fr`, giving 8 columns.

You can mix and match the `repeat` function with `px`, `auto`, `fr`.

The `repeat` function can be used anywhere inside `grid-template-columns` or `grid-template-rows` to cut down on the amount of typing that we need to do.

## Sizing Grid Items

[See Live](https://sajakhtar.github.io/wesbos_css_grid/08-sizing-grid-items)

We can size grid items that are within the grid container e.g. give an item a width, where that items width will define the width of the colum that item is in. Then the remaining columns will be divide the free space (or via any other criteria at the grid container level or width at the grid item level).

Better than giving grid items a fixed width, there is something called spanning in CSS Grid, where we can explicitly tell some of our items to be a specific width.

`grid-column: span 2` means the grid item will take up 2 columns.

`grid-row: span 2` means the grid item will take up 2 rows.

If the span excedes the possible columns available in a given row, then the element will move on to the next row, leaving some dead space for where it originally was.

If the span numnber of columns is greater than the original number of columns specified, then the extra columns are implicitly created.

This really shows the power of CSS Grid, as we're not using floats or absolute positioning to size grid items.

## Placing Grid Items

[See Live](https://sajakhtar.github.io/wesbos_css_grid/09-placing-grid-items)

Getting the items to actually go where we want can be achieved by specifying the underlying parameters of `grid-column` i.e. `grid-column-start: 2` and `grid-column-end: 5` giving them a track number to start and end at. The short-hand version is `grid-column: 2 / 5`.

You can also use `span` as well as a start/ end track e.g. `grid-column: span 2 / 5` which is span 2 columns and end at track 5; or `grid-column: 2 / span 3` start at track 2 and span 3 columns.

You can start at track 1 and always end at the last track, `grid-column: 2 / -1`.

The same applies for `grid-row`. Though here `-1` won't specify the last track unless it we've explicitly defined rows in the grid container.

If you specify `grid-column: 1 / -1` and `grid-row: 1 / -1` for a grid element, then that is essentially the entire explicit grid, which leaves no space for the rest of the elements, for which implicit tracks are created.

`-1` will only ever go to the end of the explicit grid, not the implict grid.

## Spanning and Placing Cardio

[See Live](https://sajakhtar.github.io/wesbos_css_grid/10-spanning-and-placing-cardio)

Practicing placing grid items.

## auto-fit and auto-fill

[See Live](https://sajakhtar.github.io/wesbos_css_grid/11-auto-fit-and-auto-fill)

`auto-fit`, `auto-fill` and `minmax()` are the most used parts of CSS Grid.

Insteand of specifying how many columns you want, you can use `auto-fill` e.g. ` grid-template-columns: repeat(auto-fill, 150px)`. The number of columns will depend on the screen size, so the columns reduce and increase as needed i.e. responsive.

`auto-fit` does the same thing as `auto-fill` in terms of appearance, but `auto-fit` will end the explicit grid at the last item, whill `auto-fill` will end the explicit grid based on how many more items can fit in that row for the given grid container size.

The benefit of the extended explicit grid with `auto-fill` allows use to place items anywhere within the grid container, while `auto-fit` doesn't since the explicit grid ends where the items end.

How do you know which one you want? Try one and if it's not the one that you want, then it's the other one.

## Using minmax() for responsive grids

[See Live](https://sajakhtar.github.io/wesbos_css_grid/12-minmax-for-responsive-grids)

The combination of using `auto-fit`, `auto-fill` and `minmax()` replaces the need for media queries, as these grid features make the page responsive by nature.

Being explicit about the column width can cause the content of the item to spill out if the column is too narrow.

We shouldn't have to figure out how wide our columns should be, they should flow as wide as they need to be. Here we can use `minmax(150px, 1fr)` which sets a minimum width as whatever you wish and a max width of `1fr` i.e. the entire width of the grid.

e.g. `grid-template-columns: repeat(auto-fill, minmax(150px, 1fr))`

As the grid gets smaller the items will wrap onto the next line if there isn't enough room for them based on the minimum width.

It's likely that we'd use `auto-fit` with `minmax()` i.e. `grid-template-columns: repeat(auto-fit, minmax(150px, 1fr))`. This will make the explicit grid space the entire width of the grid, with the elements strateching to take up the entire width as well, so no extra tracks.

Another grid feature is `fit-content()` function with a maximum width/height value. This can be used in sizing columns instead of the `auto` function. This is not something we'd use all that often other than in an edge case sizing scenario.

So `grid-template-columns: auto 150px 150px 150px` becomes `grid-template-columns: fit-content(100px) 150px 150px 150px`.

## Grid Template Areas

[See Live](https://sajakhtar.github.io/wesbos_css_grid/13-grid-template-areas)

We can place items based on grid areas by giving names to specific areas of our grid.

This can be done naming the the columns for each row. For example, if you have 3 columns and 3 rows, you could specify each square in the grid as follows:

```css
grid-template-areas:
  "sidebar-1    content     sidebar-2" /*row 1*/
  "sidebar-1    content     sidebar-2" /*row 2*/
  "footer       footer      footer"; /*row 3*/
```

Use `.` if you don't want to name a particualr square.

Now, when placing items, we don't need to worry about tracks, just specify the area name in `grid-area` for a given item.

We can then use media-queries to redefine the grid area config to make it responsive.

e.g.

```css
grid-template-areas:
  "content    content       content" /*row 1*/
  "sidebar-1    sidebar-1   sidebar-2" /*row 2*/
  "footer       footer      footer"; /*row 3*/
```

## Area Line Names

[See Live](https://sajakhtar.github.io/wesbos_css_grid/14-area-line-names)

When you create grid areas, you also get line names for free.

We don't have to define columns or rows, but simply define the grid area. And we don't always have use line numbers to size items. We can use the area name appended with `-start` and `-end` to reference the start and end lines of that areas, and so this can be used to size items.

e.g. `grid-column: 💩-start / 💩-end;`

## Naming Lines in CSS Grid

[See Live](https://sajakhtar.github.io/wesbos_css_grid/15-naming-lines)

It's possible to name the lines, though we don't need to name lines since they're available with `-start` and `-end`, once we define areas.

You can name the lines when you define the columns and rows.

e.g.

```css
grid-template-columns: [site-left] 1fr [content-start] 500px [content-end] 1fr [site-right];
```

We can add multiple names for a line too:

```css
grid-template-columns: [site-left sidebar-start] 1fr [sidebar-end content-start] 500px [content-end] 1fr [site-right];
```

Unufortunately, the Dev Tools don't show the names of the lines.

## grid-auto-flow dense Block Fitting

[See Live](https://sajakhtar.github.io/wesbos_css_grid/16-grid-auto-flow-dense-block-fitting)

When you have more items than can fit in the grid, by default the items will wrap onto the next line and create a new implicit row (or column if `grid-auto-flow: column` is specified).

The downside is that will be empty squars at the end of row if an item is to large for the square remainin in a row.

To fix this we use `grid-auto-flow: dense`, as allows the empty squares to be filled with other items that can fit.

This only make sense if you don't care about the the order of items. Though, CSS Grid will place the items that are required to be in specific spot first, then fill in the gaps with the remaining items.

Sometimes you will have gaps, simply because there may not be an item to fill that shape.

## CSS Grid Alignment and Centering

[See Live](https://sajakhtar.github.io/wesbos_css_grid/17-alignment-and-centering)

It's difficult to center things using CSS, while Flexbox made that easier, CSS Grid makes it easier again.

There are six properties to align things in CSS Grid:

```css
justify-items:
align-items:
justify-content:
align-content:
align-self:
justify-self:
```

**_Tips_**

- `justify-*` is row or x-axis
- `align-*` is column or y-axis
- `*-items` is within the explicit grid, at the grid container level
- `*-content` is wihtin the grid container, at the grid container level
- `*-self` allows us to overwrite alignment on case by case basis, at the grid item level

Unlike flexbox, the axis don't switch in CSS Grid.

[CSS-Tricks CSS Grid guide](https://css-tricks.com/snippets/css/complete-guide-grid/) is a good visual reference.

The default of `justify-items` is `stretch` which stretches the item across grid column. Using `center` ensure the item is only as wide as it needs to be and is at the center of the grid column. There is `start` and `end`, placing the items at the start or end of the grid column, while ensure the item is only as wide as it needs to be.

To use `align-items`, the rows must have a height.

- `center` places the item vertically center in the row
- `start` places the item at the start of the row
- `end` places the item at the end of the row

To perfectly center an item:

```css
justify-items: center;
align-items: center;
```

or use the CSS shorthand for `align-items` and `justify-items` respectively:

```css
place-items: center center;
```

If the grid is not as wide as the container, then `justify-content` and `align-content` can be used to define what happens with the extra space for columns

- `justify-content:start`is the default. Other options
- `start`
- `end`
- `center`
- `space-around` - takes the extra space and evenly divides on either side of each column
- `space-evenly` - similar to space-around
- `space-between` - takes the extra space and evenly divides it between columns, but not infront of first column or after last column

`align-content` can be used to define what happens with the extra space for rows

- `stretch` is the default
- `start`
- `start`
- `end`
- `center`
- `space-around` - takes the extra space and evenly divides on either side of each column
- `space-evenly` - similar to space-around
- `space-between` - takes the extra space and evenly divides it between columns, but not infront of first column or after last column

A fixed height on a grid is not as common as a fixed width on a grid.

`align-self` and `justify-self` allows us to overwrite alignment on case by case basis and is applied at the grid item level. They can take values of `start`, `end` and `center`.

Note that there is no `justify-self` in Flexbox.

This a great way to take what's in an element and vertically + horizontally center it.

```css
display: grid;
justify-content: center;
align-items: center;
```

## Reordering Grid Items

[See Live](https://sajakhtar.github.io/wesbos_css_grid/18-reordering-grid-items)

You can give your items an `order` property.

The `order` peroperty is useful in media queries.

The default `order` of everything is `0`.

Ordering will mess up the select and accessibility i.e. the order in which the screen reader will read it back to you, so it's not wise do change order of a paragraph tag within the content section for instnace.

## Nesting Grid with Album Layouts

[See Live](https://sajakhtar.github.io/wesbos_css_grid/19-nesting-grid-album-layout)

Fully responsive without media queries.

Each album `div` consists of

- artwork `img`
- album details `div`
  - album title `h2`
  - artist name `p`
  - album description `p`

Here `.albums` is the grid container and `.album` items are the grid items.

But, we can make each `.album` item a grid container also - nested grids

## CSS Grid Image Gallery

[See Live](https://sajakhtar.github.io/wesbos_css_grid/20-image-gallery)

An image gallery based on `grid-auto-flow: dense` and with a image overlay when an image in the gallery is clicked.

JavasScript is used to programmatically populate the HTML with 50+ image spanding upto 4 rows and 4 columns of the grid. In addition, we append a few images that span only 1 row and 1 column, to fill in the gaps in the dense grid.

Some JavaScript event listners are used to create an overlay when and is image is clicked and to close it the overlay.

## Flexbox vs CSS Grid

Here we go through a few design pattern examples for CSS Grid and Flexbox.

In general Grid can do everything that Flexbox can do.

One benefit of Flexbox over grid is that they can be transitioned i.e. animate a `flow-grow` value.
In Grid we can only transition `grid-gap`.

Grid is much more consistent across browsers with few bugs.
It's east to add more rows with Grid, even if you're starting with only a single axis.

We'd probably be using Grid more than Flexbox in the future.

Examples

- [Axis flipping](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/axis-flipping.html)
  - in Flexbox you have the ability to flip the axis from column to row
  - in Grid, `grid-template-columns: 1fr` will flip from column to row
  - Flexbox has the ability to reverse rows and columns, in Grid you would have to use the `order` property but that would be tedious
- [Controls on the right](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/controls-on-right.html)
  - use `grid-auto-flow: column` to add elements as new columns rather than rows
- [Flex on item](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/flex-on-item.html)
  - example for media controls for a video player
  - have the buttons take up as much space as they need, then remaining space will be taken up by the progress bar
  - Flexbox in this case is better
- [Perfectly centered](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/perfectly-centered.html)
  - In Flexbox, use `justify-content` and `align-items` with `flex-direction: column`
  - In Grid, use `justify-items` and `align-content`
- [Self control](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/self-control.html)
  - aligning items in all 4 corners, only possible in Grid, given that we have `justify-self`, as well as `align-self` that we can use on grid items
- [Stacked layout](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/stacked-layout.html)
  - Only possibl in Flexbox
  - Grid columns are rigid, so you'd need to do manual spanning for each grid item
  - However, there is no concept of flex-gap in Flexbox and using margins on Flex items is not ideal, as it leads to unintended margin on left and right, then you have to use negative margin to remove that - not ideal
- [Unknown content size](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/unknown-content-size.html)
  - If you know how many columns you have but don't know how wide items are and want to place it in the middle, then set the column widths to `auto` and use `justify-content: center`
- [Uknown number of items](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/unknown-number-of-items.html)
  - use `repeat(auto-fit, minmax(50px, 1fr))`
  - `auto-fit` will ensure the items that do exist, fill the width of the grid container
- [Variable widths each row](https://sajakhtar.github.io/wesbos_css_grid/21-flexbox-vs-css-grid/variable-widths-each-row.html)
  - Flexbox is a better use case, since the columns are rigid in Grid unless you manually span each grid item

## Recreating Codepen

[See Live](https://sajakhtar.github.io/wesbos_css_grid/22-recreating-codepen)

Creating an applicaiton with multiple window and scrolling, where these windows need to fit inside the viewport. Codepen is a great example of this.

THe HTML has four main parts

- Grid container: codepen
- Grid items:
  - pen (header)
  - code
  - preview
  - settings (footer)
- Then each grid item is a nested grid

## Bootstrappy Grid with CSS Variables

[See Live](https://sajakhtar.github.io/wesbos_css_grid/23-bootstrappy-grid-with-css-variables)

Grid by nature is flexible and responsive, while Bootstrap grid is rigid with 12 columns.

However, there are still valid cases for having a rigid grid system with equal sized columns.

Then we can use inline style for the span e.g.

```css
<div class="item" style="--span: 3">2</div>
```

## Responsive Website

[See Live](https://sajakhtar.github.io/wesbos_css_grid/24-responsive-website)

A responsive page consisting of

- hero image
- call to actions
- navigation - collapes into a menu button for smaller screen width
- columns for features
- feature spotlight
- image gallery e.g. from social posts

## Full Bleed Blog Layout

[See Live](https://sajakhtar.github.io/wesbos_css_grid/25-full-bleed-blog-layout)

CSS Grid is also good for laying out text.

In this case we have the main content, images, blockquotes, and `tip` text for the left/ right margin of the blog.
