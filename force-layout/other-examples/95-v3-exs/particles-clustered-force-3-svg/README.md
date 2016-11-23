This variation of a [clustered force layout](/mbostock/1747543) uses an entry transition and careful initialization to minimize distracting jitter as the force simulation converges on a stable layout.

By default, D3’s [force layout](https://github.com/mbostock/d3/wiki/Force-Layout) randomly initializes node positions. You can prevent this by setting each node’s *x* and *y* properties before starting the layout. In this example, because custom forces cluster nodes by color, most of the initial jitter is caused by the initial random placement overlapping clusters. We can reduce the jitter by initially placing nodes of the same color near other.

The number of clusters in this example is defined by the variable *m*; the local variable *i* is the node’s cluster number. To initialize clusters in a circle of radius 200px around the canvas center, we can define *x* and *y* like so:

```js
x: Math.cos(i / m * 2 * Math.PI) * 200 + width / 2 + Math.random(),
y: Math.sin(i / m * 2 * Math.PI) * 200 + height / 2 + Math.random()
```

Each node is slightly offset from the corresponding cluster’s center using [Math.random](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random). Without this offset, same-colored nodes would be coincident, which would cause divide-by-zero problems for our custom forces.

This initialization strategy is arbitrary but effective. Many other approaches would work, such as D3’s [circle-packing layout](/mbostock/7882658), so feel free to experiment! A good strategy is one that is simple to implement, accelerates convergence, and avoids undesirable artifacts on the final layout. For example, a slightly simpler strategy is to initialize each cluster’s *x*-position along a line. However, this causes striations in the final layout.

As the force layout converges, its internal temperature cools; nodes move more slowly as the layout stabilizes. We can further reduce jitter by delaying the second custom force — collision prevention. This is done using a simple transition:

```js
node.transition()
    .duration(750)
    .delay(function(d, i) { return i * 5; })
    .attrTween("r", function(d) {
      var i = d3.interpolate(0, d.radius);
      return function(t) { return d.radius = i(t); };
    });
```

As the circles expand, the displayed radius (the `"r"` attribute) increases along with the internal `radius` data property that is used by the collision detection force.