Brownian motion is observable when dust particles (here: red) follow random, erratic paths as they are pushed around by the invisibly small, but fast and numerous gas atoms or molecules. It's not only of interest in natural sciences but is also the keystone in [quantitative finance](https://en.wikipedia.org/wiki/Geometric_Brownian_motion).

It's initially hard to see how the small, fast particles impact the larger dust speckles, but in a minute or so the temperature cools and things slow down.

This [Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion) example shows physics capabilities of the versatile [d3.forceSimulation](https://github.com/d3/d3-force) in D3 4.0 which now uses [velocity Verlet integration](https://en.wikipedia.org/wiki/Verlet_integration).

D3 simulated forces are kept to a minimum: besides `d3.forceCollide` the only other force ensures that particles are not lost in space (perfectly bouncy walls of identical temperature).

A slow cooling is simulated by using a small non-zero value as `velocityDecay`.

Rendering is done on two superimposed `<canvas>` layers such that one can be continuously erased while the other shows a historical snail trail as if drawn with marker on a glass plane.

Built with [blockbuilder.org](http://blockbuilder.org)