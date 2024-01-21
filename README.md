# RISCO

This is the hub repository for **RISCO Web Maps (V2)** libraries and server software.

**RISCO Web Maps** is a generic browser-based GIS data visualization and editing solution oriented for responsiveness, ease of user interaction and mobile 

## Features

**RISCO Web Maps** is a generic browser-based GIS data visualization and editing solution oriented for responsiveness, ease of user interaction and mobile support.

## Components

RISCO Web Maps software solution is comprised of these three components:

- **RISCO js V2** -- ES6 plain JavaScript client library, offering 2D mapping on modern browsers
- **RISCO Server V2** -- Golang implementation of server side RISCO JSON-based features protocol
- **RISCO Server PG V2** -- PostgreSQL *plpgsql* implementation of server-side features protocol geodatabase funcionality

Each of these components is hosted on it's own GitHub repository, as described in the following table.

| Component | GitHub repo | Language |
| --- | --- | --- |
| RISCO js V2 | [rpcavaco/riscojs_v2](https://github.com/rpcavaco/riscojs_v2) | ES6 ECMAScript / JavaScript (plain, no third party dependencies) |
| RISCO Server V2 | [rpcavaco/riscosrv_v2](https://github.com/rpcavaco/riscosrv_v2) | Golang using FastHTTP library |
| RISCO Server PG V2 | [rpcavaco/riscosrv_v2_pg](https://github.com/rpcavaco/riscosrv_v2_pg) | PL/pgSQL |


## Dependencies

**RISCO Web Maps** has a single platform dependency on **PostgreSQL / PostGIS**. 

Other software dependencies exist solely on RISCO Server Golang, namely:

- jackc/pgx (PostgreSQL driver)
- valyala/fasthttp (FastHTTP implementation)

