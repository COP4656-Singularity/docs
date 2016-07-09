
# JSON Schema

## 'lists' table
Unstructured list of all list objects.  Each 'list' corresonds with a single to-do list for a single user.

```javascript
{
  "N": "id",    // int64 datetime stamp at object creation
  "S": "name",  // string of list name
  "S": "note"   // string of list description
}
```

## 'tasks' table
Unstructured list of all tasks.   Each 'task' is associated with a single item from the lists table.

```javascript
{
  "N": "id",    // int64 datetime stamp at object creation
  "N": "parent," // int64 datetime stamp of parent container
  "S": "name",  // string of list name
  "S": "note"   // string of list description
}
```

# Not yet implemented
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

API to support the Singularity Mobile To-Do App
## GET /list
Returns list objects for the current user.

## POST /list
Creates a new to-do list.

## GET /list/{id}
Returns a a specific list object if the object is owned by the current user or permitted to view.

## DELETE /list/{id}
Deletes a single to-do list based on the ID supplied

## POST /task
Adds a task to a given list.

## GET /task/withparent/{id}
Returns a set of tasks having the specified parent.

## GET /task/{id}
Returns a task object.

## DELETE /task/{id}
Deletes a single to-do list based on the ID supplied

# Not Currently Impemented

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
