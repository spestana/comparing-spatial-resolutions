# comparing-spatial-resolutions
Placeholder repo for hacking at "How should we compare or scale between rasters of different resolutions/grids?"


## How should we compare or scale between rasters of different resolutions/grids?

Our primary motivation is to compare satellite imagery from multiple sources with different spatial resolutions, but maybe the solution will draw from generic image processing tools. How do we compute pixel-by-pixel "zonal statistics" (without creating 1000s of shapefiles)? What tools are there to aggregate, disaggregate, resample, apply weights across rasters?

Some tools of interest that might help us out:
* [xarray-spatial](https://github.com/makepath/xarray-spatial) seems promising but it's new (there are other xarray spin-offs we could look into)
* [xarray](https://xarray.pydata.org/en/stable/) and [rioxarray](https://corteva.github.io/rioxarray/stable/)
* [rasterio](https://rasterio.readthedocs.io/en/latest/)
* [geopandas](https://geopandas.org/)
* [gdal](https://gdal.org/)

## Agenda for a mini-hackathon:

1. Introduce the problems we're trying to solve. What do these problems share in common, what can we work on together?
2. Do we have a starting point? What's been done previously?
3. What tools look like they can help us?
4. Try them out!
5. Note what worked and what didn't. Plan for next steps.
