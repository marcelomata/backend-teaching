# Web Applications and API Development Tutorial

## Table of Contents

1. [Computer Network](#computer-network)
2. [Internet](#internet)
3. [HTTP/HTTPS](#httphttps)
    - [HTTP Methods](#http-methods)
    - [HTTP Status Codes](#http-status-codes)
    - [HTTP Headers](#http-headers)
    - [HTTP Message Structure](#http-message-structure)
4. [RESTful APIs](#restful-apis)
    - [Example Employee API](#example-employee-api)
5. [Spring Framework Overview](#spring-framework-overview)
    - [Basic Example](#basic-example)
6. [Maven Overview](#maven-overview)
7. [cURL Overview](#curl-overview)
    - [Example cURL Commands](#example-curl-commands)
8. [Building the Employee API with Spring](#building-the-employee-api-with-spring)
    - [Spring Controllers](#spring-controllers)
    - [The Entity Class](#the-entity-class)
    - [Spring Services](#spring-services)
    - [Storing Data in Memory](#storing-data-in-memory)
    - [Testing with cURL](#testing-with-curl)
9. [Introduction to Containers and Docker](#introduction-to-containers-and-docker)
    - [What is a Container?](#what-is-a-container)
    - [What is Docker?](#what-is-docker)
    - [Basic Docker Commands](#basic-docker-commands)
10. [Introduction to Databases](#introduction-to-databases)
    - [What is MySQL?](#what-is-mysql)
    - [Running MySQL in a Docker Container](#running-mysql-in-a-docker-container)
11. [Integrating Spring with MySQL](#integrating-spring-with-mysql)
    - [Adding Database Dependencies](#adding-database-dependencies)
    - [Configuring the Database Connection](#configuring-the-database-connection)
    - [Spring Repositories](#spring-repositories)
    - [Updating the Entity for JPA](#updating-the-entity-for-jpa)
    - [Updating the Service to Use the Repository](#updating-the-service-to-use-the-repository)
12. [Testing the Complete Application](#testing-the-complete-application)
13. [Exercises for the Reader](#exercises-for-the-reader)
14. [Conclusion](#conclusion)

## Computer Network

A computer network is a collection of interconnected devices (such as computers, servers, smartphones, and other hardware) that communicate with each other to share resources and information. These devices are linked through various types of communication mediums, including wired connections (like Ethernet cables) and wireless connections (like Wi-Fi).

## Internet

The internet is a vast, global network of interconnected computer networks that communicate with each other using standardized protocols. It enables the exchange of data and resources among billions of devices worldwide, including computers, servers, smartphones, and other connected devices.

## HTTP/HTTPS

### HTTP Methods

- **GET**: Retrieve data from the server. Used for reading resources.
- **POST**: Send data to the server to create a new resource.
- **PUT**: Update an existing resource with new data.
- **PATCH**: Apply partial modifications to a resource.
- **DELETE**: Remove a resource from the server.
- **HEAD**: Retrieve headers for a resource, similar to GET but without the response body.
- **OPTIONS**: Describe the communication options for the target resource.
- **TRACE**: Perform a message loop-back test along the path to the target resource.

### HTTP Status Codes

- **1xx (Informational)**: Request received, continuing process.
    - 100 Continue
    - 101 Switching Protocols
- **2xx (Success)**: The action was successfully received, understood, and accepted.
    - 200 OK
    - 201 Created
    - 204 No Content
- **3xx (Redirection)**: Further action needs to be taken to complete the request.
    - 301 Moved Permanently
    - 302 Found
    - 304 Not Modified
- **4xx (Client Error)**: The request contains bad syntax or cannot be fulfilled.
    - 400 Bad Request
    - 401 Unauthorized
    - 403 Forbidden
    - 404 Not Found
- **5xx (Server Error)**: The server failed to fulfill a valid request.
    - 500 Internal Server Error
    - 502 Bad Gateway
    - 503 Service Unavailable

### HTTP Headers

Request/Response Headers (key: value):
- `Content-Type`: Indicates the media type of the resource being sent to the server.
- `Host`: Specifies the domain name of the server and the TCP port number.

### HTTP Message Structure

**Request Message**:
- Request Line: Method, URL, and HTTP version (e.g., GET /index.html HTTP/1.1).
- Headers: Key-value pairs that convey additional information (e.g., Host: www.example.com).
- Body: Optional data payload (e.g., form data in a POST request).

**Response Message**:
- Status Line: HTTP version, status code, and status message (e.g., HTTP/1.1 200 OK).
- Headers: Key-value pairs that convey additional information (e.g., Content-Type: text/html).
- Body: Optional data payload (e.g., HTML content of the web page).

## RESTful APIs

REST (Representational State Transfer) is an architectural style for designing networked applications. RESTful APIs use HTTP requests to perform CRUD (Create, Read, Update, Delete) operations.

### Example Employee API

Here is an example of a set of API endpoints to handle employee-related operations. This API will cover basic CRUD functionalities and some additional endpoints for searching and filtering employees.


#### Create a New Employee

**Endpoint:** `POST /api/employees`

**Description:** Create a new employee.

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "position": "Software Engineer",
  "salary": 60000,
  "department": "Engineering"
}
```

**Response:**
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "johndoe@example.com",
  "position": "Software Engineer",
  "salary": 60000,
  "department": "Engineering"
}
```

---

#### Get All Employees

**Endpoint:** `GET /api/employees`

**Description:** Retrieve a list of all employees.

**Response:**
```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "johndoe@example.com",
    "position": "Software Engineer",
    "salary": 60000,
    "department": "Engineering"
  },
  {
    "id": 2,
    "name": "Jane Smith",
    "email": "janesmith@example.com",
    "position": "Product Manager",
    "salary": 80000,
    "department": "Product"
  }
]
```

---

#### Get a Single Employee by ID

**Endpoint:** `GET /api/employees/{id}`

**Description:** Retrieve details of a single employee by their ID.

**Response:**
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "johndoe@example.com",
  "position": "Software Engineer",
  "salary": 60000,
  "department": "Engineering"
}
```

---

#### Update an Employee

**Endpoint:** `PUT /api/employees/{id}`

**Description:** Update the details of an existing employee.

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "position": "Senior Software Engineer",
  "salary": 70000,
  "department": "Engineering"
}
```

**Response:**
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "johndoe@example.com",
  "position": "Senior Software Engineer",
  "salary": 70000,
  "department": "Engineering"
}
```

---

#### Delete an Employee

**Endpoint:** `DELETE /api/employees/{id}`

**Description:** Delete an employee by their ID.

**Response:**
```json
{
  "message": "Employee deleted successfully"
}
```

---

#### Search Employees by Name

**Endpoint:** `GET /api/employees/search`

**Description:** Search for employees by name.

**Query Parameters:** `name`

**Example:** `GET /api/employees/search?name=John`

**Response:**
```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "johndoe@example.com",
    "position": "Software Engineer",
    "salary": 60000,
    "department": "Engineering"
  }
]
```

---

#### Filter Employees by Department

**Endpoint:** `GET /api/employees/filter`

**Description:** Filter employees by department.

**Query Parameters:** `department`

**Example:** `GET /api/employees/filter?department=Engineering`

**Response:**
```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "johndoe@example.com",
    "position": "Software Engineer",
    "salary": 60000,
    "department": "Engineering"
  }
]
```

This structure provides a comprehensive set of endpoints to manage employee data, following RESTful principles, and covers common operations needed in a backend system.

---

### Spring Framework Overview

Spring makes it easy to create Java enterprise applications. It has libraries to help develop APIs (Spring MVC), communicate with databases (Spring JPA), configure (Spring Boot), among several other features.

**Basic Example**

Here's a simple example to illustrate the basic usage of the Spring Framework (using Maven):

1. **Create a Spring Boot Application:**

    **Project Structure:**
    ```
    ├── src
    │   ├── main
    │   │   ├── java
    │   │   │   └── com
    │   │   │       └── employeeservice
    │   │   │           ├── EmployeeServiceApplication.java
    │   │   │           └── GreetingController.java
    │   │   └── resources
    │   │       └── application.properties
    └── pom.xml
    ```

    **pom.xml:**
    ```xml
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    ```

    **EmployeeServiceApplication.java:**
    ```java
    package com.employeeservice;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    @SpringBootApplication
    public class EmployeeServiceApplication {
        public static void main(String[] args) {
            SpringApplication.run(EmployeeServiceApplication.class, args);
        }
    }
    ```

    **GreetingController.java:**
    ```java
    package com.employeeservice;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class GreetingController {

        @GetMapping("/greeting")
        public String greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
            return "Hello, " + name;
        }
    }
    ```

2. **Run the Application:**

    Use Maven to build and run the application:
    ```
    mvn spring-boot:run
    ```

3. **Test the Application:**

    Open the terminal and use the command:
    ```
    curl -X GET http://localhost:8080/greeting?name=Spring
    ```

    You should see the response:
    ```
    Hello, Spring
    ```

---

### Maven Overview

Maven is a powerful build automation tool primarily used for Java projects. It helps manage project dependencies, build processes, and project lifecycles in a standardized and efficient way.

**Key Features**

- **Project Management:** Maven uses a standard project structure and conventions, making it easier to understand and maintain projects.
- **Dependency Management:** Automatically handles downloading and updating project dependencies.
- **Build Automation:** Automates compilation, testing, packaging, and deployment of projects.
- **Plugins:** Extensible via plugins for additional functionalities, such as generating reports, documentation, etc.
- **Reproducible Builds:** Ensures consistent builds across different environments.

The `pom.xml` file is the heart of a Maven project. It contains project information, configuration details, dependencies, plugins, and more.

---

### cURL Overview

cURL is a command-line tool and library for transferring data with URLs. It is widely used for interacting with web servers, APIs, and various protocols (HTTP, FTP, etc.).

**Example of using cURL to access the Employee API:**

1. **Create a New Employee**

    **Endpoint:** `POST /api/employees`
    ```
    curl -X POST http://localhost:8080/api/employees \
         -H "Content-Type: application/json" \
         -d '{
               "name": "John Doe",
               "email": "johndoe@example.com",
               "position": "Software Engineer",
               "salary": 60000,
               "department": "Engineering"
             }'
    ```

2. **Get All Employees**

    **Endpoint:** `GET /api/employees`
    ```
    curl -X GET http://localhost:8080/api/employees
    ```

3. **Get a Single Employee by ID**

    **Endpoint:** `GET /api/employees/{id}`
    ```
    curl -X GET http://localhost:8080/api/employees/1
    ```

4. **Update an Employee**

    **Endpoint:** `PUT /api/employees/{id}`
    ```
    curl -X PUT http://localhost:8080/api/employees/1 \
         -H "Content-Type: application/json" \
         -d '{
               "name": "John Doe",
               "email": "johndoe@example.com",
               "position": "Senior Software Engineer",
               "salary": 70000,
               "department": "Engineering"
             }'
    ```

5. **Delete an Employee**

    **Endpoint:** `DELETE /api/employees/{id}`
    ```
    curl -X DELETE http://localhost:8080/api/employees/1
    ```

6. **Search Employees by Name**

    **Endpoint:** `GET /api/employees/search`
    ```
    curl -X GET "http://localhost:8080/api/employees/search?name=John"
    ```

7. **Filter Employees by Department**

    **Endpoint:** `GET /api/employees/filter`
    ```
    curl -X GET "http://localhost:8080/api/employees/filter?department=Engineering"
    ```

---

## Building the Employee API with Spring

Now let's build a real implementation of the Employee API using Spring Boot. We'll start simple by storing data in memory, then later connect to a real database.

### Spring Controllers

A **Controller** in Spring is a class that handles HTTP requests. It receives requests from clients, processes them (usually by calling a service), and returns a response.

Key annotations:
- `@RestController`: Marks the class as a REST controller that returns data (JSON) instead of views (HTML).
- `@RequestMapping`: Defines the base URL path for all endpoints in the controller.
- `@GetMapping`, `@PostMapping`: Map specific HTTP methods to handler methods.
- `@RequestBody`: Converts the JSON request body into a Java object.

**EmployeeController.java:**
```java
package com.employeeservice.controller;

import com.employeeservice.model.Employee;
import com.employeeservice.service.EmployeeService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/employees")
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    @PostMapping
    public ResponseEntity<Employee> createEmployee(@RequestBody Employee employee) {
        Employee created = employeeService.createEmployee(employee);
        return new ResponseEntity<>(created, HttpStatus.CREATED);
    }

    @GetMapping
    public ResponseEntity<List<Employee>> getAllEmployees() {
        List<Employee> employees = employeeService.getAllEmployees();
        return new ResponseEntity<>(employees, HttpStatus.OK);
    }
}
```

The controller delegates the business logic to the **Service** layer. This separation keeps the code organized and easier to maintain.

---

### The Entity Class

An **Entity** represents the data model of your application. It defines the structure of the data that will be stored and transferred.

**Employee.java:**
```java
package com.employeeservice.model;

public class Employee {

    private Long id;
    private String name;
    private String email;
    private String position;
    private Double salary;
    private String department;

    // Default constructor
    public Employee() {}

    // Constructor with parameters
    public Employee(Long id, String name, String email, String position, Double salary, String department) {
        this.id = id;
        this.name = name;
        this.email = email;
        this.position = position;
        this.salary = salary;
        this.department = department;
    }

    // Getters and Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPosition() {
        return position;
    }

    public void setPosition(String position) {
        this.position = position;
    }

    public Double getSalary() {
        return salary;
    }

    public void setSalary(Double salary) {
        this.salary = salary;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }
}
```

---

### Spring Services

A **Service** in Spring contains the business logic of your application. It processes data, applies rules, and coordinates operations between the controller and data storage.

Key annotations:
- `@Service`: Marks the class as a service component, allowing Spring to manage it automatically.

**EmployeeService.java:**
```java
package com.employeeservice.service;

import com.employeeservice.model.Employee;
import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.List;

@Service
public class EmployeeService {

    private List<Employee> employees = new ArrayList<>();
    private Long nextId = 1L;

    public Employee createEmployee(Employee employee) {
        employee.setId(nextId++);
        employees.add(employee);
        return employee;
    }

    public List<Employee> getAllEmployees() {
        return employees;
    }
}
```

---

### Storing Data in Memory

In the service above, we use an `ArrayList` to store employees in memory. This is a simple approach for learning and testing, but has limitations:

- **Data is lost** when the application restarts
- **Not suitable for production** - real applications need persistent storage
- **No concurrent access handling** - multiple requests could cause issues

This approach is useful for:
- Learning and prototyping
- Unit testing
- Simple demos

**Project Structure:**
```
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── employeeservice
│   │   │           ├── EmployeeServiceApplication.java
│   │   │           ├── controller
│   │   │           │   └── EmployeeController.java
│   │   │           ├── model
│   │   │           │   └── Employee.java
│   │   │           └── service
│   │   │               └── EmployeeService.java
│   │   └── resources
│   │       └── application.properties
└── pom.xml
```

---

### Testing with cURL

Run the application:
```bash
mvn spring-boot:run
```

Test creating an employee:
```bash
curl -X POST http://localhost:8080/api/employees \
     -H "Content-Type: application/json" \
     -d '{
           "name": "John Doe",
           "email": "john@example.com",
           "position": "Developer",
           "salary": 60000,
           "department": "Engineering"
         }'
```

Expected response:
```json
{"id":1,"name":"John Doe","email":"john@example.com","position":"Developer","salary":60000.0,"department":"Engineering"}
```

Test getting all employees:
```bash
curl -X GET http://localhost:8080/api/employees
```

---

## Introduction to Containers and Docker

### What is a Container?

A **container** is a lightweight, standalone package that contains everything needed to run a piece of software:
- The application code
- Runtime environment
- Libraries and dependencies
- Configuration files

**Benefits of containers:**
- **Consistency**: Works the same on any machine (your laptop, server, cloud)
- **Isolation**: Each container runs independently, avoiding conflicts
- **Portability**: Easy to move between environments
- **Efficiency**: Lighter than virtual machines, starts in seconds

Think of a container like a shipping container: it packages everything together so it can be transported anywhere without worrying about what's inside.

---

### What is Docker?

**Docker** is the most popular platform for creating and running containers. It provides:
- **Docker Engine**: Runs containers on your machine
- **Docker Hub**: A registry to share and download container images
- **Docker Compose**: Tool to run multiple containers together

**Key concepts:**
- **Image**: A template with instructions to create a container (like a recipe)
- **Container**: A running instance of an image (like a dish made from the recipe)
- **Dockerfile**: A text file with instructions to build an image

---

### Basic Docker Commands

```bash
# Check Docker version
docker --version

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Pull an image from Docker Hub
docker pull mysql:8.0

# Run a container
docker run -d --name my-container image-name

# Stop a container
docker stop container-name

# Start a stopped container
docker start container-name

# Remove a container
docker rm container-name

# View container logs
docker logs container-name
```

---

## Introduction to Databases

### What is MySQL?

**MySQL** is one of the most popular relational databases in the world. A **relational database** stores data in tables with rows and columns, similar to a spreadsheet.

**Key concepts:**
- **Table**: Stores data about one type of entity (e.g., employees)
- **Row**: A single record (e.g., one employee)
- **Column**: A specific attribute (e.g., name, email, salary)
- **Primary Key**: Unique identifier for each row (e.g., employee ID)
- **SQL**: Language used to query and manipulate data

**Example of an employees table:**

| id | name      | email              | position  | salary |
|----|-----------|--------------------|-----------|---------|
| 1  | John Doe  | john@example.com   | Developer | 60000  |
| 2  | Jane Smith| jane@example.com   | Manager   | 80000  |

---

### Running MySQL in a Docker Container

Instead of installing MySQL directly on your computer, we can run it in a Docker container. This is cleaner and easier to manage.

**1. Pull the MySQL image:**
```bash
docker pull mysql:8.0
```

**2. Run the MySQL container:**
```bash
docker run -d \
  --name mysql-container \
  -e MYSQL_ROOT_PASSWORD=rootpassword \
  -e MYSQL_DATABASE=employeedb \
  -e MYSQL_USER=appuser \
  -e MYSQL_PASSWORD=apppassword \
  -p 3306:3306 \
  mysql:8.0
```

**Explanation of the command:**
- `-d`: Run in background (detached mode)
- `--name mysql-container`: Name the container
- `-e MYSQL_ROOT_PASSWORD`: Set the root password
- `-e MYSQL_DATABASE`: Create a database on startup
- `-e MYSQL_USER`: Create a user
- `-e MYSQL_PASSWORD`: Set the user's password
- `-p 3306:3306`: Map port 3306 from container to your machine

**3. Check if it's running:**
```bash
docker ps
```

**4. Connect to MySQL (optional, for testing):**
```bash
docker exec -it mysql-container mysql -u appuser -p
```
Enter the password `apppassword` when prompted.

---

## Integrating Spring with MySQL

Now let's connect our Spring application to the MySQL database running in Docker.

### Adding Database Dependencies

Add these dependencies to your `pom.xml`:

```xml
<dependencies>
    <!-- Existing dependency -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
    <!-- JPA for database access -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    
    <!-- MySQL Driver -->
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <scope>runtime</scope>
    </dependency>
    
    <!-- Test dependency -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

### Configuring the Database Connection

Update `application.properties` to connect to MySQL:

```properties
# Database connection
spring.datasource.url=jdbc:mysql://localhost:3306/employeedb
spring.datasource.username=appuser
spring.datasource.password=apppassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA/Hibernate settings
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

**Explanation:**
- `spring.datasource.url`: Connection URL to the database
- `spring.jpa.hibernate.ddl-auto=update`: Automatically creates/updates tables based on entities
- `spring.jpa.show-sql=true`: Shows SQL queries in the console (useful for learning)

---

### Spring Repositories

A **Repository** in Spring is an interface that provides methods to interact with the database. Spring Data JPA automatically implements common operations like save, find, delete.

Key annotations:
- `@Repository`: Marks the interface as a repository component
- Extends `JpaRepository<Entity, IdType>`: Provides built-in CRUD methods

**EmployeeRepository.java:**
```java
package com.employeeservice.repository;

import com.employeeservice.model.Employee;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    // JpaRepository provides these methods automatically:
    // - save(Employee) - Create or update
    // - findById(Long) - Find by ID
    // - findAll() - Get all records
    // - deleteById(Long) - Delete by ID
    // - count() - Count records
}
```

That's it! No implementation needed. Spring generates the code automatically.

---

### Updating the Entity for JPA

To work with the database, we need to add JPA annotations to our entity:

**Employee.java (updated):**
```java
package com.employeeservice.model;

import jakarta.persistence.*;

@Entity
@Table(name = "employees")
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    @Column(unique = true)
    private String email;

    private String position;
    private Double salary;
    private String department;

    // Default constructor (required by JPA)
    public Employee() {}

    // Constructor with parameters
    public Employee(String name, String email, String position, Double salary, String department) {
        this.name = name;
        this.email = email;
        this.position = position;
        this.salary = salary;
        this.department = department;
    }

    // Getters and Setters (same as before)
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPosition() {
        return position;
    }

    public void setPosition(String position) {
        this.position = position;
    }

    public Double getSalary() {
        return salary;
    }

    public void setSalary(Double salary) {
        this.salary = salary;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }
}
```

**New annotations explained:**
- `@Entity`: Marks this class as a database entity
- `@Table(name = "employees")`: Specifies the table name
- `@Id`: Marks the primary key
- `@GeneratedValue(strategy = GenerationType.IDENTITY)`: Auto-generates IDs
- `@Column`: Configures column properties (nullable, unique, etc.)

---

### Updating the Service to Use the Repository

Now we replace the in-memory list with the repository:

**EmployeeService.java (updated):**
```java
package com.employeeservice.service;

import com.employeeservice.model.Employee;
import com.employeeservice.repository.EmployeeRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class EmployeeService {

    @Autowired
    private EmployeeRepository employeeRepository;

    public Employee createEmployee(Employee employee) {
        return employeeRepository.save(employee);
    }

    public List<Employee> getAllEmployees() {
        return employeeRepository.findAll();
    }
}
```

**What changed:**
- Removed the `ArrayList` and `nextId` counter
- Added `@Autowired EmployeeRepository` - Spring injects the repository automatically
- Used `employeeRepository.save()` instead of `employees.add()`
- Used `employeeRepository.findAll()` instead of returning the list

**Updated Project Structure:**
```
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── employeeservice
│   │   │           ├── EmployeeServiceApplication.java
│   │   │           ├── controller
│   │   │           │   └── EmployeeController.java
│   │   │           ├── model
│   │   │           │   └── Employee.java
│   │   │           ├── repository
│   │   │           │   └── EmployeeRepository.java
│   │   │           └── service
│   │   │               └── EmployeeService.java
│   │   └── resources
│   │       └── application.properties
└── pom.xml
```

---

## Testing the Complete Application

Now let's test the complete application with the database.

**1. Make sure MySQL is running:**
```bash
docker ps
# If not running:
docker start mysql-container
```

**2. Start the Spring application:**
```bash
mvn spring-boot:run
```

You should see in the console that Hibernate creates the `employees` table automatically.

**3. Test creating employees:**
```bash
# Create first employee
curl -X POST http://localhost:8080/api/employees \
     -H "Content-Type: application/json" \
     -d '{
           "name": "John Doe",
           "email": "john@example.com",
           "position": "Developer",
           "salary": 60000,
           "department": "Engineering"
         }'

# Create second employee
curl -X POST http://localhost:8080/api/employees \
     -H "Content-Type: application/json" \
     -d '{
           "name": "Jane Smith",
           "email": "jane@example.com",
           "position": "Manager",
           "salary": 80000,
           "department": "Product"
         }'
```

**4. Test getting all employees:**
```bash
curl -X GET http://localhost:8080/api/employees
```

Expected response:
```json
[
  {"id":1,"name":"John Doe","email":"john@example.com","position":"Developer","salary":60000.0,"department":"Engineering"},
  {"id":2,"name":"Jane Smith","email":"jane@example.com","position":"Manager","salary":80000.0,"department":"Product"}
]
```

**5. Verify data persistence:**

Stop the application (Ctrl+C), then start it again:
```bash
mvn spring-boot:run
```

Check the employees:
```bash
curl -X GET http://localhost:8080/api/employees
```

The data is still there! Unlike the in-memory version, data persists because it's stored in MySQL.

---

## Exercises for the Reader

Now that you have a working API with Create and Get All endpoints, try implementing the remaining endpoints on your own:

1. **Get Employee by ID** (`GET /api/employees/{id}`)
   - Add a method in the Controller using `@GetMapping("/{id}")`
   - Use `@PathVariable` to get the ID from the URL
   - Add a method in the Service using `employeeRepository.findById()`

2. **Update Employee** (`PUT /api/employees/{id}`)
   - Add a method in the Controller using `@PutMapping("/{id}")`
   - Find the employee, update the fields, and save it back

3. **Delete Employee** (`DELETE /api/employees/{id}`)
   - Add a method in the Controller using `@DeleteMapping("/{id}")`
   - Use `employeeRepository.deleteById()` in the Service

4. **Search by Name** (`GET /api/employees/search?name=John`)
   - Use `@RequestParam` to get the query parameter
   - Create a custom query method in the Repository

5. **Filter by Department** (`GET /api/employees/filter?department=Engineering`)
   - Similar to search, but filter by department

**Hint:** The `JpaRepository` provides many useful methods. You can also define custom queries by following Spring Data JPA naming conventions (e.g., `findByName`, `findByDepartment`).

---

## Conclusion

In this tutorial, you learned:

1. **Networking Basics**: How computer networks and the internet work
2. **HTTP Protocol**: Methods, status codes, headers, and message structure
3. **RESTful APIs**: Designing endpoints following REST principles
4. **Spring Framework**: Building web applications with Java
5. **Maven**: Managing dependencies and building projects
6. **cURL**: Testing APIs from the command line
7. **Spring Controllers**: Handling HTTP requests
8. **Spring Services**: Implementing business logic
9. **Containers & Docker**: Running applications in isolated environments
10. **MySQL Database**: Storing data persistently
11. **Spring Repositories**: Interacting with databases using JPA

**Architecture Summary:**

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Client    │────▶│ Controller  │────▶│   Service   │────▶│ Repository  │
│   (cURL)    │◀────│             │◀────│             │◀────│             │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
                                                                   │
                                                                   ▼
                                                            ┌─────────────┐
                                                            │   MySQL     │
                                                            │  (Docker)   │
                                                            └─────────────┘
```

**Next Steps:**
- Add update (PUT) and delete (DELETE) endpoints
- Implement input validation
- Add error handling
- Learn about security with Spring Security
- Explore Docker Compose for running multiple containers

Happy coding!