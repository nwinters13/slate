---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Game-A-Lot API! You can use our API to access Game-A-Lot Lobby API endpoints,
which can create, modify, and delete lobbies for handling the lifecycle of rooms in your games.

We have language bindings in Shell! You can view code examples in the dark area to the right.

# Authentication

Game-A-Lot currently has no Authentication. In the future we hope to support API Keys to prevent
other accessors from being able to modify your lobbies.

<aside class="notice">
Authentication will be added to Game-A-Lot lobby APIs shortly
</aside>

# Lobbies

## Create a Lobby

```shell
curl "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby"
  -X POST
```

> The above command returns JSON structured like this:

```json
{
   "data":{
      "lobbyID":"VL8v68",
      "users":{

      },
      "isOpen":true
   },
   "statusCode":200
}
```

This endpoint creates a lobby and returns the created lobby.

### HTTP Request

`POST https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby`

## Get a Lobby

```shell
curl "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/VL8v68"
  -X GET
```

> The above command returns JSON structured like this:

```json
{
   "data":{
      "lobbyID":"VL8v68",
      "users":[
         "TJ",
         "Graham",
         "Nate",
         "Broc"
      ],
      "isOpen":true
   },
   "statusCode":200
}
```

This endpoint retrieves a specific lobby.

### HTTP Request

`GET https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/<lobbyID>`

### URL Parameters

Parameter | Description
--------- | -----------
lobbyID | The ID of the lobby to retrieve

## Delete a Lobby

```shell
curl "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/4AmFs6"
  -X DELETE
```

> The above command has no response

This endpoint deletes a specific lobby.

### HTTP Request

`DELETE https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/<lobbyID>`

### URL Parameters

Parameter | Description
--------- | -----------
lobbyID | The ID of the lobby to delete


## Open or Close a Lobby

```shell
curl "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/IIB9xP/status\?open\=0"
  -X PUT
```

> The above command returns JSON structured like this:

```json
{
   "data":"False",
   "statusCode":200
}
```

This endpoint sets the status of the lobby. The status of the lobby determines the ability for users to join a specific lobby. An open lobby will accept new users who join the lobby. A lobby that is not open will reject users attempting to join the lobby.

### HTTP Request

`PUT "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/<lobbyID>/status?open\=<isOpen>"`

### URL Parameters

Parameter | Description
--------- | -----------
lobbyID | The ID of the lobby for which the status will be updated

### Query Parameters

Parameter | Description
--------- | -----------
isOpen | The new status for the lobby. If set to `y`, `yes`, `t`, `true`, `on`, or `1`, sets the lobby to open. If set to `n`, `no`, `f`, `false`, `off`, or `0`, sets the lobby to closed.


## Add a user to a Lobby

```shell
curl "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/IIB9xP/user/TJ"
  -X PUT
```

> The above command returns JSON structured like this:

```json
{
   "data":[
      "TJ",
      "Graham",
      "Nate",
      "Broc"
   ],
   "statusCode":200
}
```

This endpoint puts a user into a lobby provided that the lobby is open.

### HTTP Request

`PUT "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/<lobbyID>/user/<userID>"`

### URL Parameters

Parameter | Description
--------- | -----------
lobbyID | The ID of the lobby in which to add the user
userID  | The user to add to the lobby


## Remove a user from a Lobby

```shell
curl "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/IIB9xP/user/BadPlayer"
  -X DELETE
```

> The above command returns JSON structured like this:

```json
{
   "data":[
      "TJ",
      "Graham",
      "Nate",
      "Broc"
   ],
   "statusCode":200
}
```

This endpoint removes a user from the specified lobby.


### HTTP Request

`DELETE "https://gb7h15dz05.execute-api.us-east-1.amazonaws.com/prod/lobby/<lobbyID>/user/<userID>"`

### URL Parameters

Parameter | Description
--------- | -----------
lobbyID | The ID of the lobby in which to add the user
userID  | The user to add to the lobby
