# goose
<b>Recipes for geospatial data preprocessing in Python.</b>

- [Notebook 1](https://github.com/carlosg-m/goose/blob/4696f621dfbc711fc68d4e30e579d8e79825a0d0/Create%202d%20grid%20with%20NumPy.ipynb): Efficiently generate the bounding coordinates (xmin, ymin, xmax, ymax) of a 2d regular grid in numpy. This array can be easily converted into shapely or pygeos geometries.

- [Notebook 2](https://github.com/carlosg-m/goose/blob/983433b1af425dbb5846e8a7614f220579ea1ecf/Intersect%20points%20with%20a%20regular%20grid%20without%20a%20spatial%20index.ipynb): Intersect points with rectangles from a regular grid without a spatial index (using only NumPy). Useful for processing rasters larger than memory through reading windows or creating database indexes.

- [Notebook 3](https://github.com/carlosg-m/goose/blob/e87259c28e47dc60227979b0a16becb23821f2f6/Copernicus%20-%20retrieve%20elevation%20for%20any%20point%20in%20Europe%20(Pandas%20version).ipynb): Retrieve elevation for any point in Europe. 
  - The dataset is the [European Digital Elevation Model (EU-DEM), version 1.1](https://land.copernicus.eu/imagery-in-situ/eu-dem/eu-dem-v1.1) from European Union's Copernicus Programme. 
  
  - The format is [Raster](https://desktop.arcgis.com/en/arcmap/10.3/manage-data/raster-and-images/what-is-raster-data.htm) data (geotiff), divided into 1000x1000km tiles, 25m resolution, accuracy of [~7m RMSE](https://ec.europa.eu/eurostat/documents/7116161/7172326/Report-EU-DEM-statistical-validation-August2014.pdf). 
  - The only dependencies of this script are Numpy, Pandas, Pyproj and Rasterio. 
  - The process was designed to minimize memory consumption. Tiles or chunks of the rasters are read sequentially from storage.
  - A distributed version of this script can be easily created with Dask for Big Data use cases.
  - Input coordinates are assumed to be in WGS84 (latitude and longitude).


