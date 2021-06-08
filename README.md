# goose
<b>Recipes for geospatial data processing in Python.</b>


#### [Notebook 1 - create bounding box coordinates of a regular grid in Numpy](https://github.com/carlosg-m/goose/blob/7288655edbaa9c84f4c2885e4c7386195508af1d/Create%202d%20grid%20with%20NumPy.ipynb)
Efficiently generate the bounding coordinates (xmin, ymin, xmax, ymax) of a 2d regular grid in numpy. This array can be easily converted into shapely or pygeos geometries.


#### [Notebook 2 - intersect points with a regular grid without a spatial index](https://github.com/carlosg-m/goose/blob/7288655edbaa9c84f4c2885e4c7386195508af1d/Intersect%20points%20with%20a%20regular%20grid%20without%20a%20spatial%20index.ipynb)
Intersect points with rectangles from a regular grid without a spatial index (using only NumPy). Useful for processing rasters larger than memory through reading windows or creating database indexes.


#### [Notebook 3 - retrieve elevation for any point in Europe](https://github.com/carlosg-m/goose/blob/f53df7b28bd9dbd8a3d0b3a4cdf746dcbefece11/Copernicus%20-%20retrieve%20elevation%20for%20any%20point%20in%20Europe%20(Pandas%20version).ipynb) 
- The dataset is the [European Digital Elevation Model (EU-DEM), version 1.1](https://land.copernicus.eu/imagery-in-situ/eu-dem/eu-dem-v1.1) from European Union's Copernicus Programme. 

- The format is [Raster](https://desktop.arcgis.com/en/arcmap/10.3/manage-data/raster-and-images/what-is-raster-data.htm) data (geotiff), divided into 1000x1000km tiles, 25m resolution, accuracy of [~7m RMSE](https://ec.europa.eu/eurostat/documents/7116161/7172326/Report-EU-DEM-statistical-validation-August2014.pdf). 
- The only dependencies of this script are Numpy, Pandas, Pyproj and Rasterio. 
- The process was designed to minimize memory consumption. Tiles or chunks of the rasters are read sequentially from storage.
- Input coordinates are assumed to be in WGS84 (latitude and longitude).
- A distributed version of this script can be easily created with Dask for Big Data use cases.

<b>Basic usage example:</b>

1) Download the raster tiles from [Copernicus website](https://land.copernicus.eu/imagery-in-situ/eu-dem/eu-dem-v1.1).

<img src="https://user-images.githubusercontent.com/55836583/121091747-68387980-c7e2-11eb-8858-de872a21bb7b.png" width=400>

2) Instantiate the object `CopernicusDEM` with the geotiff file paths and call the `get_elevation` method over a Pandas dataframe with latitude and longitude columns.
```
airports = pd.DataFrame([['LPPT', 38.775600, -9.135400],
                         ['LPPR', 41.242100, -8.678600],
                         ['LPFR', 37.017600, -7.969700],
                         ['LPBJ', 38.063700, -7.939200]], columns=['ICAO', 'Latitude', 'Longitude'])
                         
copernicus = CopernicusDEM(raster_paths=['eu_dem_v11_E20N10.TIF', 'eu_dem_v11_E20N20.TIF'])

airports = copernicus.get_elevation(airports, lat_col='Latitude', lon_col='Longitude')

print(airports)
```
![image](https://user-images.githubusercontent.com/55836583/121090044-e3e4f700-c7df-11eb-8fff-45ba81423b03.png)

