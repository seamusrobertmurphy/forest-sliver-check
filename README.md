Forest Sliver Check
================
SCS-SMurphy
2024-03-19

- [Directive](#directive)

## Directive

***Prototype Tool for Checking Minimum Size of Forest Polygons in
Submitted Baseline & Project Area Shapefiles***

``` r
tmap_mode("view")
tmap_options(check.and.fix = T)
polygon = read_sf("~/git_repos/forest-sliver-check/data/LULC_RR_2009_Dissolved.shp")
multipolygon = st_cast(polygon, "MULTIPOLYGON")
  tm_shape(st_geometry(multipolygon)) + 
  tm_borders(col = "red") + 
  tm_grid() +
    tm_basemap('Esri.WorldImagery') + 
    tm_layout(main.title = "Fig 1: Polygonized LULC Raster Submitted by Client", 
            title.size = 1.5, main.title.position = "center")
```

preserveecccbcc47a58d89e

``` r
multipolygon$area = st_area(multipolygon)
slivers = multipolygon %>%
  dplyr::filter(as.numeric(area) < 50000)
multipolygon$area
```

``` r
st_write(slivers, "slivers.shp")
```

``` r
tmap_mode("view")
tm_shape(st_geometry(slivers)) + tm_polygons()
```
