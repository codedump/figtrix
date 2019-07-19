# figtrix

A collection of tools to streamline command-line oriented production of graphics for scientific publications.

## figtile

`figtile` - Zoom, tile and overlay several EPS graphics onto a single canvas

### SYNOPSIS
**`figtile`** `[-h] [-t TILE_WIDTH | -n TILE_NUM | -l]`
`             [-s {none,0,first,1,up,down} | -S {none,0,first,1,up,down}]`
`             [-f] [-u {pt,mm,cm,inch}] [-r] [-o [OUTPUT]] [-d] [-q]`
`             `input [input ...] [-bar] [-c]`

### DESCRIPTION
**`figtile`** reads each of specified EPS input files, scales them according to the specified option (i.e. to match the largest, the smallest, or the first one of the list in either width or height), then paints them all in the specified order onto the same canvas. The ordering on the canvas can either be tiling or overlaying. Tiling is putting all images next to one another in a row, until either a maximum row width (-t option) or a maximum number of images (-n option) is reached. Then a new row is started. Overlaying is painting all images on top of one another, possibly aligning them in horizontal and/or vertical direction.

### OPTIONS
#### Positional arguments
-  `input`: EPS files to process.

#### Optional arguments:
- `-h, --help`: show this help message and exit
- `-t TILE_WIDTH, --tile-width TILE_WIDTH`: Tile graphics in of specified maximum width.
- `-n TILE_NUM, --tile-num TILE_NUM`: Tile up to the specified number of images per row.
- `-m COLUMNS, --matrix COLUMNS`: Tiles images in a matrix with COLUMNS columns (rows are auto-calculated). Images are centered horizontally and vertically at their respective positions.
- `-l, --overlay`: Stamp together (overlay) all input files in the specified order.
- `-s {none,0,first,1,up,down}, --scale-to-width {none,0,first,1,up,down}`: Scale all images uniformly to match the width of first, largest, smallest image.
- `-S {none,0,first,1,up,down}, --scale-to-height {none,0,first,1,up,down}`: Scale all images uniformly to match the height of first, largest, smallest image.
- `-f, --frames`: Draw frames around the graphics tiles.
- `-u {pt,mm,cm,inch}, --units {pt,mm,cm,inch}`: Units for user-specified measures, e.d. maximum tile width (default: cm).
- `-r, --ignore-ratio`: Do not keep the image ratio when scaling
- `-o OUTPUT, --output OUTPUT`: Output file name (EPS or PDF automatically detected from suffix).
- `-d, --debug`: Set verbosity level to debug.
- `-q, --quiet`: Surpresses informational output on stdout (i.e. all output except for the output EPS file).

### EXAMPLES
Tile four panels (fig-a.eps ... fig-d.eps) together into a 2x2 matrix and save result in figure.eps. Please note that the tile is build in EPS coordinate system, i.e. from bottom-left to top-right. Therefore, the panels to appear in the upmost row must be specified last:

    figtile -n 2 fig-c.eps fig-d.eps fig-a.eps fig-b.eps -o figure.eps

Tile all panel*.eps together, as many in a row as as fit into 15cm width:

    figtile -t 15 -u cm panel*.eps -o figure.eps

Overlay layer2.eps on top of layer1.eps, while scaling everything to match the width of layer1.eps:

    figtile -l --scale-to-width=first layer1.eps layer2.eps -o figure.eps

### DEPENDS
Needs a working Python-PyX installation, and everything that comes with it (i.e. obviously a working python environment :-)

### BUGS
PDF export does not work properly, probably related to bug in PyX version 0.11.1.

### AUTHOR
Florin Boariu <florin.figtrix(at)rootshell.ro>
