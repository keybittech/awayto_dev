---
title: "Software"
weight: 5
---

## [&#128279;](#software) Software

In no particular order, the following lists the third-party software used in Awayto, along with their key features and a primary source for  usage in the system:

| Technology | Description | Source |
|-|-|-|
| Make | Task running, building, deploying | [Makefile]({{< param "v3Repo" >}}/blob/main/Makefile) |
| Shell | Deployment install/configure scripts | [/deploy/scripts]({{< param "v3Repo" >}}/tree/main/deploy/scripts) |
| Docker | Container service, docker compose, supports cloud deployments | [/deploy/scripts/docker]({{< param "v3Repo" >}}/tree/main/deploy/scripts/docker) |
| Postgres | Primary database | [/deploy/scripts/db]({{< param "v3Repo" >}}/tree/main/deploy/scripts/db) |
| React | Front end TSX components and hooks built with a customized CRACO config | [/ts]({{< param "v3Repo" >}}/tree/main/ts) |
| ReduxJS Toolkit | React state management and API integrating with Protobufs | [/ts/src/hooks/store.ts]({{< param "v3Repo" >}}/blob/main/ts/src/hooks/store.ts) |
| PNPM | Front end package management | [/ts/package.json]({{< param "v3Repo" >}}/blob/main/ts/package.json) |
| Let's Encrypt | External certificate authority | |
| Hetzner | Cloud deployment variant | [/deploy/scripts/host]({{< param "v3Repo" >}}/tree/main/deploy/scripts/host) |
| Keycloak | Authentication and authorization, SSO, SAML, RBAC | [/java]({{< param "v3Repo" >}}/tree/main/java) |
| Redis | Sessions & caching | [/go/pkg/clients/redis.go]({{< param "v3Repo" >}}/blob/main/go/pkg/clients/redis.go) |
| Hugo | Static site generator for landing, documentation, marketing | [/landing]({{< param "v3Repo" >}}/tree/main/landing) |
| DayJS | Scheduling and time management utilities | [/ts/src/hooks/time_unit.ts]({{< param "v3Repo" >}}/blob/main/ts/src/hooks/time_unit.ts) |
| Material-UI | React UI framework based on Material Design | [/ts/src/modules]({{< param "v3Repo" >}}/tree/main/ts/src/modules) |
| Coturn | TURN & STUN server for WebRTC based voice and video calling | [/deploy/scripts/turn]({{< param "v3Repo" >}}/tree/main/deploy/scripts/turn) |
| WebSockets | Dedicated websocket server for messaging orchestration, interactive whiteboard | [/go/pkg/clients/sock.go]({{< param "v3Repo" >}}/tree/main/go/pkg/clients/sock.go) |
