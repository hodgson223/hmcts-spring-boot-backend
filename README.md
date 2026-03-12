# Task Service (Spring Boot Backend)

This project is a Spring Boot backend service for managing tasks. It provides a REST API that allows other services, such as an Express API gateway or a React frontend, to create, retrieve, and delete tasks.

The service uses Spring Boot, Spring Data JPA, and a relational database to store task information.

## Features

- Retrieve all tasks
- Create new tasks
- Delete tasks by ID
- JPA persistence with a Task entity
- Repository layer using Spring Data JPA
- Service layer for business logic
- REST controller exposing task endpoints

## Technology Stack

- Java
- Spring Boot
- Spring Web
- Spring Data JPA
- Jakarta Persistence API
- Maven or Gradle
- Relational Database (for example H2, MySQL, or PostgreSQL)

## Project Structure

```text
src/main/java/com/example/taskservice
├── controller
│   └── TaskController.java
├── model
│   └── Task.java
├── repository
│   └── TaskRepository.java
└── service
    └── TaskService.java
```

## Task Entity

The `Task` entity represents a task stored in the database.

Fields:

- `id` – unique identifier
- `title` – task title (required)
- `description` – optional description
- `status` – task status (required)
- `dueDate` – due date (required)

Example JSON:

```json
{
  "id": 1,
  "title": "Finish project",
  "description": "Complete backend implementation",
  "status": "Pending",
  "dueDate": "2026-03-20"
}
```

## API Endpoints

Base path:

```text
/internal/tasks
```

### Get All Tasks

```http
GET /internal/tasks
```

Returns a list of all tasks.

### Create Task

```http
POST /internal/tasks
```

Creates a new task.

Example request:

```json
{
  "title": "Finish project",
  "description": "Complete backend implementation",
  "status": "Pending",
  "dueDate": "2026-03-20"
}
```

### Delete Task

```http
DELETE /internal/tasks/{id}
```

Deletes a task by ID.

Example:

```http
DELETE /internal/tasks/1
```

If the task does not exist, the API returns `404 Task not found`.

## Service Layer

The `TaskService` handles business logic between the controller and the repository.

Responsibilities:

- Retrieve tasks from the repository
- Save new tasks
- Validate existence before deletion

## Repository Layer

The `TaskRepository` extends `JpaRepository` and provides built-in CRUD operations such as:

- `findAll()`
- `save()`
- `existsById()`
- `deleteById()`

No additional implementation is required.

## Running the Application

Make sure you have:

- Java installed
- Maven or Gradle installed

Start the application using:

```bash
mvn spring-boot:run
```

or

```bash
./gradlew bootRun
```

The service will run on:

```text
http://localhost:8080
```

## System Architecture Diagram

```text
+------------------+
|    React App     |
|  Frontend UI     |
+------------------+
         |
         | HTTP requests
         v
+------------------+
|  Express Gateway |
|   API Layer      |
+------------------+
         |
         | Forwards requests
         v
+------------------------+
| Spring Boot Backend    |
| Task Service API       |
+------------------------+
         |
         | JPA / Repository
         v
+------------------------+
|       Database         |
|   tasks table storage  |
+------------------------+
```

## How the Architecture Works

1. The React frontend sends requests to the Express gateway.
2. The Express gateway forwards task requests to the Spring Boot backend.
3. The Spring Boot backend processes the request using the controller, service, and repository layers.
4. The repository interacts with the database to store or retrieve task data.
5. The response is sent back through the gateway to the frontend.

## Integration

This backend is designed to work with:

- a React frontend application
- an Express API gateway

## Author

Developed as part of a university project demonstrating REST API development using Spring Boot and JPA.
