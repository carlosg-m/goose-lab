# goose

Recipes for geospatial data preprocessing in Python.

- [Notebook 1](https://github.com/carlosg-m/goose/blob/4696f621dfbc711fc68d4e30e579d8e79825a0d0/Create%202d%20grid%20with%20NumPy.ipynb): Efficiently generate the bounding coordinates (xmin, ymin, xmax, ymax) of a 2d regular grid in numpy. This array can be easily converted into shapely or pygeos geometries.

- [Notebook 2](https://github.com/carlosg-m/goose/blob/983433b1af425dbb5846e8a7614f220579ea1ecf/Intersect%20points%20with%20a%20regular%20grid%20without%20a%20spatial%20index.ipynb): Intersect points with rectangles from a regular grid without a spatial index (using only NumPy). Useful for processing rasters larger than memory through reading windows or creating database indexes.
