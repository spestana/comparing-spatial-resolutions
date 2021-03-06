# comparing-spatial-resolutions
Placeholder repo for hacking at "How should we compare or scale between rasters of different resolutions/grids?"

*Also, maybe this is the first of a continuing series of mini-hackathons where we set aside a block of time help each other out.*

## How should we compare or scale between rasters of different resolutions/grids?

Our primary motivation is to compare satellite imagery from multiple sources with different spatial resolutions, but maybe the solution will draw from generic image processing tools. How do we compute pixel-by-pixel "zonal statistics" (without creating 1000s of shapefiles)? What tools are there to aggregate, disaggregate, resample, apply weights across rasters?

Some tools of interest that might help us out:
* [xarray-spatial](https://github.com/makepath/xarray-spatial) seems promising but it's new (there are other xarray spin-offs we could look into)
* [xarray](https://xarray.pydata.org/en/stable/) and [rioxarray](https://corteva.github.io/rioxarray/stable/)
* [rasterio](https://rasterio.readthedocs.io/en/latest/)
* [geopandas](https://geopandas.org/)
* [gdal](https://gdal.org/)

Some shapefile-defined zonal stats notebooks I have:
* For ASTER imagery: 
  - [aster_utils.py](https://github.com/spestana/goes-cues/blob/master/aster_utils.py), Functions for working with ASTER TIR imagery(from the [AST_L1T product](https://lpdaac.usgs.gov/products/ast_l1tv003/)): converting DN to radiance, radiance to brightness temperature, and computing zonal statistics given a shapefile.
  - [zonal-statistics-aster.ipynb](https://nbviewer.jupyter.org/github/spestana/goes-cues/blob/master/zonal-statistics-aster.ipynb), Example notebook to read in an AST_L1T geotiff, shapefile, and compute zonal statistics.
  - [goes-aster-2017-2020.ipynb](https://nbviewer.jupyter.org/github/spestana/goes-cues/blob/master/goes-aster-2017-2020.ipynb), see this applied here with GOES-16 ABI and ASTER imagery
* For ECOSTRESS imagery: 
  - [eco-clearlake.ipynb](https://nbviewer.jupyter.org/github/spestana/whw2020_firewater/blob/master/ECOSTRESS/eco-clearlake.ipynb), Clip ECOSTRESS TIR imagery with a shapefile to look at lake surface temperature.

## Agenda for a mini-hackathon:

1. Introduce the problems we're trying to solve. What do these problems share in common, what can we work on together?
2. Do we have a starting point? What's been done previously?
3. What tools look like they can help us?
4. Try them out!
5. Note what worked and what didn't. Plan for next steps.


## My notes:

- use geojson instead of shapefiles
- make sure my goes-ortho geotiffs have the correct "PixelIsArea" or "PixelIsPoint" metadata flag (are my coordinates referencing the upper-left of the pixel or the center of the pixel?)
- try doing a bilinear interpolation with my ASTER imagery to get it on the NED DEM grid (30m or 90m?) so that all my datasets are on the same grid and resolution
  - [gdal_rasterize](https://gdal.org/programs/gdal_rasterize.html) (-tap, -ts, -tr, -te options)
  - [gdal_polygonize](https://gdal.org/programs/gdal_polygonize.html)
- other tools and resources of interest:
  - [ESMPy](https://earthsystemcog.org/projects/esmpy/) : ESMF Python Regridding Interface
  - [GEOS](https://trac.osgeo.org/geos) - Geometry Engine, Open Source - this is what gdal and a lot of other libraries (e.g. shapely) use in the background. Read documentation/source here for details on whats going on behind the scenes
  - [Raster data model (gdal)](https://gdal.org/user/raster_data_model.html)
  - [raster corner vs center coords figure](https://www.esri.com/about/newsroom/arcuser/understanding-raster-georeferencing/)
- xarray-spatial's [zonal statistics function](https://makepath.github.io/xarray-spatial/zonal_statistics.html) worked well!
  - **see my example notebook here:** [try-xarray-spatial.ipynb](https://github.com/spestana/comparing-spatial-resolutions/blob/master/try-xarray-spatial.ipynb), or on [nbviewer](https://nbviewer.jupyter.org/github/spestana/comparing-spatial-resolutions/blob/master/try-xarray-spatial.ipynb)
