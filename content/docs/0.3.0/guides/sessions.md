---
title: "Sessions"
weight: 2
---

### [&#128279;](#sessions) Sessions

In a handler function, a reference to the session can be retrieved from Redis by passing the current request into the ReqSession function, as seen in [Handling an API](#handling-an-api). This returns a `UserSession` with the following available properties:

```go
type UserSession struct {
	UserSub                 string   `json:"userSub"`
	UserEmail               string   `json:"userEmail"`
	GroupName               string   `json:"groupName"`
	GroupId                 string   `json:"groupId"`
	GroupSub                string   `json:"groupSub"`
	GroupExternalId         string   `json:"groupExternalId"`
	GroupAi                 bool     `json:"ai"`
	SubGroups               []string `json:"subGroups"`
	SubGroupName            string   `json:"subGroupName"`
	SubGroupExternalId      string   `json:"subGroupExternalId"`
	Nonce                   string   `json:"nonce"`
	AvailableUserGroupRoles []string `json:"availableUserGroupRoles"`
}
```

Each handler also provides direct access to the standard Go library server `Request` and `ResponseWriter` objects. There are a few additional Request context parameters available:

- `LogId` - a unique request id.
- `SourceIp` - the remote address.
- `UserSession` - references the above struct.

