# Table of Contents:
- [1. Necessary dependencies](#Necessary-dependencies)
- [2. Parent pom](#Parent-pom)

## 1. Necessary dependencies
### 1.1. Foundation dependencies 
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <optional>true</optional>
</dependency>

<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-api</artifactId>
</dependency>

<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>

<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>

<dependency>
    <groupId>com.fasterxml.jackson.datatype</groupId>
    <artifactId>jackson-datatype-jsr310</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```
Explanation:
- spring-boot-starter-actuator:
  - Meaning: Monitor and manage application (health, metrics, beans, threads, etc.) 
  - Config: 
     - management.endpoints.web.exposure.include=health,metrics,info,bean,threadump
     - management.endpoint.health.show-details=always
  - Usage:
     - endpoint: http://localhost:8080/actuator

- spring-boot-starter-validation
  - Meaning: Validate request data using Jakarta Bean Validation
  - Common annotations:
     - @NotNull → field must not be null
     - @NotBlank → string must not be empty
     - @NotEmpty → collection/string must not be empty
     - @Size → limit size of string/collection
     - @Email → validate email format
     - @Pattern → regex validation
     - @Min / @Max → numeric range
     - @Positive / @Negative → number sign
     - @Past / @Future → date validation
  - Usage:
     - Validate request body (DTO)
     - Combine with @Valid in controller

- spring-boot-starter-web
  - Meaning: Build REST APIs and web applications (Spring MVC)
  - Main features:
     - REST controller support
     - JSON request/response handling
     - Embedded server (Tomcat)
     - HTTP request mapping
  - Common annotations:
     - @RestController → define REST API controller
     - @Controller → MVC controller
     - @RequestMapping → base URL mapping
     - @GetMapping → GET API
     - @PostMapping → POST API
     - @PutMapping → PUT API
     - @DeleteMapping → DELETE API
     - @RequestBody → bind request body
     - @PathVariable → get value from URL
     - @RequestParam → query parameters
  - Usage:
     - Build REST endpoints
     - Handle HTTP requests/responses
- lombok
  - Meaning: Reduce boilerplate code in Java classes
  - Common annotations:
     - @Getter / @Setter → generate getters/setters
     - @Data → includes getter, setter, toString, equals, hashCode
     - @Builder → builder pattern
     - @NoArgsConstructor → no-args constructor
     - @AllArgsConstructor → full constructor
     - @RequiredArgsConstructor → constructor for final fields
     - @ToString → generate toString()
     - @EqualsAndHashCode → generate equals & hashCode
  - Usage:
     - Simplify DTO, Entity, Model classes
- springdoc-openapi-starter-webmvc-api
  - Meaning: Generate OpenAPI specification (API documentation in JSON)
  - Common annotations:
     - @Operation → describe API endpoint
     - @Parameter → describe parameters
     - @Schema → model description
     - @Tag → group APIs
     - @Hidden → hide API from docs
  - Usage:
     - Endpoint: /v3/api-docs
- springdoc-openapi-starter-webmvc-ui
  - Meaning: Provide Swagger UI interface to visualize and test APIs
  - Usage:
    - Swagger UI: http://localhost:8080/swagger-ui.html
  - Features:
    - Interactive API testing
    - Auto-generated UI from OpenAPI spec
- spring-boot-starter-tomcat (provided)
  - Meaning: Embedded Tomcat server
  - Scope:
    - provided → external server will provide it (e.g., deploy WAR)
  - Usage:
    - Run Spring Boot app as web server
    - Optional when deploying to external Tomcat
- jackson-dataformat-xml
  - Meaning: Enable XML request/response support (besides JSON)
  - Usage:
    - Convert Java object ↔ XML
    - Support XML APIs
- jackson-datatype-jsr310 (combine with ObjectMapper to convert java time)
  - Meaning: Support Java 8+ Date/Time API (java.time)
  - Supported types:
    - LocalDate
    - LocalDateTime
    - ZonedDateTime
    - Instant
  - Usage:
    - Proper serialization/deserialization of date/time
- spring-boot-starter-test
  - Meaning: Testing framework for Spring Boot applications
  - Includes:
    - JUnit
    - Mockito
    - Spring Test
  - Common annotations:
    - @SpringBootTest → full application test
    - @WebMvcTest → controller test
    - @DataJpaTest → JPA test
    - @MockBean → mock dependency
    - @Autowired → inject bean in test
  - Usage:
    - Unit testing
    - Integration testing
- hibernate-validator
  - Meaning: Validate by Hibernate, has the same annotations with lombok dependency
  - Usage:
    - assign @NonNull, @Email (import from jakarta.validation, not from lombok) and call Validator.validate(object)
- 
### 1.2. Database dependencies (Ex: postgreSql)
```
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```
Explanation:
- postgresql
  - Meaning: PostgreSQL JDBC driver
  - Scope:
    - runtime → only needed at runtime
  - Usage:
    - Connect application to PostgreSQL database
- spring-boot-starter-data-jpa
  - Meaning: JPA + Hibernate for database access
  - Features:
    - ORM (Object Relational Mapping)
    - Repository abstraction
    - Query methods
  - Common annotations:
    - @Entity → map class to table
    - @Table → define table name
    - @Id → primary key
    - @GeneratedValue → auto-generate ID
    - @Column → map field to column
    - @Repository → DAO layer
    - @Transactional → transaction management
  - Usage:
    - Perform CRUD operations on database

### 1.3. Security (Ex: postgreSql)
```
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-core</artifactId>
    <version>10.1.40</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>6.1.14</version>
</dependency>
```
Explanation:
- tomcat-embed-core (10.1.40)
  - Meaning: Fix vulnerability CVE-2025-24813
- spring-core (6.1.14)
  - Meaning: Fix vulnerability CVE-2024-38820

## 2. Parent pom

```
<parent>
  <groupId></groupId>
  <artifactId></artifactId>
  <version></version>
  <relativePath/>
</parent>
<repositories>
  <repository>
    <id></id>
    <url></url>
    <releases></releases>
    <snapshots></snapshots>
  </repository>
</repositories>
<dependencies></dependencies>
```
~/.m2/settings.xml
```
<settings>
  <servers>
    <server>
      <id>my-repo</id>
      <username>my-username</username>
      <password>my-secret-password</password>
    </server>
  </servers>
</settings>
```
Explanation:
Maven first tries to resolve the parent POM using the relativePath (from the local workspace).
If it is not found, Maven then looks in the local repository (.m2).
If it is still not found, Maven will try to download it from remote repositories.

- Release tag: enables Maven to download release (stable) versions
- Snapshot tag: enables Maven to download snapshot versions
- Maven determines whether a version is a release or a snapshot based on the version naming
  - Stable version: 1.2.0
  - Snapshot version: 1.2.0-SNAPSHOT


