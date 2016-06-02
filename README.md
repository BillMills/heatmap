## heatmap

Heatmap is a lightweight canvas library meant to support rapid drawing of heatmaps with large numbers of bins.

### Usage

#### Basic

To create a new heatmap, declare a heatmap object, and add its `canvas` display to the dom:

```
hm = new heatmap(width_in_pixels, height_in_pixels);
document.body.appendChild(hm.canvas);
```

Assign data to plot to the `.raw` member variable:

```
hm.raw = myData
```

where data `myData` is an array of z values, packed like `[z_x0_y0, z_x1_y0, ..., z_x0_y1, z_x1_y1, ..., z_xmax_ymax]` (in other words, the first row in x, then the second row in x etc.)

finally, draw your heatmap:

```
hm.drawData().
```

A working example of this basic usage can be found in `demo.html`.

#### Optional

`heatmap` exposes a few options and features for doing fancier things:

 - **`heatmap.preRender`** can have a function assigned to it, which will be run before the final image is generated at each update.
 - **`heatmap.slowDataWarning`** can have a function assigned to it which is called twice: once before the heatmap cells are recalculated with the single argument `'on'`, and once after heatmap recalculation is complete, with the single argument `'off'`. Use this to notify the user that histogram redraw is in progress for particularly enormous histograms.
 - **An annotation layer** in the form of a canvas found on `heatmap.layers[1]`, and its corresponding 2D context at `heatmap.ctx[1]`; use this layer to add an overlay to your plot. In order to update your overlay without redrawing the data, call `heatmap.render()`.
 - **shift-click interaction.** A custom event called `'heatmap_shiftclick'` is dispatched to `heatmap.canvas` whenever the user clicks on the plot while holding shift. Add a [custom event listener](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events) for this event to create custom interactions with your plot. This custom event carries the following data:
 ```
 event.detail = {
    cell: {x: x_bin, y: y_bin}
 }
 ```
 where `x_bin` and `y_bin` are the bin numbers clicked on in x and y respectively.
 - **Labels and titles** can be assigned to the following keys:
   - `heatmap.plotTitle`: appears at the top of the plot
   - `heatmap.xaxisTitle`: label for x axis
   - `heatmap.yaxisTitle`: label for y axis
 - **heatmap.zoom(xmin, ymin, xmax, ymax)** will zoom the plot to the specifiex x and y ranges.

#### Interactions

`heatmap` supports the following default mouse interactions:

 - click and drag to zoom to a subset of the heatmap.
 - doubleclick to zoom out to the maximum x and y ranges of the data currently found on `heatmap.raw`.

Also see the customizable shift-click interaction specified above.

### Contributing

Contributions are very welcome! If you have an idea, question or comment, please open an issue. If you would like to make a change to this project, please follow these steps:
 - start by opening an issue or empty PR to discuss your ideas
 - please limit individual PRs to less than 500 lines (Why? See figure 1 [here](https://smartbear.com/SmartBear/media/pdfs/11_Best_Practices_for_Peer_Code_Review.pdf)).
 - please encapsulate all new behavior wherever possible in functions of 50 lines or less each.
 - note that `heatmap` is a performance-first, feature-minimal project; for a more feature complete charting library, see ex [plot.ly](https://plot.ly/).

