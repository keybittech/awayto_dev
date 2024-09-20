---
title: "0.3.0"
weight: 1
---

# 0.3.0 [repo]({{< param "v3Repo" >}})

Version 0.3.0 updates the stack to use a Go backend in a monolithic structure. This is in contrast to version 0.2.0's multi-server default installation utilizing Docker. 0.3.0 lessens the scope of Docker and microservices, in favor of a more unified server based on Go and Protobufs. As well, the frontend uses a revised implementation of RTK-Query in order to streamline the development and usage of API endpoints: defined Protobufs are used to generate an OpenAPI spec document, which in turn is used to auto-generate RTK-Query hooks for React. 

Some of the information here may be the same or similar to 0.2.0, but with revisions and updates where necessary.
