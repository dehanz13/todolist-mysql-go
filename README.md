# Todo List API server + React Frontend

This is a simple and classic Todo List API server built with Golang that connects to a Frontend page. As part of this exercise, I decided to use MySQL + Docker to handle the backend and React for frontend.

## Prerequisites

- Golang & Docker installed in your system
- A basic Golang & JQuery knowledge

## Tech Stack

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

## ORM Model
Our TodoItem `struct` consists of:
- Id: int - This is our _*primary_key*_
- Description: string - This is what we will display in our Frontend UI
- Completed: boolean - This is to determine if the todo item is completed or not

---

### Helpful Commands:

#### Docker Commands
```bash

# launch a MySQL container and expose the port 3306 to the localhost
> docker run -d -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=root mysql
# spin up the docker container to have our MySQL database server up
> docker exec -it mysql mysql -uroot -proot -e 'CREATE DATABASE todolist'

# running mysql on a separate terminal
> docker exec -it mysql mysql -uroot -proot
```

#### MySQL Commands

> Run this on a separate terminal (#2)

```sql
mysql> use todolist;
Database changed
mysql> show tables;
+--------------------+
| Tables_in_todolist |
+--------------------+
| todo_item_models   |
+--------------------+
1 row in set (0.020 sec)
mysql> SELECT * FROM todo_item_models;
+----+--------------+-----------+
| id | description  | completed |
+----+--------------+-----------+
|  1 | Run 10 Miles |         0 |
+----+--------------+-----------+
1 row in set (0.001 sec)
mysql> 
```

#### Go Commands
```bash
# initial part of the app
go init todolist-mysql-go
cd /src
# run Auto-migration against our MySQL database immediately after starting our API server
go mod tidy
go run todolist.go
```

#### Curl commands to call API endpoints:

> Run this on a separate terminal (#3)

##### Check app healthz:
```bash
curl -i localhost:8000/healthz   
```
##### Create a todo item:
```bash
curl -i -X POST -d "description=Run 10 Miles" localhost:8000/todo
```
##### Get all the completed todo items from database:
```bash
curl -i GET localhost:8000/todo-completed
```
##### Get all the incomplete todo item from database:
```bash
curl -i GET localhost:8000/todo-incomplete
```
##### Complete a todo item:
```bash
curl -i -X POST -d "completed=true" localhost:8000/todo/1
```
##### Delete a todo item from database:
```bash
curl -i -X DELETE -d "deleted=true" localhost:8000/todo/1
```