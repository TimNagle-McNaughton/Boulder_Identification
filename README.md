# Requirements
- ESRI ArcGIS & ArcPy
- Python 3+ (64-bit strongly recommended)
- Jupyter Notebook (can be converted to a .py)

### This method is based on the proximity of an illuminated face to a shadow.

**The full process is as follows:**
- The user supplies necessary input variables
- A 20-pixel radius mean filter is applied to the input HiRISE image to ‘smooth’ the image
- The averaged HiRISE image is split into three brightness interval images (‘dark’, ‘medium’, and ‘light’) based on user-determined pixel values
- A 2x2 range kernel filter is applied to each of the three brightness interval images 
- ‘Boulder’ pixels are iteratively extracted from each of the range-filtered images based on a user-determined range and step (i.e. all pixels above value n, for n in range x to y with step z)
- For each brightness interval, the user then visually compares the original HiRISE image to each of the boulder-pixel rasters to determine the pixel threshold at which no false-positive boulder pixels are present (the ‘conservative’ threshold), and the threshold at which no false-negative pixels are present (the ‘liberal’ threshold)
- The boulder rasters corresponding to the conservative and liberal values are converted to simplified polygons (polygons containing a minimum number of segments while remaining as close as possible the original raster cells)
- The minimum-bounding geometry of each polygon is calculated
- The resulting database tables are exported for further analysis
