# RISCO

This is the hub repository for **RISCO Web Maps (V2[^1])** client libraries and server software.

**RISCO Web Maps** is a generic browser-based 2D GIS data visualisation and editing solution oriented for responsiveness and mobile support.

After reading this introductory README, you'll need to know how to get started. If it's not your first time here, you'll also need aditional information. Please check this project Wiki [here](https://github.com/rpcavaco/risco.wiki.git).

**RISCO Workshop - Mentor Streams OGC-ASF Codesprint Evora 2024**
-------



Please, follow this [link](#risco-workshop) to find the workshop materials.

-------

## Why RISCO

Central objective of creating RISCO: provide direct read and write web access to PostGIS tables.

Publishing web maps on wide available JS API's like [Leaflet](https://leafletjs.com/) or [OpenLayers](https://openlayers.org/) is a client-side only out-of-the-box solution to straightaway display GIS data.

After having your web map published like that, you might stumble into some difficulties:
- usually you will rely on some third party WFS or WMS layers provider infrastructure for which you have limited or no admin access and you cannot easily adapt or customise it to your needs;
- widgeting: you will be wondering for out-of-the-box functionality beyond feature popups like, e.g., *table of contents*, base map swapping, measuring tools, etc.;
- you might need to edit data and you might want to do it fully real-time, either on desktop or on mobile, having edits reflected on published maps without delay - existing libraries do provide base functionality for this but you must know how to, and put some effort to, properly wire it to an available geo web services provider infrastructure.

RISCO tries to address these needs, providing basic out-of-the-box client-side functionality combined with rich server side functionality and a tight coupling between both, client and server sides of your solution.

RISCO was devised to work at larger scales, for municpalities or regions, providing a reliable editing environment. For this, RISCO is prepared to use plane coordinates used on larger scale cartography. For many reasons, usual  Web Mercator EPSG:3857 coordinate system should be avoided. 

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
- ArcGIS Server layers (MapServer - including Query layer - and ImageServer)

Editing is only supported on RISCO's own layers. 
Raster is only supported through WMS (not yet through WMTS).

Starting soon: implementing reading support for **[OGC API - Maps](https://ogcapi.ogc.org/maps/)**

### Coordinate systems

RISCO does not transform coordinate systems (CS) in client. 

RISCO was devised for higher scale work (higher detail). It is supposed to work only with plane coordinates.

WMS, WFS or ArcGIS services used must allow for the CS defined in map config. 

RISCO own layers, if not in map's CS, are automatically transformed through PostGIS.

### Webmap configuring and styling

Configuring is provided on JSON files.
Styling is achieved with parameters similar to CSS. 

Out of the box,it allows for info-style or maptip-style popups and interactive table of contents (TOC).


### Geometry editing

RISCO provides tools for geometry editing.

### Dashboarding and slicing

Work is underway to get simple dashboard functionality and siliging filtering using graphic widgets sucha as treemaps, etc.


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
| RISCO webapp | TBD | Python 3, HTML, CSS, JavaScript |


## Dependencies

**RISCO Web Maps** has a single platform dependency on **PostgreSQL / PostGIS**. 

Other software dependencies exist on RISCO Server, namely:

- jackc/pgx (PostgreSQL driver)
- valyala/fasthttp (FastHTTP implementation)

Demo web app is built on Python framework FastAPI

## Installation

Please access each of the components repositories to find installation instructions.

There is also a Docker container "compose" configuration prepared for [OGC-ASF Joint Code Sprint 2024 workshop](#risco-workshop) 


-----

## Risco Workshop

**RISCO Workshop - Mentor Streams OGC-ASF Codesprint Evora 2024**

Slides are located [here](https://docs.google.com/presentation/d/1jw2zNSeX8iBuVtAlq6LxXecfri2DPuM9QaScz8g4wxY/edit?usp=sharing).

> [!WARNING]  
> Workshop containers are not ready for Windows environment, due to the use of unsupported --net=host parameter

To run workshop container bundle, you need to:

1. have Docker in your system
2. choose a folder as workspace
3. in your chosen workspace, download both files found [here](OGC_ASF_Workshop_Evora_2024)
4. Extract 'cont_shared_folders.zip', creating a folder with same name
5. Making sure you have 'compose.yaml' in your workspace, open a terminal and type

		docker-compose --project-name risco_workshop up
 
	to see logs in interactive terminal, or run it detached using   

		docker-compose --project-name risco_workshop up -d

6. To stop it, if using interactive terminal, you must first type Ctrl-C in it.

	To completely stop and clean containers and volumes, type:

		docker-compose --project-name risco_workshop down -v

If using detached form, you can check logs inside cont_shared_folders folder.


-----

**Notes**

[^1]: V2 stands for "Version 2": current RISCO evolved from a much more limited preceding package.

[^2]: RISCO JS client provides no coordinate transforms functionality.