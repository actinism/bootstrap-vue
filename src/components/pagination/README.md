# Pagination

> Quick first, previous, next, last, and page buttons for pagination control of another component
> (such as `<b-table>` or lists).

For pagination that navigates to a new URL, use the
[`<b-pagination-nav>`](/docs/components/pagination-nav) component instead.

```html
<template>
  <div class="overflow-auto">
    <div>
      <h6>Default</h6>
      <b-pagination size="md" :total-rows="100" v-model="currentPage" :per-page="10" />
    </div>

    <div class="mt-3">
      <h6>Small</h6>
      <b-pagination size="sm" :total-rows="100" v-model="currentPage" :per-page="10" />
    </div>

    <div class="mt-3">
      <h6>Large</h6>
      <b-pagination size="lg" :total-rows="100" v-model="currentPage" :per-page="10" />
    </div>

    <div class="mt-3">Current Page: {{ currentPage }}</div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        currentPage: 3
      }
    }
  }
</script>

<!-- b-pagination.vue -->
```

## Overview

`<b-pagination>` is a custom input component that provides a current page number input control. The
value should be bound via `v-model` in your app. Page numbers are indexed from 1. The number of
pages is computed from the provided prop values for `total-rows` and `per-page`.

## Customizing

`<b-pagination>` supports several props that allow you to customize the appearance.

### Props

| Prop                    | Description                                                                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `limit`                 | Limit the maximum number of displayed page buttons (including ellipsis if present, and excluding first/prev/next/last buttons) |
| `number-of-pages`       | The total number of pages                                                                                                      |
| `hide-ellipsis`         | never show ellipsis indicators                                                                                                 |
| `hide-goto-end-buttons` | never display goto first/last buttons                                                                                          |

And provides several props for setting the content of the bookend buttons:

| Prop            | Description                                                 |
| --------------- | ----------------------------------------------------------- |
| `first-text`    | The "goto first page" button text (plain html supported)    |
| `prev-text`     | The "goto previous page" button text (plain html supported) |
| `next-text`     | The "goto next page" button text (plain html supported)     |
| `last-text`     | The "goto last page" button text (plain html supported)     |
| `ellipsis-text` | the `...` indicator text (plain html supported)             |

Ellipsis indicator(s) will only be ever shown at the front and/or end of the page number buttons.
For `limit` values less than or equal to `3`, the ellipsis indicator(s) will never be shown for
practical display reasons.

**Note:** HTML is supported via the bookend content props. If allowing user supplied content to
populate these props, you should use named slots (see below) instead to avoid possible XSS attacks.

### Named slots

| Slot            | Description                                                          |
| --------------- | -------------------------------------------------------------------- |
| `first-text`    | The "goto first page" button text (html/sub-components supported)    |
| `prev-text`     | The "goto previous page" button text (html/sub-components supported) |
| `next-text`     | The "goto next page" button text (html/sub-components supported)     |
| `last-text`     | The "goto last page" button text (html/sub-components supported)     |
| `ellipsis-text` | the `...` indicator text (html/sub-components supported)             |

Ellipsis indicator(s) will only be ever shown at the front and/or end of the page number buttons.
For `limit` values less than or equal to `3`, the ellipsis indicator(s) will never be shown for
practical display reasons.

## Alignment

By default the pagination component is left aligned. Change the alignment to `center` or `right`
(`right` is an alias for `end`) by setting the prop `align` to the appropriate value.

```html
<template>
  <div class="overflow-auto">
    <div>
      <h6>Left alignment (default)</h6>
      <b-pagination :total-rows="100" v-model="currentPage" :per-page="10" />
    </div>

    <div class="mt-3 text-center">
      <h6>Center alignment</h6>
      <b-pagination align="center" :total-rows="100" v-model="currentPage" :per-page="10" />
    </div>

    <div class="mt-3 text-right">
      <h6>Right (end) alignment</h6>
      <b-pagination align="right" :total-rows="100" v-model="currentPage" :per-page="10" />
    </div>

    <div class="mt-3">Current Page: {{ currentPage }}</div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        currentPage: 3
      }
    }
  }
</script>

<!-- b-pagination-alignment.vue -->
```

## Small screen support

On smaller screens (i.e. mobile), some of the `<b-pagination>` buttons will be hidden to minimize
the potential of the pagination interface wrapping onto multiple lines:

- The ellipsis indicators will be hidden on screens `xs` and smaller.
- Page number buttons will be limited to a maximum of 3 visible on `xs` screens and smaller.

This ensures that no more than 3 page number buttons are visible, along with the goto _first_,
_prev_, _next_, and _last_ buttons.

## Accessibility

The `<b-pagination>` component provides many features to support assistive technology users, such as
`aria-` attributes and keyboard navigation.

### `aria-controls`

When pagination is controlling another component on the page (such as `<b-table>`), set the
`aria-controls` prop to the `id` of the element it is controlling. This will help non-sighted users
know what component is being updated/controlled.

### ARIA labels

`<b-pagination>` provides various `*-label-*` props which are used to set the `aria-label`
attributes on the various elements within the component, which will help users of assistive
technology.

| Prop               | `aria-label` content default                            |
| ------------------ | ------------------------------------------------------- |
| `label-first-page` | "Goto first page"                                       |
| `label-prev-page`  | "Goto previous page"                                    |
| `label-next-page`  | "Goto next page"                                        |
| `label-last-page`  | "Goto last page"                                        |
| `label-page`       | "Goto page", appended with the page number              |
| `aria-label`       | "Pagination", applied to the outer pagination container |

### Keyboard navigation support

`<b-pagination>` supports keyboard navigation out of the box.

- Tabbing into the pagination component will autofocus the current page button
- <kbd>LEFT</kbd> and <kbd>RIGHT</kbd> arrow keys will focus the previous and next buttons in the
  page list, respectively, and <kbd>ENTER</kbd> or <kbd>SPACE</kbd> keys will select (click) the
  focused page button

## Events

`<b-pagination>` provides two events that are emitted on the component:

- `input` is emitted anytime the current page changes (either programmatically or via user
  interaction)
- `change` is emitted only when the current page changes based on user interaction

Both events provide the single argument of the current page number (starting from 1)

## See Also

For navigation based pagination, please see the
[`<b-pagination-nav>`](/docs/components/pagination-nav) component.

<!-- Component reference added automatically from component package.json -->
