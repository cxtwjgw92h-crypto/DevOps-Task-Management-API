# Task Management REST API

A small Spring Boot REST API for creating and retrieving tasks. Tasks are stored in an in-memory list, so they are cleared whenever the application stops. No database or user interface is used.

## Files

- `pom.xml` declares the project, Java 17, Spring Boot web and validation dependencies, and the Maven packaging plugin.
- `src/main/java/com/example/taskmanagement/TaskManagementApplication.java` is the Spring Boot entry point.
- `src/main/java/com/example/taskmanagement/controller/TaskController.java` implements `GET /todos`, `POST /todos`, and `GET /todos/{id}` and stores tasks in memory.
- `src/main/java/com/example/taskmanagement/model/Task.java` defines the task returned as JSON.
- `src/main/java/com/example/taskmanagement/model/CreateTaskRequest.java` defines and validates the JSON body for creating a task.
- `src/main/resources/application.properties` configures the server to use port 8080.

## Build and run

Install Java 17 and Maven, then run these commands from the project root:

```sh
mvn clean package
mvn spring-boot:run
```

The API will be available at `http://localhost:8080`. The packaged application can also be started with:

```sh
java -jar target/task-management-api-0.0.1-SNAPSHOT.jar
```

## Try the endpoints

Retrieve all tasks (initially an empty array):

```sh
curl -i http://localhost:8080/todos
```

Create a task. A successful request returns `201 Created` and the new task JSON:

```sh
curl -i -X POST http://localhost:8080/todos -H "Content-Type: application/json" -d '{"title":"Prepare DevOps assignment"}'
```

Retrieve a task using its ID (the first created task has ID 1):

```sh
curl -i http://localhost:8080/todos/1
```

Task titles must contain non-whitespace text. Invalid request bodies receive `400 Bad Request`; an unknown task ID receives `404 Not Found`.

