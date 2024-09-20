---
title: "Application Architecture"
weight: 1
---

### [&#128279;](#application-architecture) Application Architecture

For the purposes of core development, services are defined in a central [docker-compose]({{< param "v2Repo" >}}/blob/main/docker-compose.yml) file in the root of the project. Here's a brief overview of each and their ports. You can find a root-level folder for each in most cases, containing its own Dockerfile.

|Name|Purpose|Ports|
|-|-|-|
|app|An Nginx host for reverse proxying to other services, and serving Hugo and React files.|80, 443|
|api|Express.js in a node alpine container.|9443|
|db|Postgres in its managed alpine container.|5432|
|redis|Redis in its managed container.|6379|
|fs|A custom file storage implementation, utilizing SQLite and Socat in an alpine container.|8000|
|auth|Keycloak in its managed container.|8080, 8443|
|sock|A custom websocket server in a node alpine container.|8888|
|turn|Coturn in its managed container, using host network to handle port assignments.|3478, 44400-44500 UDP|
|mongo|MongoDB in its managed container.|27017, used by Graylog only.|
|elasticsearch|Elasticsearch in its managed container.|9200, used by Graylog only.|
|graylog|Graylog in its managed container.|9000, 1514 TCP/UDP, 12201 TCP/UDP|
|mail|TBD|TBD|

When starting the stack with `docker compose up -d`, all these ports should be available on the host system. You can review the compose file to see which services depend on others. Not all services are required to be run at the same time. For example, it's often the case we'll stop graylog when developing locally, `docker compose stop graylog mongo elasticsearch`.

With regard to service routing, most services are configured to directly communicate with each other utilizing Docker's networking capabilities. However, to simplify communication with external requests, we use Nginx as a reverse proxy. This way, consumers need only interact with a single host to gain access to platform features.

![Application Reverse Proxy](/doc_images/app_reverse_proxy.png)
