# a-z-skill

Please create a single, cohesive mini-project that meets these criteria:

* **Simple Domain & Schema**
  Use a minimal data model (for example, just two entities with 2–3 fields each). Keep database tables or collections tiny—no large schemas or complex joins.

* **Teaching Focus (Beginner → Advanced)**
  Write inline comments that explain each line for a newcomer (“What does this annotation do?”), include intermediate notes (“Why choose Redis for caching rather than a Java map?”), and add advanced insights (“How Spring’s auto-configuration wires beans under the hood,” or “Trade-offs when tuning a Cassandra partition key”). Ensure any developer, from novice to expert, can read the code and understand both the “how” and the “why.”

* **Documentation & Structure**
  Organize everything in a single codebase with clear packages or modules so each feature is easy to find. Include a `README.md` that describes the overall architecture and maps each demonstration to the relevant code section. Provide a `concepts.md` (or similar) that explains every major concept in plain English from basic to expert level.

* **Must Include These Demonstrations**

**Ticket and task Mapping**

* **Ticket 01 - Tasks 1–5** establish foundational Java, SQL, and database concepts.
* **Ticket 02 - Tasks 6–10** introduce Spring Boot, JPA/Hibernate, configuration, exception handling, and security.
* **Ticket 03 - Tasks 11–13** cover service discovery, API gateway, and observability basics (Actuator, metrics).
* **Ticket 04 - Tasks 14–16** delve deeper into Hibernate internals, Vert.x reactive programming, and resilience patterns.
* **Ticket 05 - Tasks 17–18** microservice communication patterns, and Kafka messaging.
* **Ticket 06 - Tasks 19–20** add alternative messaging systems (RabbitMQ, JMS).
* **Ticket 07 - Tasks 21–26** demonstrate database migrations, NoSQL integrations (MongoDB, Cassandra, Redis, DynamoDB), and AWS S3.
* **Ticket 08 - Tasks 27–28** cover containerization and CI/CD pipelines.
* **Ticket 09 - Tasks 29–30** round out logging and monitoring with centralized logging, Prometheus, Grafana, and distributed tracing.

 The project’s primary aim is to demo each feature, every task is framed around creating a clear, runnable demonstration with teaching notes. Here’s the  list with “Demo”-focused titles and descriptions
Here are the 1-30 Tasks

1. **Define Domain Model with Java OOP Principles**
   *Create `User` and `Task` classes using inheritance or interfaces (e.g., `BaseEntity`), and demonstrate polymorphism in a service method. Explain interfaces, abstract classes, and method overriding for beginners and note design choices for advanced readers.*

2. **Process Collections with Streams API and Lambdas**
   *Implement a method that processes a `List<Task>` to filter by status, map to DTOs using a `Function<Task, TaskDto>`, and validate with a `Predicate<Task>`. Include inline comments on stream stages, lambda syntax, and performance considerations.*

3. **Implement Concurrency with Executors and CompletableFuture**
   *Use `Executors.newFixedThreadPool` to run multiple asynchronous notification tasks, then combine results using `CompletableFuture`. Explain thread pools vs. raw threads, and discuss potential race conditions and tuning for high throughput.*

4. **Design SQL Schema and Write Optimized Queries**
   *Create simple `users(id, username, email)` and `tasks(task_id, title, status, user_id)` tables. Write a JOIN query with aggregation (e.g., count tasks per user), show its `EXPLAIN ANALYZE` plan, and add an index on `task.status` to improve performance. Comment on index trade-offs and query plans.*

5. **Add Stored Procedure, Trigger, and View**
   *Define a stored procedure that inserts a new `task`, a trigger that assigns a default status on insert, and a view that joins `users` and `tasks` for reporting. Explain PL/SQL basics for beginners and versioning/migration considerations for advanced users.*

6. **Set Up Spring Boot and Create REST Endpoint with Dependency Injection**
   *Initialize a Spring Boot project, build a `UserController` annotated with `@RestController`, and inject a `UserService` via constructor. Expose `GET /users` and `POST /users`. Clarify what `@RestController`, `@Autowired`, and constructor injection do, and discuss best practices.*

7. **Integrate Spring Data JPA/Hibernate with Entity Relationships and Caching**
   *Define a `User` entity (`@Entity`, `@Table`) with a `@OneToMany(mappedBy="user")` relationship to `Task`. Create a `UserRepository extends JpaRepository`. Demonstrate lazy vs. eager loading in a test and configure EHCache for second-level caching. Explain session management and cache invalidation.*

