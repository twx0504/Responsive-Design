# 01-Flexible Box Layout

- Conventional layout by `float` & `position` is well-supported and compatible, but is buggy.
  - Collapse issue.
  - Cumbersome when applying layout to mobile devices.
  - As a fallback to older browser support.
- Flexbox is easy to use, and simple to apply layout to mobile devices.

## Concepts

1. What is Flex?
2. What is flex containers and flex item?
3. What is the main axis and cross axis?
4. Default flex item behaviours

### What is Flex?

- flex is shortform of flexbox.
- a new css layout mode.
- flexbox gives the power to its children for alignment and space distribution.
- one-dimensional, deals only for row or column.

### What is flex containers and flex items?

- the element applied flex will be the flex containers, and all its direct children becomes flex items.
- display sets an element's inner and outer display types.
  - `display: flex;`: makes the flex container (parent) display block (outer type) and inner display type as flex.
  -  `display: inline-flex;`: makes the flex container (parent) display inline-block (outer type) and inner display type as flex - you can set height and width too, this is the difference from inline in which you can't.
-  any element can be set as flex.
-  no margin collapse in flex items (children). To know more,[Mastering_margin_collapsin](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing)
- `float`, `clear`, and `vertical align` will not work in flex item.


```html
<style>
    .flex-container {
        display: flex;
        
        background-color: skyblue;
    }

    .inline-flex-container {
      /* Width takes up as much as the total width occupied by its children. */
      /* Note you can also specify the width and height yourself. */
        display: inline-flex; 
      background-color: skyblue;
    }

    .flex-item {
        width: 100px;
        height: 100px;
        margin: 10px;
        background-color: pink;
    }
</style>

<body>
    <!-- Flex -->
    <div class="flex-container">
      <div class="flex-item">Flex Items</div>
      <div class="flex-item">Flex Items</div>
      <div class="flex-item">Flex Items</div>
      <div class="flex-item">Flex Items</div>
    </div>
    <br />
    <!-- Inline-Flex -->
    <div class="inline-flex-container">
      <div class="flex-item">Flex Items</div>
      <div class="flex-item">Flex Items</div>
      <div class="flex-item">Flex Items</div>
      <div class="flex-item">Flex Items</div>
    </div>
  </body>
```

![flex and inline flex](flex.png)

### What is main axis and cross axis?

- there's two axes in a flex container: the horizontal main axis and vertical cross axis.
- main start: starting point of main axis, main end: end point of main axis.
- cross start: starting point of cross axis, cross end: end point of cross axis.
- main size: the space in the main axis occupied by the single flex item, cross size: the space in the cross axis occupied by the single flex item.
- By default, flex items align along the main axis.

![axes](axes.png)

### Default flex item behaviours

- when we do not apply flex container / flex item related props, the default behaviours of flex items are as follow:
  - `flex-direction: row`
  - alignment along the main axis.
  - do not extend along the main axis, unless the flex container is too small, it will shrink to fit in.
  - extend to fit the size available in the cross axis when height is not specified (flex item height = container height when it is only single line). If specified height, display based on height set.
  - `flex-basis : auto;` : width as content width, unless specified AND the flex container is able to accomodate all flex items.
  - `flex-wrap: nowrap;`: do not wrap when there's no more space.

## Flex Container Properties

The following properties are set on the flex container (parent).

- `flex-direction` : set the direction of main axis (cross axis is not affected).
  - row (default): left to right
  - row-reverse: right to left
  - column: top to bottom
  - column-reverse: bottom to top
- `flex-wrap` : set whether the flex items will wrap onto multiple lines when there isn't enough space in the container to fit them all on a single line.
  - nowrap (default)
  - wrap
  - wrap-reverse
- `flex-flow: flex-direction flex-wrap`: shorthand property for `flex-direction` and `flex-wrap`.
  - default: row nowrap
- `justify-content`: set the alignment of flex items on the main axis. 
  - flex-start (default - though in MDN the initial value of justify-content is normal, and normal seems to have many meaning depending on the context of the layout mode)
  - flex-end
  - center
  - space-between
  - space-around
  - space-evenly
  > Confusion about the default value of justify content: [Default value of Justify Content](https://stackoverflow.com/questions/57720598/what-is-the-default-value-of-justify-content)
- `align-items`: set the alignment of flex items on the cross axis. (single line).  Note: The group of flex items is seemed to be the one entity.
  - stretch (default): when we do not set height on flex items or set as auto, the flex item will take up as much space as the container height.
  - flex-start
  - flex-end
  - center
  - baseline: all flex items align based on baseline (e.g., the baseline of the text) - rarely used.
  ![baseline alignment](baseline.png)
  > **Space Distribution between multiple flex lines.**
  ![space between flex line distribution](flexline.png)
  ```js
  // Question: How does the space occupation by each flex lines being calculated / distributed?
  const sharedSpacePerLine = flexContainerHeight - sumOfTheHighestFlexItemOfEachFlexLine / numberOfFlexLines;
  // 800px - 200px - 100px = 500 / 2 = 250 
  const flexLineSpace = highestFlexItem + sharedSpcePerLine;
  /*
   flex line 1: 
   200px (Highest Item) + 250px  (Shared Space)= 450px
  
   flex line 2: 
   100px (Highest Item) + 250px  (Shared Space)= 350 

   Therefore, this is why flex line 1 has more height compared to flex line 2.
   Note that the space occupied by each flex line is not necessarily equal. Though the shared space is evenly distributed.
   It is pretty much dependent on the tallest flex item on that line.
   */
  ```
- `align-content`: control the space between **flex lines** on the cross axis (multiple lines). If there's only one flex line, this property would not work.
  - stretch (Default)
  - flex-start
  - flex-end
  - center
  - space-between
  - space-around
  - space-evenly

> Note: **flex lines**** refers to the group of flex items that forms a single line after wrapping.


## Flex Item Properties

## 