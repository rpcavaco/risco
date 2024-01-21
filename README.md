# RISCO

This is the hub repository for **RISCO Web Maps (V2[^1])** libraries and server software.

**RISCO Web Maps** is a generic browser-based 2D GIS data visualisation and editing solution oriented for responsiveness and mobile support.

## Why RISCO

Central objective of creating RISCO: provide direct read and write web access to PostGIS tables.

Publishing web maps on wide available JS API's like [Leaflet](https://leafletjs.com/) or [OpenLayers](https://openlayers.org/) is a client-side only out-of-the-box solution to straightaway display GIS data.

After having your web map published like that, you might stumble into some difficulties:
- usually you will rely on some third party WFS or WMS layers provider infrastructure for which you have limited or no admin access and you cannot easily adapt or customise it to your needs;
- widgeting: you will be wondering for out-of-the-box functionality beyond feature popups like, e.g., *table of contents*, base map swapping, measuring tools, etc.;
- you might need to edit data and you might want to do it fully real-time, either on desktop or on mobile, having edits reflected on published maps without delay - existing libraries do provide base functionality for this but you must know how to, and put some effort to, properly wire it to an available geo web services provider infrastructure.

RISCO tries to address these needs, providing basic out-of-the-box client-side functionality combined with rich server side functionality and a tight coupling between both, client and server sides of your solution.

## What RISCO is not 

Both Leaflet and OpenLayers are seasoned client libraries, offering coordinate system transforms[^2], a profusion of modern data source support from the likes of Mapbox or CartoDB, a huge range of extended visualisation functionality, and extensibility through a plugin architecture (Leaflet).

The functionality RISCO offers is not JavaScript centric, instead it heavily relies on the very rich server-side PostGIS functions.

An example: clustering or binning of point features. This functionality is still on the making but it will rely solely on calling PostGIS clustering functions.

So, as a web developer, you might feel uncomfortable for RISCO not being JavaScript centric, not relying on any kind of NodeJS support, not depending on modernities like Angular, React or Vue, or not depending on popular server side technologies like PHP or MySQL.

Also it is clear RISCO is really new and not (hopefully yet ;) ) supported by a solid contributors community.

## Features

RISCO was brought up around the idea of providing very easy read and write web access to PostGIS tables. So, RISCO was built natively as a client and server solution.

### Types of layers

- Raster (from WMS)
- Vectors from web data server sources
- Synthetic generated vectors like graticules or gridded objects

All vectors can exhibit "map tip" behaviour: the display of a lightweight popup and selection markers shown on mouse hover (on desktop) or on "mobile interaction modes".

### Supported web data sources

- RISCO own vector layers (serving any PostGIS geometry-enabled table)
- OGC WMS or WFS layers
- ArcGIS Server feature layers

Editing is only supported on RISCO's own layers. 
Raster is only supported through WMS (not yet through WMTS).

Starting soon: implementing reading support for **[OGC API -Features](https://ogcapi.ogc.org/features/)**

### Coordinate systems

RISCO does not transform coordinate systems (CS) in client. 

RISCO was devised for low scale work (higher detail). It is supposed to work only with plane coordinates.

WMS, WFS or ArcGIS services used must allow for the CS defined in map config. 

RISCO own layers, if not in map's CS, are automatically transformed through PostGIS.

### Webmap configuring and styling

Configuring ....


### Geometry editing

### Mobile interaction modes

### Relationships between vector features

bla bla ...

### Dashboarding


## Components

RISCO Web Maps software solution is comprised of these three components:

- **RISCO js V2** -- ES6 plain JavaScript client library, offering 2D mapping on modern browsers
- **RISCO Server V2** -- Golang implementation of server side RISCO JSON-based features protocol
- **RISCO Server PG V2** -- PostgreSQL and PostGIS *PL/pgSQL* implementation of geodatabase server-side features protocol and geometric analysis functionality  

Example applications:

- **RISCO page** -- Basic (non-editing) RISCO map web page (suggesting uses of extension mechanisms) 
- **RISCO webapp** -- Editing-oriented RISCO Python FastAPI webapp (supporting authentication)


Each of these components and example applications is hosted on it's own GitHub repository, as described in the following table.

| Component | GitHub repo | Language |
| --- | --- | --- |
| RISCO js V2 | [rpcavaco/riscojs_v2](https://github.com/rpcavaco/riscojs_v2) | ES6 ECMAScript / JavaScript (plain, no third party dependencies) |
| RISCO Server V2 | [rpcavaco/riscosrv_v2](https://github.com/rpcavaco/riscosrv_v2) | Golang using FastHTTP library |
| RISCO Server PG V2 | [rpcavaco/riscosrv_v2_pg](https://github.com/rpcavaco/riscosrv_v2_pg) | PL/pgSQL |
| RISCO page | TBD | HTML, CSS, JavaScript |
| RISCO webapp | TBD | Python 3, HTML, CSS, JavaScript |


## Dependencies

**RISCO Web Maps** has a single platform dependency on **PostgreSQL / PostGIS**. 

Other software dependencies exist solely on RISCO Server Golang, namely:

- jackc/pgx (PostgreSQL driver)
- valyala/fasthttp (FastHTTP implementation)

## Installation


-----

**Notes**

[^1]: V2 stands for "Version 2": current RISCO evolved from a much more limited preceding package.

[^2]: RISCO JS client provides no coordinate transforms functionality.