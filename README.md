# Tiles Layout Planner

A single-file tile estimating tool for contractors. Enter room sizes and a tile
size; get the number of boxes to order, a to-scale layout drawing with every cut
piece dimensioned, and a printable report.

Live: https://tiles.illall.tech

## Why it exists

The usual estimate is `area ÷ tile area, round up`. That undercounts, because a
cut piece still consumes a **whole** source tile — it never plans where the cuts
land. This tool simulates the actual grid instead, so the box count reflects what
gets laid on site.

## What it does

- **Floor and Wall modes**, kept completely separate (different SKUs, so box
  counts must never pool together).
- **Box quantity** from a real grid simulation, not area division. Cut wastage is
  computed from the layout; only the handling/breakage buffer is a manual input.
- **Layout comparison** across 5 alignments × both tile orientations. Ranked by
  *smallest edge piece*, not box count — alignment never changes how many tiles
  you need, only how thin the edge slivers are. Orientation does change the count.
- **Openings** (windows, doors, fixtures) deducted from wall tiling, measured from
  the bottom-left corner the way a mason measures.
- **Skirting** quantity, calculated from strips cut out of the field tile.
- **Multiple rooms** pooled into one order, showing what pooling saves versus
  ordering room by room.
- **Units**: ft, ft-in (`10'6"`), inch, metre, mm — for both input and display.
  Feet is the internal canonical unit, so switching never loses precision.
- **Tile photos**: upload several pattern variants; adjacent tiles never repeat
  the same face.
- **Printable report** with per-room dimensioned drawings.

## Running it

No build step, no dependencies. Open `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
```

## Deploying

Any static host. On Vercel, no configuration is needed — `index.html` at the repo
root is served directly.

## Notes

- Pieces-per-box in the tile presets are typical values and vary by brand. Check
  the printed box label before ordering; the field is editable under Advanced.
- Tile presets convert mm to feet precisely (600 mm = 1.969 ft, not 2.0 ft). That
  ~1.5% difference decides whether an extra edge cut appears.
