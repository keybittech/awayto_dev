---
title: "Deployment"
weight: 8
---

## [&#128279;](#deployment) Deployment

In version 0.3.0, we continue to rely on Hetzner for self-hosting. However, only a single monolithic server is deployed, as opposed to the distributed server setup in 0.2.0. This greatly simplifies the processes and resources necessary for deployment. The [Makefile]({{< param "v3Repo" >}}/Makefile) offers two simple commands for deployment management. Deployed metadata is stored in the `deployed` folder, once deployment is complete.

- `make host_up` - Deploys Hetzner instance based on `.env` properties.
- `make host_down` - Deletes Hetzner instance based on `.env` properties. 
