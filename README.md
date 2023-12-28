# OpenSCAD hexagon STL creator

Code to create a hexagon grid
- 5 minute build with ChatGPT
- added some comments for better readability

Can be tested on:
- https://openscad.cloud/openscad/
- [Direct link](https://openscad.cloud/openscad/?&sharedFileLink=W3sibmFtZSI6Im1haW4uc2NhZCIsInR4dCI6Ii8vIHNpemUgPSByYWRpdXMgb2YgdGhlIGhleGFnb25cclxubW9kdWxlIGhleGFnb24oc2l6ZSwgaGVpZ2h0KSB7XHJcbiAgICBkaWZmZXJlbmNlKCkge1xyXG4gICAgICAgIC8vIDYgY29ybmVycyA9IGhleGFnb25cclxuICAgICAgICBjeWxpbmRlcihoID0gaGVpZ2h0LCByID0gc2l6ZSwgJGZuID0gNik7IC8vIG91dGVyIGhleGFnb25cclxuICAgICAgICB0cmFuc2xhdGUoWzAsIDAsIC0xXSkgY3lsaW5kZXIoaCA9IGhlaWdodCArIDIsIHIgPSBzaXplIC0gMiwgJGZuID0gNik7IC8vIGlubmVyIGhleGFnb25cclxuICAgIH1cclxufVxyXG5cclxubW9kdWxlIGhleGFnb25fZ3JpZChyb3dzLCBjb2x1bW5zLCBzaXplLCBoZWlnaHQpIHtcclxuICAgIGZvciAoaSA9IFswOnJvd3MgLSAxXSkge1xyXG4gICAgICAgIGZvciAoaiA9IFswOmNvbHVtbnMgLSAxXSkge1xyXG4gICAgICAgICAgICB0cmFuc2xhdGUoW1xyXG4gICAgICAgICAgICAgICAgMy8yICogc2l6ZSAqIGosIFxyXG4gICAgICAgICAgICAgICAgc3FydCgzKSAqIHNpemUgKiBpICsgKGogJSAyKSAqIHNxcnQoMykvMiAqIHNpemUsIFxyXG4gICAgICAgICAgICAgICAgMFxyXG4gICAgICAgICAgICBdKVxyXG4gICAgICAgICAgICBoZXhhZ29uKHNpemUsIGhlaWdodCk7XHJcbiAgICAgICAgfVxyXG4gICAgfVxyXG59XHJcblxyXG4vLyBjcmVhdGUgYSAzeDMgZ3JpZCB3aXRoIGhleGFnb25zIDIwIG1tIHJhZGl1cyBhbmQgMTAgbW0gaGVpZ2h0XHJcbmhleGFnb25fZ3JpZCgzLCAzLCAyMCwgODApOyJ9XQ==)

TODOs:
- add parameter for wall thickness (currently 2 mm)
- add argument to add base plate
- further ideas? --> Feel free to create a issue :) 


## OpenSCAD code
```
// size = radius of the hexagon
module hexagon(size, height) {
    difference() {
        // 6 corners = hexagon
        cylinder(h = height, r = size, $fn = 6); // outer hexagon
        translate([0, 0, -1]) cylinder(h = height + 2, r = size - 2, $fn = 6); // inner hexagon
    }
}

module hexagon_grid(rows, columns, size, height) {
    for (i = [0:rows - 1]) {
        for (j = [0:columns - 1]) {
            translate([
                3/2 * size * j, 
                sqrt(3) * size * i + (j % 2) * sqrt(3)/2 * size, 
                0
            ])
            hexagon(size, height);
        }
    }
}

// create a 3x3 grid with hexagons 20 mm radius and 80 mm height
hexagon_grid(3, 3, 20, 80);
```
