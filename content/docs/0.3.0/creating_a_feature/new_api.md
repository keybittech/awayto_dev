---
title: "Defining API Endpoints"
weight: 3
---

### [&#128279;](#defining-api-endpoints) Defining API Endpoints

Protobufs are used to define APIs, using the `service` and `rpc` constructs, along with custom- and Google-based protos for HTTP related features. For each `rpc` defined in a `service` proto, a corresponding handler file needs to be created in a `/go/pkg/handlers` file. See existing handlers for examples. 

Existing protos use a standard method of defining service RPCs and then the input/output messages for each individual RPC. Care must be taken when designing an API in such a way that it doesn't become too large and cumbersome. Input and output messages should be simple, containing a few properties each, with specific purposes in mind.


#### External Properties

Use of Google-based proto annotations can be researched online, as well as studied in existing protos, and include:

- `google/protobuf/struct.proto`
- `google/api/annotations.proto`
- `google/api/field_behavior.proto`

#### Custom Properties

Custom properties are further defined in the `util.proto`:

**cache**: By default, the server will cache all GET requests for 180 seconds.
- DEFAULT - Default behavior.
- SKIP - Never cache endpoint responses.
- STORE - Permanently cache response in Redis, and use that on subsequent GETs.

**cache_duration**: Seconds. Used to override default 180 second cache duration for GET requests.

**throttle**: Todo. Throttles endpoint for 10 requests per n seconds.

**siteRole**: Limit access to a particular site role. Check `util.proto` for current values.

Following our example, we might create a service for our Todos like this:

```proto
service TodoService {
  rpc PostTodo(PostTodoRequest) returns (PostTodoResponse) {
    option (google.api.http) = {
      post: "/v1/todos"
      body: "*"
    };
  }

  rpc GetTodos(GetTodosRequest) returns (GetTodosResponse) {
    option (google.api.http) = {
      get: "/v1/todos"
    };
  }

  rpc DeleteTodo(DeleteTodoRequest) returns (DeleteTodoResponse) {
    option (google.api.http) = {
      delete: "/v1/todos/{id}"
    };
  }
}
```

And its corresponding input/output objects:

```proto
message PostTodoRequest {
  ITodo todo = 1 [(google.api.field_behavior) = REQUIRED];
}

message PostTodoResponse {
  string id = 1 [(google.api.field_behavior) = REQUIRED];
  bool done = 2 [(google.api.field_behavior) = REQUIRED];
}

message GetTodosRequest {}

message GetTodosResponse {
  repeated ITodo todos = 1 [(google.api.field_behavior) = REQUIRED];
}

message DeleteTodoRequest {
  string id = 1 [(google.api.field_behavior) = REQUIRED];
}

message DeleteTodoResponse {
  string id = 1 [(google.api.field_behavior) = REQUIRED];
}
```
