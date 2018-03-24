---
title: "PostgreSQL_PostGIS_Notes_1"
date: 2018-03-24T18:10:12-04:00
draft: false
tags: [PostgreSQL/PostSQL]
categories: [tech]
---

## PostgreSQL / PostGIS Notes (1)

All contents are from Carto Academy Tutorial: [*Learning SQL through the CARTO Editor*](https://carto.com/academy/courses/sql-postgis/intro-to-sql-and-postgis/)

### 1. the_geom

In our case, we have a point type geometry with coordinates at the values listed. Note that longitude is first and latitude is second, similar to (x,y) from plotting in a Cartesian coordinate plane. Just like there are different coordinate systems besides Cartesian (e.g., polar, spherical, etc.), maps have different coordinate systems, or **projections**. `The_geom` is stored in a system called WGS84.



---

### 2. the_geom_webmercator

```sql
SELECT cartodb_id, ST_AsText(the_geom_webmercator) AS the_geom_webmercator
FROM earthquake_sql
```

`the_geom_webmercator` contains all the same points that were in `the_geom`, but projected to Web Mercator, a web-optimized version of the historical Mercator projection. 

As you can see, the values range from around -20 million meters to +20 million meters in both the N/S and E/W directions because the circumference of the earth is around 40 million meters. This projection takes the furthest North and South to be ± 85.0511°, which allows the earth to be projected as a large square, very convenient for using square tiles with on the web. It excludes the poles, so other projections will have to be used if your data requires them.



---

### 3. Projection

- **4326** for [WGS84](http://en.wikipedia.org/wiki/World_Geodetic_System), which defines `the_geom`;
- **3857** for [Web Mercator](http://en.wikipedia.org/wiki/Web_Mercator), which defines `the_geom_webmercator`.

we will use `CDB_LatLng(lat,long)` to get a coordinate in the 4326 projection (WGS84).

```sql
SELECT cdb_latlng(cast(lat as float), cast(lng as float)) as geo FROM dfan.mcd_mn
```



---

### Distance & Unit

- `geometry` type arguments: allows you to measure the distance in degrees (lat/long)
- `geography` type arguments: allows you to measure the distance in meters
- `use_spheroid` argument: use WGS84’s [oblate spheroid earth](http://en.wikipedia.org/wiki/World_Geodetic_System#Main_parameters) (pass `true`) or assume the earth is perfectly spherical (pass `false`)

```sql
SELECT
  *,
  ST_Distance(
    the_geom::geography,
    CDB_LatLng(37.7833,-122.4167)::geography
  ) / 1000 AS dist
FROM
  earthquake_sql
```



In spatial functions, if an option is available that includes the `boolean use_spheroid` option, it will achieve the same result as casting your results using the `::geography` method

```sql
SELECT ST_Distance(the_geom, CDB_LatLng(37.7833,-122.4167), true) FROM earthquake_sql
```



Example

```plsql
SELECT
  AVG(ST_Distance(the_geom::geography,CDB_LatLng(43,-122)::geography) - ST_Distance(the_geom,CDB_LatLng(43,-122),true)) as average,
  STDDEV(ST_Distance(the_geom::geography,CDB_LatLng(43,-122)::geography) - ST_Distance(the_geom,CDB_LatLng(43,-122),true)) as std_deviation
FROM earthquake_sql
```



---

### 4. PostGIS Functions

- ST_SaveAsText:  **wkt**
- ST_Distance

![PostgreSQL/PostGIS](https://i0.wp.com/geosymp.com/wp-content/uploads/2017/07/Postgis_1-300x235.png?fit=300%2C235&ssl=1)