# forGRIDable - any-column grid system with CSS3 Grid layout and Custom Properties (variables)

Each `.grid` container can be the wrapper of a "whatever number of columns" grid system (12 by default but a single variable can transform independently each of them in a 2, 3, 4, (…), 42 or 1337-columns grid)

## How-to

Add the `grid` class to your container:

```html
<div class="grid">
  <div>grid item A</div>
  <div>grid item B</div>
  <div>grid item C</div>
  <div>(…)</div>
</div><!-- /.grid -->
```

You now have a - default - centered 12-column grid for resolutions above 576px with a maximum width of 1230px. All children elements are _grid items_ occupying 1/12<sup>th</sup> of their parent width with a gutter between them, both horizontally and vertically (`grid-gap`).

Everything except one parameter is customizable via CSS variables. Here are some examples:

A 16-column grid is as simple as:

```html
<div class="grid" style="--nb-col: 16">
  <div>(…)</div>
</div><!-- /.grid -->
```

Another grid - in the same page - can be a 5- or 24-column wide one by setting another value to `--nb-col` variable. This is useful when components like a site footer are very different from content or for different templates across your site(s).

If you don't want to use the style attribute, another longer way is adding your own class and creating a CSS rule:

```html
<div class="grid my-16-col">
  <div>(…)</div>
</div><!-- /.grid.my-16-col -->
```

```css
.my-16-col { --nb-col: 16; }
```

I'll stick to the --var-in-HTMLⓇ way of customizing forGRIDable from now on.

### Grid items

You'll most probably need grid items that span many columns of the grid, not just one column. Configure them with `--col`. For example:

```html
<div class="grid">
  <div style="--col: 6">
    half-wide
  </div>
  <div style="--col: 3">quarter</div>
  <div style="--col: 3">quarter</div>
  <div style="--col: 4">third</div>
  <div style="--col: 8">two thirds</div>
  <div>(…)</div>
</div><!-- /.grid -->
```

You can have grid items that span more than 1 *row* with `--row` variable: `<div class="--row: 3">a tall one</div>`.

Even more configuration of each grid item: you can *position* them so they start at a given column with `--col-start` and/or start at a certain row with `--row-start` (default values for each of them: `auto`, which is what you expect from a grid system).
Grid container has the default `grid-auto-flow: column` so be careful when using them.


## Support

CSS3 Grid layout is supported by modern browsers: Firefox, Chrome, Safari, Opera and Edge 16+. All of them also support CSS3 Custom properties.
We make sure they're the only browsers targeted by wrapping rules in an `@supports (grid-area: auto)` feature query at-rule.

*Not supported:* IE11 and Edge 12-15. They only support the first Grid layout syntax introduced by IE10 with its limitations; you'll need to add your own prefixed properties outside (and probably before) the @supports at-rule or do mostly nothing and _graceful degradation_ FTW).
Also not supported: any browser that doesn't support CSS3 Grid layout, any older version of browsers that didn't.
