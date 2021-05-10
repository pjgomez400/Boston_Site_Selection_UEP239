# Boston_Site_Selection_UEP239
Final project for UEP 239, Geospatial Programming in Python

Hours spent: 15

**User needs to check the ACS metadata to understand column names and decide what they want to change them to in the script**

This script evaluates four demographic and three spatial criteria to determine best ZCTAs for families with newborns. It does not use an ordinal scale through a ranking indicator, but rather selects ZCTA's that are in ALL of the top 50% of the demographic criteria. 

-Demographic criteria:
1) Number of married households
2) Number of kids in public schools
3) Percent of households making between 100K-150K
4) Number of households where the head of household has at least a BA degree.

-Spatial criteria
1) Within the Boston area as per the Metropolitan Regional Organization boundary
2) ZCTAs without four year colleges. Young children should not be growing up near degeneracy!
3) Air quality. EPA <https://www.epa.gov/outdoor-air-quality-data/download-daily-data> fine particulate matter smaller than 2.5 micrometers, which are dangerously small inhalable particles


ZCTA's with four year colleges were omitted, then ZCTAs within the Boston region were then selected. Finally, air quality was interpolated from monitoring stations to determine which ZCTA's were in the lowest 25%.


Thank you to the following Python experts:

Ismail Hachimi for the inspiration to use functools' reduce function for merging my dataframes:
https://stackoverflow.com/questions/44327999/python-pandas-merge-multiple-dataframes

DeepSpace for suggesting the apply method for changing column types:
https://stackoverflow.com/questions/33961028/remove-non-numeric-rows-in-one-column-with-pandas

CS95 for informing me that strings cannot be passed in boolean experssions, requiring the .query method instead:
https://stackoverflow.com/questions/46164141/keyerror-in-pandas-when-passing-concatenated-string-as-key

martinfleis for suggesting using spatial indicies to add a boolean column to my dataframe denoting whether there was an intersection with my other layer of interest (colleges):
https://gis.stackexchange.com/questions/375407/geopandas-intersects-doesnt-find-any-intersection

Saul Montoya for the tutorial on triangular interpolation in matplotlib:
https://www.hatarilabs.com/ih-en/geospatial-triangular-interpolation-with-python-scipy-geopandas-and-rasterio-tutorial


**Future improvement**
The raster created from the interpolation was not compatible with rasterstats zonal statistics. Instead, point_query (ESRI's Extract Values by Points) was used, creating a less accurate reading of ZCTA-wide air quality. This output also created a geojson output, which required extra wrangling to merge back to the ZCTA layer.