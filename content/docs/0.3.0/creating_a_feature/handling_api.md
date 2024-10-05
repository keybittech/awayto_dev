---
title: "Handling an API"
weight: 4
---

### [&#128279;](#handling-an-api) Handling an API

Each RPC we define in a Protobuf will be auto-discovered on build of the Go server. A corresponding handler must be created in `go/pkg/handlers`to handle the RPC. When writing handler functions, the API provides functionality from a number of built-in clients. Clients can be extended by adding to `go/pkg/clients` and should come with a corresponding interface in `go/pkg/clients/interfaces.go`. This version supports an LLM service, the database, Redis, Keycloak, and our WebSocket server. Clients are attached to the `Handlers` class and can be used like `h.Database`, `h.Redis`, etc., as seen below.

At this point, we've set up some data structures around our feature, including some endpoints and params we can interact with. To handle the endpoint from the API context, we'll make a new file `/go/pkg/handlers/todo.go`. If we don't add a handler, a warning will be given during startup of the Go server.

An example of a handler we could create, based on the Protobuf `service` definition we defined earlier:

```go
func (h *Handlers) PostTodo(w http.ResponseWriter, req *http.Request, data *types.PostTodoRequest) (*types.PostTodoResponse, error) {
	session := h.Redis.ReqSession(req)

	var id string
	err := h.Database.Client().QueryRow(`
		INSERT INTO dbtable_schema.todos (task, done, created_on, created_sub)
		VALUES ($1, FALSE, $2, $3::uuid)
		RETURNING id
	`, data.GetTodo().GetTask(), time.Now().Local().UTC(), session.UserSub).Scan(&id)

	if err != nil {
		return nil, util.ErrCheck(err)
	}

	return &types.PostTodoResponse{Id: id, Done; false}, nil
}
```
