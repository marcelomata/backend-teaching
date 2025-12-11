# Tutorial de Desenvolvimento de Aplicações Web e APIs

## Índice

1. [Rede de Computadores](#rede-de-computadores)
2. [Internet](#internet)
3. [HTTP/HTTPS](#httphttps)
    - [Métodos HTTP](#métodos-http)
    - [Códigos de Status HTTP](#códigos-de-status-http)
    - [Cabeçalhos HTTP](#cabeçalhos-http)
    - [Estrutura de Mensagem HTTP](#estrutura-de-mensagem-http)
4. [APIs RESTful](#apis-restful)
    - [Exemplo de API de Funcionários](#exemplo-de-api-de-funcionários)
5. [Visão Geral do Spring Framework](#visão-geral-do-spring-framework)
    - [Exemplo Básico](#exemplo-básico)
6. [Visão Geral do Maven](#visão-geral-do-maven)
7. [Visão Geral do cURL](#visão-geral-do-curl)
    - [Exemplos de Comandos cURL](#exemplos-de-comandos-curl)
8. [Construindo a API de Funcionários com Spring](#construindo-a-api-de-funcionários-com-spring)
    - [Spring Controllers](#spring-controllers)
    - [A Classe Entity](#a-classe-entity)
    - [Spring Services](#spring-services)
    - [Armazenando Dados em Memória](#armazenando-dados-em-memória)
    - [Testando com cURL](#testando-com-curl)
9. [Introdução a Containers e Docker](#introdução-a-containers-e-docker)
    - [O que é um Container?](#o-que-é-um-container)
    - [O que é Docker?](#o-que-é-docker)
    - [Comandos Básicos do Docker](#comandos-básicos-do-docker)
10. [Introdução a Bancos de Dados](#introdução-a-bancos-de-dados)
    - [O que é MySQL?](#o-que-é-mysql)
    - [Executando MySQL em um Container Docker](#executando-mysql-em-um-container-docker)
11. [Integrando Spring com MySQL](#integrando-spring-com-mysql)
    - [Adicionando Dependências do Banco de Dados](#adicionando-dependências-do-banco-de-dados)
    - [Configurando a Conexão com o Banco de Dados](#configurando-a-conexão-com-o-banco-de-dados)
    - [Spring Repositories](#spring-repositories)
    - [Atualizando a Entity para JPA](#atualizando-a-entity-para-jpa)
    - [Atualizando o Service para Usar o Repository](#atualizando-o-service-para-usar-o-repository)
12. [Testando a Aplicação Completa](#testando-a-aplicação-completa)
13. [Exercícios para o Leitor](#exercícios-para-o-leitor)
14. [Conclusão](#conclusão)

## Rede de Computadores

Uma rede de computadores é uma coleção de dispositivos interconectados (como computadores, servidores, smartphones e outros hardwares) que se comunicam entre si para compartilhar recursos e informações. Esses dispositivos são conectados através de vários tipos de meios de comunicação, incluindo conexões com fio (como cabos Ethernet) e conexões sem fio (como Wi-Fi).

## Internet

A internet é uma vasta rede global de redes de computadores interconectadas que se comunicam entre si usando protocolos padronizados. Ela permite a troca de dados e recursos entre bilhões de dispositivos em todo o mundo, incluindo computadores, servidores, smartphones e outros dispositivos conectados.

## HTTP/HTTPS

### Métodos HTTP

- **GET**: Recuperar dados do servidor. Usado para leitura de recursos.
- **POST**: Enviar dados para o servidor para criar um novo recurso.
- **PUT**: Atualizar um recurso existente com novos dados.
- **PATCH**: Aplicar modificações parciais a um recurso.
- **DELETE**: Remover um recurso do servidor.
- **HEAD**: Recuperar cabeçalhos de um recurso, similar ao GET mas sem o corpo da resposta.
- **OPTIONS**: Descrever as opções de comunicação para o recurso alvo.
- **TRACE**: Executar um teste de loop-back de mensagem ao longo do caminho para o recurso alvo.

### Códigos de Status HTTP

- **1xx (Informacional)**: Solicitação recebida, continuando o processo.
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

### Cabeçalhos HTTP

Cabeçalhos de Requisição/Resposta (chave: valor):
- `Content-Type`: Indica o tipo de mídia do recurso sendo enviado para o servidor.
- `Host`: Especifica o nome de domínio do servidor e o número da porta TCP.

### Estrutura de Mensagem HTTP

**Mensagem de Requisição**:
- Linha de Solicitação: Método, URL e versão HTTP (ex.: GET /index.html HTTP/1.1).
- Headers: Pares de chave-valor que transmitem informações adicionais (ex.: Host: www.example.com).
- Body: Carga útil de dados opcional (ex.: dados de formulário em uma requisição POST).

**Mensagem de Resposta**:
- Linha de Status: Versão HTTP, código de status e mensagem de status (ex.: HTTP/1.1 200 OK).
- Headers: Pares de chave-valor que transmitem informações adicionais (ex.: Content-Type: text/html).
- Body: Carga útil de dados opcional (ex.: conteúdo HTML da página web).

## APIs RESTful

REST (Transferência de Estado Representacional) é um estilo arquitetural para projetar aplicações em rede. APIs RESTful usam requisições HTTP para realizar operações CRUD (Create, Read, Update, Delete - Criar, Ler, Atualizar, Excluir).

### Exemplo de API de Funcionários

Aqui está um exemplo de um conjunto de endpoints de API para lidar com operações relacionadas a funcionários. Esta API cobrirá funcionalidades básicas de CRUD e alguns endpoints adicionais para pesquisa e filtragem de funcionários.


#### Criar um Novo Funcionário

**Endpoint:** `POST /api/employees`

**Descrição:** Criar um novo funcionário.

**Corpo da Requisição:**
```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "position": "Software Engineer",
  "salary": 60000,
  "department": "Engineering"
}
```

**Resposta:**
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

#### Obter Todos os Funcionários

**Endpoint:** `GET /api/employees`

**Descrição:** Recuperar uma lista de todos os funcionários.

**Resposta:**
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

#### Obter um Funcionário por ID

**Endpoint:** `GET /api/employees/{id}`

**Descrição:** Recuperar detalhes de um único funcionário pelo seu ID.

**Resposta:**
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

#### Atualizar um Funcionário

**Endpoint:** `PUT /api/employees/{id}`

**Descrição:** Atualizar os detalhes de um funcionário existente.

**Corpo da Requisição:**
```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "position": "Senior Software Engineer",
  "salary": 70000,
  "department": "Engineering"
}
```

**Resposta:**
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

#### Excluir um Funcionário

**Endpoint:** `DELETE /api/employees/{id}`

**Descrição:** Excluir um funcionário pelo seu ID.

**Resposta:**
```json
{
  "message": "Employee deleted successfully"
}
```

---

#### Pesquisar Funcionários por Nome

**Endpoint:** `GET /api/employees/search`

**Descrição:** Procurar funcionários pelo nome.

**Parâmetros de Consulta:** `name`

**Exemplo:** `GET /api/employees/search?name=John`

**Resposta:**
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

#### Filtrar Funcionários por Departamento

**Endpoint:** `GET /api/employees/filter`

**Descrição:** Filtrar funcionários por departamento.

**Parâmetros de Consulta:** `department`

**Exemplo:** `GET /api/employees/filter?department=Engineering`

**Resposta:**
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

Esta estrutura fornece um conjunto abrangente de endpoints para gerenciar dados de funcionários, seguindo os princípios RESTful, e cobre operações comuns necessárias em um sistema backend.

---

### Visão Geral do Spring Framework

Spring facilita a criação de aplicações empresariais em Java. Ele possui bibliotecas para ajudar no desenvolvimento de APIs (Spring MVC), comunicar-se com bancos de dados (Spring JPA), configurar (Spring Boot), entre várias outras funcionalidades.

**Exemplo Básico**

Aqui está um exemplo simples para ilustrar o uso básico do Spring Framework (usando Maven):

1. **Criar uma Aplicação Spring Boot:**

    **Estrutura do Projeto:**
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

2. **Executar a Aplicação:**

    Use o Maven para compilar e executar a aplicação:
    ```
    mvn spring-boot:run
    ```

3. **Testar a Aplicação:**

    Abra o terminal e use o comando:
    ```
    curl -X GET http://localhost:8080/greeting?name=Spring
    ```

    Você deverá ver a resposta:
    ```
    Hello, Spring
    ```

---

### Visão Geral do Maven

Maven é uma poderosa ferramenta de automação de build usada principalmente para projetos Java. Ela ajuda a gerenciar dependências do projeto, processos de build e ciclos de vida do projeto de forma padronizada e eficiente.

**Principais Recursos**

- **Gerenciamento de Projetos:** O Maven usa uma estrutura de projeto padrão e convenções, tornando mais fácil entender e manter projetos.
- **Gerenciamento de Dependências:** Lida automaticamente com o download e atualização das dependências do projeto.
- **Automação de Build:** Automatiza compilação, testes, empacotamento e implantação de projetos.
- **Plugins:** Extensível via plugins para funcionalidades adicionais, como geração de relatórios, documentação, etc.
- **Builds Reproduzíveis:** Garante builds consistentes em diferentes ambientes.

O arquivo `pom.xml` é o coração de um projeto Maven. Ele contém informações do projeto, detalhes de configuração, dependências, plugins e mais.

---

### Visão Geral do cURL

cURL é uma ferramenta de linha de comando e biblioteca para transferir dados com URLs. É amplamente utilizado para interagir com servidores web, APIs e vários protocolos (HTTP, FTP, etc.).

**Exemplo de uso do cURL para acessar a API de Funcionários:**

1. **Criar um Novo Funcionário**

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

2. **Obter Todos os Funcionários**

    **Endpoint:** `GET /api/employees`
    ```
    curl -X GET http://localhost:8080/api/employees
    ```

3. **Obter um Funcionário por ID**

    **Endpoint:** `GET /api/employees/{id}`
    ```
    curl -X GET http://localhost:8080/api/employees/1
    ```

4. **Atualizar um Funcionário**

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

5. **Excluir um Funcionário**

    **Endpoint:** `DELETE /api/employees/{id}`
    ```
    curl -X DELETE http://localhost:8080/api/employees/1
    ```

6. **Pesquisar Funcionários por Nome**

    **Endpoint:** `GET /api/employees/search`
    ```
    curl -X GET "http://localhost:8080/api/employees/search?name=John"
    ```

7. **Filtrar Funcionários por Departamento**

    **Endpoint:** `GET /api/employees/filter`
    ```
    curl -X GET "http://localhost:8080/api/employees/filter?department=Engineering"
    ```

---

## Construindo a API de Funcionários com Spring

Agora vamos construir uma implementação real da API de Funcionários usando Spring Boot. Começaremos de forma simples armazenando dados em memória, e depois conectaremos a um banco de dados real.

### Spring Controllers

Um **Controller** no Spring é uma classe que lida com requisições HTTP. Ele recebe requisições dos clientes, as processa (geralmente chamando um service) e retorna uma resposta.

Anotações principais:
- `@RestController`: Marca a classe como um controller REST que retorna dados (JSON) em vez de views (HTML).
- `@RequestMapping`: Define o caminho base da URL para todos os endpoints no controller.
- `@GetMapping`, `@PostMapping`: Mapeiam métodos HTTP específicos para métodos handler.
- `@RequestBody`: Converte o corpo da requisição JSON em um objeto Java.

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

O controller delega a lógica de negócio para a camada de **Service**. Essa separação mantém o código organizado e mais fácil de manter.

---

### A Classe Entity

Uma **Entity** representa o modelo de dados da sua aplicação. Ela define a estrutura dos dados que serão armazenados e transferidos.

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

    // Construtor padrão
    public Employee() {}

    // Construtor com parâmetros
    public Employee(Long id, String name, String email, String position, Double salary, String department) {
        this.id = id;
        this.name = name;
        this.email = email;
        this.position = position;
        this.salary = salary;
        this.department = department;
    }

    // Getters e Setters
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

Um **Service** no Spring contém a lógica de negócio da sua aplicação. Ele processa dados, aplica regras e coordena operações entre o controller e o armazenamento de dados.

Anotações principais:
- `@Service`: Marca a classe como um componente service, permitindo que o Spring a gerencie automaticamente.

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

### Armazenando Dados em Memória

No service acima, usamos um `ArrayList` para armazenar funcionários em memória. Esta é uma abordagem simples para aprendizado e testes, mas tem limitações:

- **Dados são perdidos** quando a aplicação reinicia
- **Não é adequado para produção** - aplicações reais precisam de armazenamento persistente
- **Sem tratamento de acesso concorrente** - múltiplas requisições podem causar problemas

Esta abordagem é útil para:
- Aprendizado e prototipagem
- Testes unitários
- Demos simples

**Estrutura do Projeto:**
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

### Testando com cURL

Execute a aplicação:
```bash
mvn spring-boot:run
```

Teste criando um funcionário:
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

Resposta esperada:
```json
{"id":1,"name":"John Doe","email":"john@example.com","position":"Developer","salary":60000.0,"department":"Engineering"}
```

Teste obtendo todos os funcionários:
```bash
curl -X GET http://localhost:8080/api/employees
```

---

## Introdução a Containers e Docker

### O que é um Container?

Um **container** é um pacote leve e independente que contém tudo necessário para executar um software:
- O código da aplicação
- Ambiente de execução
- Bibliotecas e dependências
- Arquivos de configuração

**Benefícios dos containers:**
- **Consistência**: Funciona da mesma forma em qualquer máquina (seu laptop, servidor, nuvem)
- **Isolamento**: Cada container executa independentemente, evitando conflitos
- **Portabilidade**: Fácil de mover entre ambientes
- **Eficiência**: Mais leve que máquinas virtuais, inicia em segundos

Pense em um container como um container de transporte: ele empacota tudo junto para que possa ser transportado para qualquer lugar sem se preocupar com o que está dentro.

---

### O que é Docker?

**Docker** é a plataforma mais popular para criar e executar containers. Ele fornece:
- **Docker Engine**: Executa containers na sua máquina
- **Docker Hub**: Um registro para compartilhar e baixar imagens de containers
- **Docker Compose**: Ferramenta para executar múltiplos containers juntos

**Conceitos principais:**
- **Imagem**: Um template com instruções para criar um container (como uma receita)
- **Container**: Uma instância em execução de uma imagem (como um prato feito da receita)
- **Dockerfile**: Um arquivo de texto com instruções para construir uma imagem

---

### Comandos Básicos do Docker

```bash
# Verificar versão do Docker
docker --version

# Listar containers em execução
docker ps

# Listar todos os containers (incluindo parados)
docker ps -a

# Baixar uma imagem do Docker Hub
docker pull mysql:8.0

# Executar um container
docker run -d --name meu-container nome-da-imagem

# Parar um container
docker stop nome-do-container

# Iniciar um container parado
docker start nome-do-container

# Remover um container
docker rm nome-do-container

# Ver logs do container
docker logs nome-do-container
```

---

## Introdução a Bancos de Dados

### O que é MySQL?

**MySQL** é um dos bancos de dados relacionais mais populares do mundo. Um **banco de dados relacional** armazena dados em tabelas com linhas e colunas, similar a uma planilha.

**Conceitos principais:**
- **Tabela**: Armazena dados sobre um tipo de entidade (ex.: funcionários)
- **Linha**: Um único registro (ex.: um funcionário)
- **Coluna**: Um atributo específico (ex.: nome, email, salário)
- **Chave Primária**: Identificador único para cada linha (ex.: ID do funcionário)
- **SQL**: Linguagem usada para consultar e manipular dados

**Exemplo de uma tabela de funcionários:**

| id | name      | email              | position  | salary |
|----|-----------|--------------------|-----------|--------|
| 1  | John Doe  | john@example.com   | Developer | 60000  |
| 2  | Jane Smith| jane@example.com   | Manager   | 80000  |

---

### Executando MySQL em um Container Docker

Ao invés de instalar o MySQL diretamente no seu computador, podemos executá-lo em um container Docker. Isso é mais limpo e fácil de gerenciar.

**1. Baixar a imagem do MySQL:**
```bash
docker pull mysql:8.0
```

**2. Executar o container MySQL:**
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

**Explicação do comando:**
- `-d`: Executar em segundo plano (modo detached)
- `--name mysql-container`: Nomear o container
- `-e MYSQL_ROOT_PASSWORD`: Definir a senha do root
- `-e MYSQL_DATABASE`: Criar um banco de dados na inicialização
- `-e MYSQL_USER`: Criar um usuário
- `-e MYSQL_PASSWORD`: Definir a senha do usuário
- `-p 3306:3306`: Mapear a porta 3306 do container para sua máquina

**3. Verificar se está executando:**
```bash
docker ps
```

**4. Conectar ao MySQL (opcional, para testes):**
```bash
docker exec -it mysql-container mysql -u appuser -p
```
Digite a senha `apppassword` quando solicitado.

---

## Integrando Spring com MySQL

Agora vamos conectar nossa aplicação Spring ao banco de dados MySQL executando no Docker.

### Adicionando Dependências do Banco de Dados

Adicione estas dependências ao seu `pom.xml`:

```xml
<dependencies>
    <!-- Dependência existente -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
    <!-- JPA para acesso ao banco de dados -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    
    <!-- Driver MySQL -->
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <scope>runtime</scope>
    </dependency>
    
    <!-- Dependência de teste -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

### Configurando a Conexão com o Banco de Dados

Atualize o `application.properties` para conectar ao MySQL:

```properties
# Conexão com o banco de dados
spring.datasource.url=jdbc:mysql://localhost:3306/employeedb
spring.datasource.username=appuser
spring.datasource.password=apppassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# Configurações JPA/Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

**Explicação:**
- `spring.datasource.url`: URL de conexão com o banco de dados
- `spring.jpa.hibernate.ddl-auto=update`: Cria/atualiza tabelas automaticamente baseado nas entities
- `spring.jpa.show-sql=true`: Mostra as queries SQL no console (útil para aprendizado)

---

### Spring Repositories

Um **Repository** no Spring é uma interface que fornece métodos para interagir com o banco de dados. O Spring Data JPA implementa automaticamente operações comuns como save, find, delete.

Anotações principais:
- `@Repository`: Marca a interface como um componente repository
- Extende `JpaRepository<Entity, TipoId>`: Fornece métodos CRUD integrados

**EmployeeRepository.java:**
```java
package com.employeeservice.repository;

import com.employeeservice.model.Employee;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    // JpaRepository fornece estes métodos automaticamente:
    // - save(Employee) - Criar ou atualizar
    // - findById(Long) - Buscar por ID
    // - findAll() - Obter todos os registros
    // - deleteById(Long) - Excluir por ID
    // - count() - Contar registros
}
```

É isso! Nenhuma implementação necessária. O Spring gera o código automaticamente.

---

### Atualizando a Entity para JPA

Para trabalhar com o banco de dados, precisamos adicionar anotações JPA à nossa entity:

**Employee.java (atualizado):**
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

    // Construtor padrão (obrigatório pelo JPA)
    public Employee() {}

    // Construtor com parâmetros
    public Employee(String name, String email, String position, Double salary, String department) {
        this.name = name;
        this.email = email;
        this.position = position;
        this.salary = salary;
        this.department = department;
    }

    // Getters e Setters (mesmos de antes)
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

**Novas anotações explicadas:**
- `@Entity`: Marca esta classe como uma entidade do banco de dados
- `@Table(name = "employees")`: Especifica o nome da tabela
- `@Id`: Marca a chave primária
- `@GeneratedValue(strategy = GenerationType.IDENTITY)`: Gera IDs automaticamente
- `@Column`: Configura propriedades da coluna (nullable, unique, etc.)

---

### Atualizando o Service para Usar o Repository

Agora substituímos a lista em memória pelo repository:

**EmployeeService.java (atualizado):**
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

**O que mudou:**
- Removido o `ArrayList` e o contador `nextId`
- Adicionado `@Autowired EmployeeRepository` - Spring injeta o repository automaticamente
- Usado `employeeRepository.save()` ao invés de `employees.add()`
- Usado `employeeRepository.findAll()` ao invés de retornar a lista

**Estrutura do Projeto Atualizada:**
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

## Testando a Aplicação Completa

Agora vamos testar a aplicação completa com o banco de dados.

**1. Certifique-se de que o MySQL está executando:**
```bash
docker ps
# Se não estiver executando:
docker start mysql-container
```

**2. Inicie a aplicação Spring:**
```bash
mvn spring-boot:run
```

Você deve ver no console que o Hibernate cria a tabela `employees` automaticamente.

**3. Teste criando funcionários:**
```bash
# Criar primeiro funcionário
curl -X POST http://localhost:8080/api/employees \
     -H "Content-Type: application/json" \
     -d '{
           "name": "John Doe",
           "email": "john@example.com",
           "position": "Developer",
           "salary": 60000,
           "department": "Engineering"
         }'

# Criar segundo funcionário
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

**4. Teste obtendo todos os funcionários:**
```bash
curl -X GET http://localhost:8080/api/employees
```

Resposta esperada:
```json
[
  {"id":1,"name":"John Doe","email":"john@example.com","position":"Developer","salary":60000.0,"department":"Engineering"},
  {"id":2,"name":"Jane Smith","email":"jane@example.com","position":"Manager","salary":80000.0,"department":"Product"}
]
```

**5. Verifique a persistência dos dados:**

Pare a aplicação (Ctrl+C), depois inicie novamente:
```bash
mvn spring-boot:run
```

Verifique os funcionários:
```bash
curl -X GET http://localhost:8080/api/employees
```

Os dados ainda estão lá! Diferente da versão em memória, os dados persistem porque estão armazenados no MySQL.

---

## Exercícios para o Leitor

Agora que você tem uma API funcionando com os endpoints de Criar e Obter Todos, tente implementar os endpoints restantes por conta própria:

1. **Obter Funcionário por ID** (`GET /api/employees/{id}`)
   - Adicione um método no Controller usando `@GetMapping("/{id}")`
   - Use `@PathVariable` para obter o ID da URL
   - Adicione um método no Service usando `employeeRepository.findById()`

2. **Atualizar Funcionário** (`PUT /api/employees/{id}`)
   - Adicione um método no Controller usando `@PutMapping("/{id}")`
   - Encontre o funcionário, atualize os campos e salve de volta

3. **Excluir Funcionário** (`DELETE /api/employees/{id}`)
   - Adicione um método no Controller usando `@DeleteMapping("/{id}")`
   - Use `employeeRepository.deleteById()` no Service

4. **Pesquisar por Nome** (`GET /api/employees/search?name=John`)
   - Use `@RequestParam` para obter o parâmetro da query
   - Crie um método de query personalizado no Repository

5. **Filtrar por Departamento** (`GET /api/employees/filter?department=Engineering`)
   - Similar à pesquisa, mas filtre por departamento

**Dica:** O `JpaRepository` fornece muitos métodos úteis. Você também pode definir queries personalizadas seguindo as convenções de nomenclatura do Spring Data JPA (ex.: `findByName`, `findByDepartment`).

---

## Conclusão

Neste tutorial, você aprendeu:

1. **Fundamentos de Redes**: Como redes de computadores e a internet funcionam
2. **Protocolo HTTP**: Métodos, códigos de status, cabeçalhos e estrutura de mensagens
3. **APIs RESTful**: Projetando endpoints seguindo princípios REST
4. **Spring Framework**: Construindo aplicações web com Java
5. **Maven**: Gerenciando dependências e construindo projetos
6. **cURL**: Testando APIs pela linha de comando
7. **Spring Controllers**: Lidando com requisições HTTP
8. **Spring Services**: Implementando lógica de negócio
9. **Containers e Docker**: Executando aplicações em ambientes isolados
10. **Banco de Dados MySQL**: Armazenando dados de forma persistente
11. **Spring Repositories**: Interagindo com bancos de dados usando JPA

**Resumo da Arquitetura:**

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Cliente   │────▶│ Controller  │────▶│   Service   │────▶│ Repository  │
│   (cURL)    │◀────│             │◀────│             │◀────│             │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
                                                                   │
                                                                   ▼
                                                            ┌─────────────┐
                                                            │   MySQL     │
                                                            │  (Docker)   │
                                                            └─────────────┘
```

**Próximos Passos:**
- Adicionar endpoints de atualização (PUT) e exclusão (DELETE)
- Implementar validação de entrada
- Adicionar tratamento de erros
- Aprender sobre segurança com Spring Security
- Explorar Docker Compose para executar múltiplos containers

Bom código!