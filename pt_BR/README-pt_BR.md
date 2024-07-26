# Web Applications and API Development Tutorial

## Índice

1. [Rede de Computadores](#computer-network)
2. [Internet](#internet)
3. [HTTP/HTTPS](#httphttps)
    - [Métodos HTTP](#http-methods)
    - [HTTP Status Codes](#http-status-codes)
    - [HTTP Headers](#http-headers)
    - [Estrutura de Mensagem HTTP](#http-message-structure)
4. [APIs RESTful](#restful-apis)
    - [Exemplo de API de Funcionários](#example-employee-api)
5. [Visão Geral do Spring Framework](#spring-framework-overview)
    - [Exemplo Básico](#basic-example)
6. [Visão Geral do Maven](#maven-overview)
7. [Visão Geral do cURL](#curl-overview)
    - [Example cURL Commands](#example-curl-commands)

## Rede de Computadores

A computer network is a collection of interconnected devices (such as computers, servers, smartphones, and other hardware) that communicate with each other to share resources and information. These devices are linked through various types of communication mediums, including wired connections (like Ethernet cables) and wireless connections (like Wi-Fi).

## Internet

The internet is a vast, global network of interconnected computer networks that communicate with each other using standardized protocols. It enables the exchange of data and resources among billions of devices worldwide, including computers, servers, smartphones, and other connected devices.

## HTTP/HTTPS

### Métodos HTTP

- **GET**: Recuperar dados do servidor. Used for reading resources.
- **POST**: Enviar dados para o servidor para criar um novo recurso.
- **PUT**: Atualizar um recurso existente com novos dados.
- **PATCH**: Aplicar modificações parciais a um recurso.
- **DELETE**: Remover um recurso do servidor.
- **HEAD**: Recuperar cabeçalhos de um recurso, similar to GET but without the response body.
- **OPTIONS**: Descrever as opções de comunicação para o recurso alvo.
- **TRACE**: Executar um teste de loop-back de mensagem ao longo do caminho para o recurso alvo.

### HTTP Status Codes

- **1xx (Informational)**: Solicitação recebida, continuando o processo.
    - 100 Continue
    - 101 Switching Protocols
- **2xx (Success)**: A ação foi recebida com sucesso, compreendida e aceita.
    - 200 OK
    - 201 Created
    - 204 No Content
- **3xx (Redirection)**: Ação adicional precisa ser tomada para completar a solicitação.
    - 301 Moved Permanently
    - 302 Found
    - 304 Not Modified
- **4xx (Client Error)**: A solicitação contém sintaxe incorreta ou não pode ser atendida.
    - 400 Bad Request
    - 401 Unauthorized
    - 403 Forbidden
    - 404 Not Found
- **5xx (Server Error)**: O servidor não conseguiu atender a uma solicitação válida.
    - 500 Internal Server Error
    - 502 Bad Gateway
    - 503 Service Unavailable

### HTTP Headers

Request/Response Headers (key: value):
- `Content-Type`: Indica o tipo de mídia do recurso sendo enviado para o servidor.
- `Host`: Especifica o nome de domínio do servidor e o número da porta TCP.

### Estrutura de Mensagem HTTP

**Request Message**:
- Linha de Solicitação: Método, URL e versão HTTP (e.g., GET /index.html HTTP/1.1).
- Headers: Pares de chave-valor que transmitem informações adicionais (e.g., Host: www.example.com).
- Body: Carga útil de dados opcional (e.g., form data in a POST request).

**Response Message**:
- Linha de Status: Versão HTTP, código de status e mensagem de status (e.g., HTTP/1.1 200 OK).
- Headers: Pares de chave-valor que transmitem informações adicionais (e.g., Content-Type: text/html).
- Body: Carga útil de dados opcional (e.g., HTML content of the web page).

## APIs RESTful

REST (Transferência de Estado Representacional) is an architectural style for designing networked applications. APIs RESTful use HTTP requests to perform CRUD (Create, Read, Update, Delete) operations.

### Exemplo de API de Funcionários

Here is an example of a set of API endpoints to handle employee-related operations. This API will cover basic CRUD functionalities and some additional endpoints for searching and filtering employees.


#### Criar um Novo Funcionário

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

**Description:** Recuperar uma lista de todos os funcionários.

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

**Description:** Recuperar detalhes de um único funcionário pelo seu ID.

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

**Description:** Atualizar os detalhes de um funcionário existente.

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

**Description:** Excluir um funcionário pelo seu ID.

**Response:**
```json
{
  "message": "Employee deleted successfully"
}
```

---

#### Search Employees by Name

**Endpoint:** `GET /api/employees/search`

**Description:** Procurar funcionários pelo nome.

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

**Description:** Filtrar funcionários por departamento.

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

### Visão Geral do Spring Framework

Spring facilita a criação de aplicações empresariais em Java. It has bibliotecas para ajudar no desenvolvimento de APIs (Spring MVC), comunicar-se com bancos de dados (Spring JPA), configurar (Spring Boot), entre várias outras funcionalidades.

**Exemplo Básico**

Here's a simple example to illustrate the basic usage of the Spring Framework (using Maven):

1. **Create a Aplicação Spring Boot:**

    **Estrutura do Projeto:**
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
    <dependências>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependências>
    ```

    **DemoApplication.java:**
    ```java
    package com.example.demo;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigurar.SpringBootApplication;

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

2. **Executar a Aplicação:**

    Use Maven to build and run the application:
    ```
    mvn spring-boot:run
    ```

3. **Testar a Aplicação:**

    Open the terminal and use the command:
    ```
    curl -X GET http://localhost:8080/greeting?name=Spring
    ```

    You should see the response:
    ```
    Hello, Spring
    ```

---

### Visão Geral do Maven

Maven é uma poderosa ferramenta de automação de build usada principalmente para projetos Java. It helps manage project dependências, build processes, and project lifecycles in a standardized and efficient way.

**Key Features**

- **Gerenciamento de Projetos:** Maven uses a standard project structure and conventions, making it easier to understand and maintain projects.
- **Gerenciamento de Dependências:** Automatically handles downloading and updating project dependências.
- **Automação de Build:** Automates compilation, testing, packaging, and deployment of projects.
- **Plugins:** Extensible via plugins for additional functionalities, such as generating reports, documentation, etc.
- **Builds Reproduzíveis:** Ensures consistent builds across different environments.

The `pom.xml` file is the heart of a Maven project. It contains project information, configuration details, dependências, plugins, and more.

---

### Visão Geral do cURL

cURL é uma ferramenta de linha de comando e biblioteca para transferir dados com URLs. É amplamente utilizado para interagir com servidores web, APIs e vários protocolos (HTTP, FTP, etc.).

**Exemplo de uso do cURL para acessar a API de Funcionários:**

1. **Criar um Novo Funcionário**

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