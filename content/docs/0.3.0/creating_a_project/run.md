---
title: "Run the Project"
weight: 2
---

### [&#128279;](#run-the-project) Run the Project

#### Run Docker containers

Docker is used for Redis, Postgres, Coturn, and Goetnberg.

```
make docker_up
```

#### Build the project

```
make build
```

#### Develop the landing site

```
make landing_dev
```

#### Develop the app front end

```
make ts_dev
```

#### Develop the app back end

```
make go_dev
```

If the ts_dev server is also running, the go_dev server will proxy that for local development, instead of the front end static build folder.

#### Visit the site

Access the project at [https://localhost:7443](https://localhost:7443).