8. **Implement Configuration Properties with `@ConfigurationProperties`**
   *Create a POJO annotated with `@ConfigurationProperties(prefix="app.settings")` to load custom settings (e.g., cache TTL) from `application.yml`. Show how Spring Boot binds externalized config, and discuss profiles and environment-specific overrides.*

9. **Create Global Exception Handling via `@ControllerAdvice`**
   *Write a `@ControllerAdvice` class with an `@ExceptionHandler(EntityNotFoundException.class)` method that returns a custom JSON error response. Explain how exception resolution works in Spring MVC and best practices for error payloads.*

10. **Configure Spring Security with JWT/OAuth 2.0 and Protect Endpoints**
    *Implement a `/auth/login` endpoint that validates credentials and issues a signed JWT. Add a `OncePerRequestFilter` to validate incoming JWTs and set `SecurityContextHolder`. Protect `/tasks` with `@PreAuthorize("hasRole('USER')")`. Explain token structure, roles vs. authorities, and advanced token revocation considerations.*

11. **Set Up Service Discovery with Eureka/Consul and Load-Balanced RestTemplate**
    *Configure Eureka (or Consul) server and have `UserService` and `TaskService` register. In `TaskService`, use `@LoadBalanced RestTemplate` (or `WebClient`) to call `http://USER-SERVICE/users/{id}`. Explain client-side vs. server-side load balancing and heartbeats.*

12. **Configure Spring Cloud Gateway with Routing and Filters**
    *Create a gateway application that routes `GET /api/users/**` to `UserService` and `GET /api/tasks/**` to `TaskService`. Add a pre-filter to log requests and a post-filter to add a custom header (e.g., `X-Gateway: active`). Explain filter order and reactive vs. servlet-based routing.*

13. **Add Spring Boot Actuator and Custom Metrics with Prometheus and Grafana**
    *Expose `/actuator/health` and `/actuator/metrics`. Create a custom `Counter` (e.g., `taskCreationCounter`) and increment it whenever a new task is created. Provide a `prometheus.yml` scrape config for `/actuator/prometheus` and include a Grafana dashboard JSON that plots task creation rate. Explain metric naming conventions and dashboard design.*

14. **Demonstrate Hibernate Session and EntityManager Lifecycle**
    *Write a service method that manually begins and commits a transaction (`entityManager.getTransaction().begin()`). Show lazy vs. eager loading in a unit test and explain `LazyInitializationException` when accessing a collection outside a transaction. Discuss second-level cache and session flush modes.*

15. **Integrate Vert.x Verticle and Reactive HTTP Endpoint**
    *Develop a Vert.x `Verticle` that listens on the Vert.x `EventBus` address `"task.process"` and performs a nonblocking computation (e.g., simulating I/O). Expose a Spring Boot endpoint `/vertx/processTask` that publishes a message to `"task.process"` and returns a `Future` result. Explain event-loop vs. blocking operations and thread confinement.*

16. **Apply Resilience4j Circuit Breaker and Retry Mechanisms**
    *Wrap an external REST call (e.g., `http://external-service/api/data`) with `@CircuitBreaker(name="externalService", fallbackMethod="fallbackHandler")` and `@Retry(name="externalServiceRetry", maxAttempts=3)`. Implement a fallback method that returns a default response. Discuss circuit breaker metrics, thread isolation, and fallback strategies.*

17. **Implement Microservices Communication via REST and Kafka Messaging**
    *Have `TaskService` call `UserService` via REST to validate `userId` before creating a task. Also, publish a `TaskCreatedEvent` to Kafka. Create a `NotificationService` microservice (in the same repo) that consumes `TaskCreatedEvent` and logs a notification. Explain synchronous vs. asynchronous communication patterns and event-driven design.*

18. **Configure Kafka Producer and Consumer with Event Schema and Partitioning**
    *Set up a Kafka producer bean in Spring Boot to send a JSON `TaskCreatedEvent` to topic `task-events`. Create a `@KafkaListener(topics="task-events", groupId="notificationGroup")` to process events. Define and register a JSON serializer/deserializer. Explain topic partitioning (e.g., `userId % numPartitions`), consumer group rebalancing, and offset management.*

19. **Add RabbitMQ Messaging with Queue, Exchange, and Listener**
    *Configure a `DirectExchange` bean named `taskExchange`, a `Queue` bean named `taskQueue`, and bind them with routing key `task.create`. In `TaskService`, publish a `CreateTaskMessage` to `taskExchange` with `task.create`. Implement a `@RabbitListener(queues="taskQueue")` that consumes and logs messages. Explain queue durability, acknowledgments, prefetch count, and QoS.*

