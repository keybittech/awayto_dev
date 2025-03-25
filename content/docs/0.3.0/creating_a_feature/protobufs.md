---
title: "Protobufs"
weight: 2
---

### [&#128279;](#core-types) Protobufs

Protobufs are central to the platform's API. By creating Protobufs, we can auto generate Go structs for the back end, and an OpenAPI-based set of hooks for React using RTK-Query. New Protobuf definitions can be added to the `proto` folder in the main directory. Upon building, auto-generated elements will be placed into the `/ts/hooks` folder (in the case of the RTK-Query API), and `/go/pkg/types` (in the case of Go structs).

Review existing Protobufs in the `proto` folder. Some Google extensions and `protovalidate` are available to use when declaring messages. Messages are validated automatically on request to the API. As well, adding REQUIRED field_behavior to a field will cause it to be mandatory in its generated Typescript types.

For our example, we'll create a proto that looks something like this:

```protobuf
message ITodo {
  string id = 1 [(buf.validate.field).string.uuid = true];
  string task = 2 [
    (buf.validate.field).string.min_len = 1,
    (google.api.field_behavior) = REQUIRED
  ];
  bool done = 3 [(google.api.field_behavior) = REQUIRED];
  string createdOn = 4;
}
```

Note: Any time you add a new file or update to the core package, it's generally a good idea to fully restart any running dev servers when developing the API or UI.
