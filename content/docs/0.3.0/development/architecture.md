---
title: "Application Architecture"
weight: 1
---

### [&#128279;](#application-architecture) Application Architecture

0.3.0 is built around a monolithic Go server. It serves the HTML, caches requests with Redis, stores data in a Postgres database, acts as a WebSocket server, as well as proxies requests to Docker-managed services Keycloak, Gotenberg, and Coturn. As part of cloud deployment, only HTTP ports 80, 443, and Coturn related ports will be public-facing. 

|Name|Docker|Purpose|Ports|
|-|-|-|-|
|Go server||Custom Go standard lib HTTP server.|80, 443|
|db|x|Postgres in its managed alpine container.|5432|
|redis|x|Redis in its managed container.|6379|
|auth|x|Keycloak in its managed container.|8080, 8443|
|turn|x|Coturn in its managed container, using host network to handle port assignments.|3478, 44400-44500 UDP|
|docs|x|Gotenberg container for file conversion to PDF.|8000|
