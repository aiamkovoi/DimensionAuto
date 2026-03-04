Auto Dims SC v5
A pyRevit script for automatic dimensioning of structural elements (walls, pylons, and structural columns) relative to grids in Revit.
What It Does
Select grids and structural elements with a box selection — the script automatically creates dimensions based on the spatial relationship between each element and its nearest grid:
ScenarioResultGrid passes through elementEdge→Grid→Edge snap chain (row 1) + Edge→Edge overall (row 2)Grid coincides with element edgeGrid→Edge dimension (row 1)Grid is outside elementGrid→Edge→Edge single chain (row 1)
Additionally, the script creates grid-to-grid dimension chains (pairwise + overall) positioned near the grid bubbles.
Features

Box selection workflow — select grids and elements in one go, press Enter
Automatic side detection — dimensions are placed on the side closest to the nearest parallel grid; X and Y dimensions follow the same diagonal to avoid overlap
Collision prevention — occupied zones are tracked so dimension lines don't stack on top of each other
Element collision avoidance — dimension lines route around other walls/columns in the path
Small text displacement — tight dimension values are nudged outward for readability
Failure handling — Revit "not parallel" and similar errors are auto-resolved without dialogs
Family instance support — correct reference conversion from symbol to instance geometry for columns

Usage

Open a plan view in Revit
Click the Auto Dims SC v5 button in pyRevit
Box-select grids and elements (walls, structural columns)
Press Enter

Settings
Configurable constants at the top of the script:
ParameterDefaultDescriptionOFFSET_1_MM800Row 1 offset from element (mm)OFFSET_2_MM1400Row 2 offset from element (mm)OFFSET_CHAIN_1_MM1500Grid chain offset from bubble (mm)OFFSET_CHAIN_GAP_MM700Gap between pairwise and overall grid chains (mm)ZERO_TOL_MM5Tolerance for "grid on edge" detection (mm)INTERSECT_TOL_MM50Tolerance for "grid intersects element" detection (mm)MAX_SNAP_DIST_MM10000Max distance to snap to a grid (mm)DEBUGTruePrint detailed log to pyRevit output
Requirements

Revit 2020+
pyRevit 4.8+

Installation
Copy auto_dims_v5.py into your pyRevit extension under a pushbutton bundle, e.g.:
YourExtension.extension/
  YourTab.tab/
    YourPanel.panel/
      AutoDims.pushbutton/
        script.py          ← rename the file to script.py
        icon.png           ← optional icon
Reload pyRevit and the button will appear.
License
MIT
