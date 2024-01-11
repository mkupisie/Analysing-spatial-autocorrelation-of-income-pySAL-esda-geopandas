## Calculating global and spatial autocorrelation of income
Calculating global and local spatial autocorrelation of income (average monthly gross wages and salaries) noted per each polish county in 2022 based on Moran's I and LISA statistics. Calculations were conducted using the following packages: pySAL, splot.esda, geopandas.

The data that were used in the calculation were obtained from the Local Data Bank: https://bdl.stat.gov.pl/bdl/start.

More details about data can be found here: https://stat.gov.pl/en/metainformation/glossary/terms-used-in-official-statistics/693,term.html.

Detailed steps of calculating spatial autocorrelation are described within the code.

*Note: For the purpose of spatial autocorrelation calculation, the geometry of counties shapefile must have been fixed as it contained overlapping polygons (overlapping polygons could influence the results as in the calculation 'neighbour' was defined as any polygon that is sharing at least one common vertex of the border).*

### Fixing overlapping polygons
For this purpose the following steps and vector function in QGIS were used:
- **Topology Checker:** to identify overlapping polygons
- **Polygon Self-Intersection:** to create new separate polygons from overlapping parts
- **Editing ids of new created polygons**, so that it is the same as one of the polygons to which it is adjacent
- **Dissolve:** to dissolve polygons based on their unique ids

the technique can be seen here: https://www.youtube.com/watch?v=DMmGTtLx73M
(this technique was chosen for the purpose of the spatial autocorrelation calculation, because the area of the overlapping polygons was less than 1% of the Poland area,
so regardless of which neighboring polygon the overlapping layers were attached to, it should not affect the results).

**Topology checker**
![QGIS_topography_checker_overlapping](https://github.com/mkupisie/Calculating-spatial-autocorrelation-of-income-pySAL-esda-geopandas/assets/130785524/bf433b4f-ee6e-4fa7-8256-87f2cd281f5e)

**Polygon Self-intersection**
![QGIS_intersected_parts](https://github.com/mkupisie/Calculating-spatial-autocorrelation-of-income-pySAL-esda-geopandas/assets/130785524/d708cdee-43ff-4ff3-9efd-b3ff3c61dd9b)

**Topology checker after dissolving polygons**
![topology_check_after](https://github.com/mkupisie/Calculating-spatial-autocorrelation-of-income-pySAL-esda-geopandas/assets/130785524/dd3cae7a-dc9f-4303-b602-04be04ae8a47)


  
