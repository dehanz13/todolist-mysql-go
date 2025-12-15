# Todo List API server + React Frontend

This is a simple and classic Todo List API server built with Golang that connects to a Frontend page. As part of this exercise, I decided to use MySQL + Docker to handle the backend and React for frontend.

## Prerequisites

- Golang & Docker installed in your system
- A basic Golang & JQuery knowledge

## Tech Stackx

- MySQL as our DB
- GORM as ORM for interacting with our DB
- Request router using gorilla/mux
- Logrus for logging

## API Server Specs
- It listens to port ```8000``` on localhost
- It has 5 endpoints:
  1. ```healthz```
  2. ```createItem```
  3. ```getCompletedItems```
  4. ```getIncompleteItems```
  5. ```updateItems```
  6. ```deleteItem```


### Helpful Commands:

```sql
SELECT * FROM todo_list_table;

```

```go
go init todolist-mysql-go
cd /src

go mod tidy
go run todolist.go
```