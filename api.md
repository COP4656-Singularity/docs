
# JSON Schema

## User

```javascript
“user”: {
	“self”: href,
	“passwordHash”: string
	“email”: string
	“firstName”: string,
	“lastName”: string,
	“thumbnail”: base64
}
```

## To Do List

```javascript
"todo": {
	“self”: href,
	“version”: int,
	“name”: string,
	“owner”: href,
	“acl”: [
		href
	]
	“tasks”: [ {
		“name”: string,
		“note”: string,
		“complete” : boolean,
		“subtasks” : {
			“name”: string,
			“note”: string,
            “complete”: boolean
			}
		}
	]
}
```

# REST API

All methods assume a user is authenticated. All URLs are limited to the current user context.

## POST /login
Accepts a username and password form variables. Authenticates the user. If successful returns HTTP 200 and href of user. HTTP 401 otherwise. Think about OAuth access token...

## GET /user
Returns user object for the current user.

## POST /user
Creates new user. Read: registration.

## PUT /user/{id}
Updates the user object if the user represents the current user.

## GET /friend
Returns list of user objects representing friends of the current user.

## GET /friend/{id}
Returns a specific user object for a friend of the current user.

## DELETE /friend/{id}
Removes a friend from the current user’s friend list.

## GET /todo
Returns list of todo objects for the current user.

## GET /todo/{id}
Returns a specific todo object if the object is owned by the current user or permitted to view.

## POST /todo
Creates a new todo list.

## PUT /todo/{id}
Updates a given todo list. See: revision guard.

## DELETE /todo/{id}
Deletes a given todo list.
