---
title: "Protobufs"
weight: 2
---

### [&#128279;](#core-types) Protobufs

Protobufs are central to the platform's API. By creating Protobufs, we can auto generate Go structs for the back end, and an OpenAPI-based set of hooks for React using RTK-Query. To add Protobufs to the project, add `proto` files to the `protos` folder in the main directory. New Protobuf definitions can be added to the `proto` folder in the main directory. Upon building, auto-generated elements will be placed into the `/ts/hooks` folder (in the case of the RTK-Query API), and `/go/pkg/types` (in the case of Go structs).

Review existing Protobufs in the `proto` folder.

For our example, we'll create a proto that looks something like this:

```protobuf
message ITodo {
  string id = 1;
  string task = 2;
  bool done = 3;
  string createdOn = 4;
}
```

Note: Any time you add a new file or update to the core package, it's generally a good idea to fully restart any running dev servers when developing the API or UI.
