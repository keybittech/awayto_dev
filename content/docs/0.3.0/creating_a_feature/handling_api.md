---
title: "Handling an API"
weight: 4
---

### [&#128279;](#handling-an-api) Handling an API

At this point, we've set up some data structures around our feature, including some endpoints and params we can interact with. To handle the endpoint from the API context, we'll make a new file `/go/pkg/handlers/todo.go`. If we don't add a handler, a warning will be given during startup of the Go server.

An example of a handler we could create, based on the Protobuf `service` definition:

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
