# Task Manager

A sample Spring Boot REST API for managing tasks. Built to demonstrate a
standard layered architecture (controller → service → repository) plus a
GitHub Actions CI/CD pipeline.

## Tech stack

- Java 21
- Spring Boot 3.3.x (Web, Data JPA, Validation)
- H2 in-memory database
- JUnit 5 + Spring MockMvc
- Maven

## Run locally

```bash
cd task-manager
mvn spring-boot:run
```

The API starts on `http://localhost:8080`.

## Endpoints

| Method | Endpoint      | Description        |
|--------|---------------|--------------------|
| GET    | `/tasks`      | List all tasks     |
| GET    | `/tasks/{id}` | Get one task       |
| POST   | `/tasks`      | Create a task      |
| PUT    | `/tasks/{id}` | Update a task      |
| DELETE | `/tasks/{id}` | Delete a task      |

### Example

```bash
# Create a task
curl -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Buy groceries","description":"Milk and eggs","completed":false}'

# List tasks
curl http://localhost:8080/tasks
```

## Test

```bash
cd task-manager
mvn test
```

## CI/CD

Every push and pull request to `main` triggers
[`.github/workflows/ci.yml`](.github/workflows/ci.yml), which:

1. Checks out the code
2. Sets up JDK 21 (Temurin) with Maven caching
3. Runs `mvn -B verify` (compile + test + package)
4. Uploads the built JAR as a workflow artifact

## Project layout

```
task-manager/
├── pom.xml
├── .github/workflows/ci.yml
└── src/
    ├── main/java/com/example/taskmanager/
    │   ├── TaskManagerApplication.java
    │   ├── controller/TaskController.java
    │   ├── model/Task.java
    │   ├── repository/TaskRepository.java
    │   └── service/TaskService.java
    ├── main/resources/application.properties
    └── test/java/com/example/taskmanager/
        ├── TaskManagerApplicationTests.java
        └── controller/TaskControllerTest.java
```