20. **Add ActiveMQ / JMS Integration with JmsTemplate and Listener**
    *Configure `ActiveMQConnectionFactory` to connect to `tcp://localhost:61616` and define a `JmsTemplate` bean. Send a `TextMessage` to queue `auditQueue` via `jmsTemplate.convertAndSend("auditQueue", "Task created: " + taskId)`. Create a `@JmsListener(destination="auditQueue")` to receive messages and log them. Discuss durable vs. non-durable subscriptions and message selectors.*

21. **Set Up Database Migrations with Flyway or Liquibase**
    *Create migration scripts to define `users(id PK, username, email)` and `tasks(task_id PK, title, status, user_id FK)`. Configure Flyway (or Liquibase) in `application.yml` so migrations run on startup. Explain version control for database schema and rollback strategies.*

22. **Integrate MongoDB Document Save and Read**
    *Configure a `MongoTemplate` or `MongoRepository<LogEntry, String>` for a `logs` collection. Insert a document `{timestamp, level, message}` when a task is created, then query the latest 10 logs. Explain document modeling vs. relational tables and indexing strategies.*

23. **Integrate Cassandra Wide-Column Modeling Example**
    *Provide CQL to create a keyspace `app` and table `metrics(user_id UUID, metric_name text, metric_value double, PRIMARY KEY (user_id, metric_name))`. Use the DataStax Java driver to insert and query metrics in a service. Explain partition keys, clustering keys, denormalization trade-offs, and eventual consistency.*

24. **Configure Redis Cache and Caffeine In-Memory Cache**
    *Set up a `RedisCacheManager` bean, annotate `findUserById(Long id)` with `@Cacheable(cacheNames="users", key="#id")`, and demonstrate repeated calls hitting Redis. In `TaskService`, configure a Caffeine cache for `findAllTasksByUserId(Long userId)` with a 30-second TTL. Explain cache-aside vs. read-through and cache invalidation strategies.*

25. **Integrate DynamoDB for NoSQL Data Storage**
    *Configure AWS SDK to connect to a local DynamoDB instance (Docker) or AWS. Create a table `Notifications` with `notificationId` as the primary key and `userId` as a Global Secondary Index. Write methods that put a `Notification` item and query by `userId`. Discuss read/write capacity units, partition design, and cost trade-offs.*

26. **Implement AWS S3 File Storage Integration**
    *Use `AmazonS3Client` to upload a small JSON or text file (e.g., a task log) to an S3 bucket named `my-app-logs`. Show how to retrieve that object by key. Explain AWS credential configuration (IAM roles vs. environment variables), region setup, and bucket policies.*

27. **Create Dockerfile and Docker-Compose for Containerization**
    *Provide a multi-stage `Dockerfile` that uses `maven:3.6-jdk-11` to build a fat JAR, then copies it into `openjdk:11-jre-slim`. Write a `docker-compose.yml` that brings up PostgreSQL, Redis, Kafka, Zookeeper, MongoDB, Cassandra, and all microservices. Explain multi-stage builds, service dependencies, and network configuration.*

28. **Define CI/CD Pipeline with Jenkinsfile or GitHub Actions**
    \*Write a `Jenkinsfile` (or `.github/workflows/ci.yml`) that:

    1. Checks out code.
    2. Runs `mvn clean test` (or `gradle test`).
    3. Builds the Docker image and tags it with `${GIT_COMMIT}`.
    4. Pushes the image to Docker Hub (or AWS ECR).
    5. Deploys to a staging environment (e.g., via `docker-compose -f docker-compose.prod.yml up -d`).
    6. Includes a rollback stage that redeploys the previous Docker tag on failure.
       Explain pipeline stages, artifact versioning, and environment promotion.\*

29. **Configure Centralized Logging with JSON Formatter for ELK/CloudWatch**
    *Set up Logback (or Log4j2) with a JSON encoder so every log line includes `timestamp`, `level`, `serviceName`, and optional `traceId`. Provide a snippet to send logs to a local file for Logstash ingestion or directly to CloudWatch Logs. Explain how to define index patterns in Kibana and use Grafana to query log-based metrics.*

30. **Add Metrics & Tracing with Prometheus, Zipkin, and Grafana**
    *Register a `Timer` metric (e.g., `taskProcessingDuration`) and a `Gauge` metric (e.g., `activeUserCount`) using Micrometer. Configure Prometheus to scrape `/actuator/prometheus`, and include a Grafana dashboard JSON that visualizes HTTP request latency, task processing durations, and error rates. Integrate Spring Sleuth and Zipkin, annotate service methods with `@NewSpan`, and explain how to view distributed traces in Zipkin UI.*

---


