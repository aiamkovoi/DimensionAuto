# Auto Dims SC v5

A pyRevit script for automatic dimensioning of structural elements (walls, pylons, and structural columns) relative to grids in Revit.

## What It Does

Select grids and structural elements with a box selection — the script automatically creates dimensions based on the spatial relationship between each element and its nearest grid:

| Scenario | Result |
|---|---|
| Grid passes through element | Edge→Grid→Edge snap chain (row 1) + Edge→Edge overall (row 2) |
| Grid coincides with element edge | Grid→Edge dimension (row 1) |
| Grid is outside element | Grid→Edge→Edge single chain (row 1) |

Additionally, the script creates **grid-to-grid dimension chains** (pairwise + overall) positioned near the grid bubbles.

## Features

- **Box selection workflow** — select grids and elements in one go, press Enter
- **Automatic side detection** — dimensions are placed on the side closest to the nearest parallel grid; X and Y dimensions follow the same diagonal to avoid overlap
- **Collision prevention** — occupied zones are tracked so dimension lines don't stack on top of each other
- **Element collision avoidance** — dimension lines route around other walls/columns in the path
- **Small text displacement** — tight dimension values are nudged outward for readability
- **Failure handling** — Revit "not parallel" and similar errors are auto-resolved without dialogs
- **Family instance support** — correct reference conversion from symbol to instance geometry for columns

## Usage

1. Open a plan view in Revit
2. Click the **Auto Dims SC v5** button in pyRevit
3. Box-select grids and elements (walls, structural columns)
4. Press **Enter**

## Settings

Configurable constants at the top of the script:

| Parameter | Default | Description |
|---|---|---|
| `OFFSET_1_MM` | 800 | Row 1 offset from element (mm) |
| `OFFSET_2_MM` | 1400 | Row 2 offset from element (mm) |
| `OFFSET_CHAIN_1_MM` | 1500 | Grid chain offset from bubble (mm) |
| `OFFSET_CHAIN_GAP_MM` | 700 | Gap between pairwise and overall grid chains (mm) |
| `ZERO_TOL_MM` | 5 | Tolerance for "grid on edge" detection (mm) |
| `INTERSECT_TOL_MM` | 50 | Tolerance for "grid intersects element" detection (mm) |
| `MAX_SNAP_DIST_MM` | 10000 | Max distance to snap to a grid (mm) |
| `DEBUG` | True | Print detailed log to pyRevit output |

## Requirements

- Revit 2020+
- [pyRevit](https://github.com/pyrevitlabs/pyRevit) 4.8+

## Installation

Copy `auto_dims_v5.py` into your pyRevit extension under a pushbutton bundle, e.g.:

```
YourExtension.extension/
  YourTab.tab/
    YourPanel.panel/
      AutoDims.pushbutton/
        script.py          ← rename the file to script.py
        icon.png           ← optional icon
```

Reload pyRevit and the button will appear.

## License

[MIT](LICENSE)
