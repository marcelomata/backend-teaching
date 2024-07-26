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
  "department": "Engineering",
  "createdAt": "2023-01-01T12:00:00Z"
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
  "department": "Engineering",
  "updatedAt": "2023-01-02T12:00:00Z"
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
    │   │   │       └── example
    │   │   │           └── demo
    │   │   │               ├── DemoApplication.java
    │   │   │               └── GreetingController.java
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

    **DemoApplication.java:**
    ```java
    package com.example.demo;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    @SpringBootApplication
    public class DemoApplication {
        public static void main(String[] args) {
            SpringApplication.run(DemoApplication.class, args);
        }
    }
    ```

    **GreetingController.java:**
    ```java
    package com.example.demo;

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
    curl -X POST http://localhost:8080/api/employees          -H "Content-Type: application/json"          -d '{
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
    curl -X PUT http://localhost:8080/api/employees/1          -H "Content-Type: application/json"          -d '{
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
    curl -X GET http://localhost:8080/api/employees/search?name=John
    ```

7. **Filter Employees by Department**

    **Endpoint:** `GET /api/employees/filter`
    ```
    curl -X GET http://localhost:8080/api/employees/filter?department=Engineering
    ```