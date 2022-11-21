# maplibre-3d-linestring-demo
Using custom layers to build a 3D line string for maplibre 3D maps.

This is a simple prototype for displaying 3D-lines with the help of custom WebGL-layers in Maplibre.
The code is based on the example in the Maplibre docs: [Add a custom style layer](https://maplibre.org/maplibre-gl-js-docs/example/custom-style-layer/)

## Working principle

The 3D-coordinates of the path are passed to the vertex shader. It builds the track piece by piece between two coordinates. For that, each track segment (truncated rectangular prism) is constructed by using the two endpoints of the track part, as well as the two neighboring points. With those four points, the vertex shader determines the orientation of each prism face by calculating two vectors (plane_right, plane_up) and expanding the track to a certain width/height accordingly. The vertices will then be positioned at the edges of the prism. One track segment will be drawn as a triangle strip of 8 triangles (2 per prism face x 4 faces) i.e. 10 vertices.

<img width="1599" alt="image" src="https://github.com/weglide/maplibre-3d-linestring-demo/blob/main/screenshot.png">
