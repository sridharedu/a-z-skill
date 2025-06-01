Below is the requested breakdown, adding one more level of detail (Level 3) under each Level 2 category. Use this to organize topics hierarchically:

---

**1. Programming Languages & Core APIs**

* **1.1 Java Versions & Language Features**

  * *Java 8*

    * Streams API introduction
    * Lambda syntax and functional interfaces (`Function`, `Predicate`)
    * Default and static methods in interfaces
    * `Optional` usage and best practices
  * *Java 11*

    * Local‐variable type inference (`var`)
    * New `String` methods (`isBlank()`, `lines()`, `strip()`)
    * HTTP Client (`HttpClient`) enhancements
    * Running single‐file programs (`java Foo.java`)
  * *Java 17*

    * Records (compact data carrier classes)
    * Sealed classes for restricted hierarchies
    * Pattern‐matching for `switch` expressions
    * Text blocks (multiline string literals)

* **1.2 Object-Oriented Design**

  * *Encapsulation*

    * Access modifiers (`private`, `protected`, `public`)
    * Getters/setters vs. direct field access
    * Immutability patterns (making fields `final`)
  * *Abstraction*

    * Abstract classes vs. interfaces
    * Designing interface contracts (method signatures)
    * Hiding implementation details
  * *Inheritance*

    * `extends` keyword usage
    * `super` to call parent constructors or methods
    * Method overriding rules
  * *Polymorphism*

    * Runtime polymorphism via overridden methods
    * Compile‐time polymorphism with method overloading
    * Liskov Substitution Principle considerations
  * *SOLID Principles*

    * Single Responsibility Principle (one class, one purpose)
    * Open/Closed Principle (extend behavior without modifying existing code)
    * Liskov Substitution Principle (subtypes must be substitutable)
    * Interface Segregation Principle (many specific interfaces rather than one general)
    * Dependency Inversion Principle (depend on abstractions, not concretions)

* **1.3 Streams API & Lambda Expressions**

  * *Stream Creation*

    * From Collections (`list.stream()`)
    * From Arrays (`Arrays.stream(arr)`)
    * From files (`Files.lines(Path)`)
  * *Intermediate Operations*

    * `filter(Predicate)` to select items
    * `map(Function)` to transform elements
    * `distinct()` to remove duplicates
    * `sorted(Comparator)` for ordering
    * `flatMap(...)` for nested lists
  * *Terminal Operations*

    * `collect(Collectors.toList())` or `toSet()`
    * `reduce()` for combining elements
    * `forEach(...)` for side‐effects
    * `count()`, `anyMatch()`, `allMatch()` for boolean/predicate checks
  * *Collectors*

    * `Collectors.groupingBy(...)` to group elements
    * `Collectors.partitioningBy(...)` to partition by predicate
    * `Collectors.joining(...)` for string concatenation
    * Downstream collectors (e.g., `Collectors.groupingBy(..., Collectors.counting())`)
  * *Parallel Streams*

    * `parallelStream()` vs. sequential
    * Thread‐safety concerns when using shared mutable state
    * Performance considerations: overhead vs. speedup

* **1.4 Concurrency & Multithreading**

  * *Thread Creation*

    * Extending `Thread` vs. implementing `Runnable`
    * Using `Callable` to return results from threads
    * `Executors.newFixedThreadPool(...)` for managing thread pools
  * *Synchronization*

    * `synchronized` keywords on methods and blocks
    * `ReentrantLock` vs. synchronized blocks (fair vs. non‐fair locks)
    * `volatile` fields for visibility guarantees
  * *Executor Framework*

    * `ExecutorService` lifecycle (`shutdown()`, `awaitTermination()`)
    * `ScheduledExecutorService` for delayed/periodic tasks
    * Configuring thread pool sizes (`newFixedThreadPool`, `newCachedThreadPool`)
  * *CompletableFuture*

    * `supplyAsync(...)` and `runAsync(...)` for asynchronous tasks
    * Chaining (`thenApply`, `thenAccept`, `thenCompose`)
    * Combining results (`allOf(...)`, `anyOf(...)`)
    * Exception handling (`exceptionally`, `handle`)
  * *Concurrent Collections*

    * `ConcurrentHashMap` for thread-safe maps
    * `CopyOnWriteArrayList` and `CopyOnWriteArraySet` for safe iteration
    * `BlockingQueue` implementations (`LinkedBlockingQueue`, `ArrayBlockingQueue`)
  * *Thread Safety & Pitfalls*

    * Race conditions and critical sections
    * Deadlock scenarios and avoidance
    * Liveness issues (starvation, livelock)

---

**2. Frameworks & Libraries**

* **2.1 Spring Boot / Spring Core / Spring MVC**

  * *Auto-Configuration*

    * `@SpringBootApplication` composition (`@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan`)
    * Starter dependencies (e.g., `spring-boot-starter-web`) enabling default beans (Tomcat, Jackson)
    * Excluding auto-configurations (e.g., `@EnableAutoConfiguration(exclude=…)`)
  * *Dependency Injection (DI)*

    * Constructor Injection vs. Field Injection vs. Setter Injection
    * Bean discovery with `@Component`, `@Service`, `@Repository`, `@Controller`
    * Qualifiers and custom beans (`@Qualifier`, `@Primary`)
    * Bean scopes (singleton, prototype, request, session, application)
  * *Bean Lifecycle & Profiles*

    * Post‐construct and pre‐destroy callbacks (`@PostConstruct`, `@PreDestroy`)
    * Conditional beans (`@ConditionalOnProperty`, `@ConditionalOnMissingBean`)
    * Using Spring Profiles (`@Profile("dev")`) to load environment‐specific beans
  * *REST Controllers*

    * `@RestController` vs. `@Controller` + `@ResponseBody`
    * Request mappings (`@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`)
    * Binding request parameters (`@PathVariable`, `@RequestParam`, `@RequestBody`)
    * Returning `ResponseEntity<>` with custom status codes and headers
    * Validation annotations (`@Valid`, `@Validated`, `@NotNull`, `@Size`)

* **2.2 Spring Data JPA & Hibernate**

  * *Entity Mapping Basics*

    * `@Entity`, `@Table`, `@Id`, `@GeneratedValue(strategy=…)`
    * Column mapping (`@Column`, `@Enumerated`, `@Temporal`)
    * Composite primary keys (`@EmbeddedId`, `@IdClass`)
  * *Relationships*

    * One‐to‐One (`@OneToOne`) and how to map unidirectional vs. bidirectional
    * One‐to‐Many (`@OneToMany(mappedBy="…")`) vs. Many‐to‐One (`@ManyToOne`)
    * Many‐to‐Many (`@ManyToMany`) with join tables (`@JoinTable`)
    * Cascade types (`CascadeType.PERSIST`, `MERGE`, `REMOVE`, etc.) and orphan removal
    * Fetch types: `FetchType.LAZY` vs. `FetchType.EAGER` and implications
  * *JPQL vs. Criteria API*

    * Writing JPQL queries (`@Query("SELECT u FROM User u WHERE u.email = :email")`)
    * Using `EntityManager.createQuery(...)` for dynamic JPQL
    * Criteria API: building type-safe queries with `CriteriaBuilder`, `CriteriaQuery`
  * *Repository Interfaces*

    * `CrudRepository`, `JpaRepository` methods (`save`, `findById`, `findAll`, `delete`)
    * Derived query methods (`findByUsername`, `findByStatusOrderByCreatedDate`)
    * Pagination and sorting (`Pageable`, `Sort`)
  * *Hibernate Session & Cache*

    * First‐level cache (session scope) and entity state transitions (transient, persistent, detached)
    * Second‐level cache providers (EHCache, Hazelcast) and `@Cacheable`
    * Query cache vs. entity cache and using `@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)`
    * Flush modes (`FlushMode.AUTO`, `FlushMode.COMMIT`) and transaction boundaries

* **2.3 Vert.x**

  * *Verticle Basics*

    * Extending `AbstractVerticle` and overriding `start()` and `stop()`
    * Deploying verticles (`vertx.deployVerticle(...)`, options like `instances`)
    * Worker verticles vs. standard verticles for blocking code
  * *EventBus*

    * Sending messages (`eventBus.send(address, message)`) vs. publishing (`publish(address, message)`)
    * Registering consumers (`eventBus.consumer(address, handler)`)
    * Reply handlers (`message.reply(...)`) and request‐response pattern
    * Message codecs for custom objects (register codec)
  * *Vert.x HTTP Server*

    * Creating `HttpServer` and `Router`
    * Defining routes (`router.route("/vertx/processTask").handler(routingContext -> {...})`)
    * Using `RoutingContext` to handle requests and responses
    * Nonblocking I/O with `Vertx.executeBlocking(...)` for CPU‐bound tasks
  * *Integrating with Spring Boot*

    * Launching a Vert.x verticle from a Spring `@Component` using `Vertx.vertx().deployVerticle(...)`
    * Sharing configuration beans between Spring and Vert.x

* **2.4 Resilience4j**

  * *Circuit Breaker Basics*

    * States: CLOSED, OPEN, HALF\_OPEN
    * Configuration properties: `failureRateThreshold`, `slowCallRateThreshold`, `ringBufferSizeInClosedState`, `ringBufferSizeInHalfOpenState`
    * Using `CircuitBreakerRegistry` to create/configure breakers programmatically
    * Annotation support: `@CircuitBreaker(name="externalService", fallbackMethod="fallback")`
  * *Retry Mechanism*

    * `@Retry(name="externalServiceRetry")` configuration (`maxAttempts`, `waitDuration`)
    * Synchronous vs. asynchronous retries
    * Backoff strategies (exponential backoff, fixed backoff)
  * *Bulkhead & Rate Limiter*

    * Bulkhead types: semaphore‐based vs. thread‐pool‐based isolation
    * Configuring `BulkheadConfig` (maxConcurrentCalls, maxWaitDuration)
    * Rate limiting (permits per period, timeout duration) with `RateLimiterConfig`
  * *Fallback Methods*

    * Defining fallback signatures (`fallbackMethod(String id, Exception ex)`)
    * Returning default values vs. wrapping in `Try`

* **2.5 Debezium**

  * *Connector Configuration*

    * `connector.class=io.debezium.connector.postgresql.PostgresConnector`
    * Database connection settings (`database.hostname`, `database.port`, `database.user`, `database.password`)
    * Snapshot mode (`snapshot.mode=initial`) and slot name (`plugin.name=pgoutput`)
    * Topic prefix and schema naming strategy
  * *Change Event Structure*

    * Envelope fields: `schema`, `payload`
    * `payload.before`, `payload.after`, `payload.source`, `payload.op` (c for create, u for update, d for delete)
  * *Integration with Kafka*

    * Topic naming: `serverName.databaseName.schemaName.tableName`
    * Handling tombstone messages for deletes
    * Schema evolution: using Avro converter vs. JSON converter
  * *Handling Schema Changes*

    * Debezium’s support for schema registry (Confluent Schema Registry)
    * Evolving Avro schemas and backward/forward compatibility

---

**3. Architectural & Design Patterns**

* **3.1 Microservices**

  * *Bounded Context & Service Granularity*

    * Defining business capabilities per service
    * Avoiding data coupling; each service owns its data
  * *API Design Principles*

    * REST conventions: resource naming, HTTP methods, status codes
    * HATEOAS (Hypermedia as the Engine of Application State) basics
    * Versioning strategies (URI versioning, header versioning)
  * *Database per Service*

    * Each microservice has its own database schema/instance
    * Avoiding shared database tables across services
    * Handling cross-service transactions (two-phase commit vs. Sagas)
  * *Synchronous vs. Asynchronous Communication*

    * REST calls using `RestTemplate` or `WebClient` for immediate and blocking requests
    * Messaging via Kafka or RabbitMQ for eventual consistency and decoupling

* **3.2 Event-Driven Architecture**

  * *Event Types*

    * Domain events vs. integration events
    * Command events vs. Event notifications
  * *Event Schema Design*

    * Choosing JSON vs. Avro vs. Protobuf
    * Defining schema evolution rules (backward-compatible changes, optional fields)
  * *Publish/Subscribe Patterns*

    * Single producer, multiple consumers (fan-out)
    * Ensuring idempotency in consumers (use of unique event IDs)
  * *Event Ordering & Idempotency*

    * Partitioning strategy (partition by key for ordering within a partition)
    * Consumer design to handle duplicate or out-of-order events
  * *Ensuring Eventual Consistency*

    * Compensating transactions when failures occur
    * Saga choreography vs. orchestration

* **3.3 Service Discovery & Load Balancing**

  * *Eureka/Consul Setup*

    * Running a standalone Eureka/Consul server
    * Service registration via `@EnableDiscoveryClient`
    * Health check endpoints (`/actuator/health`) for registration
  * *Client-Side Load Balancing*

    * Ribbon (deprecated) vs. Spring Cloud LoadBalancer
    * `@LoadBalanced RestTemplate` or `WebClient` auto-configuration
    * Retry and timeout settings in load balancer clients
  * *Server-Side Load Balancing*

    * Using API gateway (Spring Cloud Gateway or Netflix Zuul) as a load balancer
    * Zero-downtime rolling updates and gateway configuration

* **3.4 API Gateway Pattern**

  * *Routing Configuration*

    * Defining route predicates (path, header, method) in `application.yml` or Java DSL
    * Path rewriting and prefix strip
  * *Request/Response Filters*

    * Pre‐filters for authentication/authorization checks
    * Post‐filters for adding headers, logging, response modification
  * *Rate Limiting & Throttling*

    * Configuring Redis-backed rate limiting in Spring Cloud Gateway
    * Rejecting requests with 429 (Too Many Requests) status
  * *Aggregation & Request Merging*

    * Fan-out fan-in patterns (aggregating multiple downstream calls into a single response)
    * Circuit breaker at the gateway level for fallback responses

* **3.5 Circuit Breaker Pattern**

  * *Resilience4j Integration*

    * `io.github.resilience4j.circuitbreaker.CircuitBreakerRegistry` usage
    * Monitoring circuit status (metrics) via Micrometer
  * *Configuration Parameters*

    * `failureRateThreshold`, `slowCallRateThreshold`
    * `ringBufferSizeInClosedState`, `ringBufferSizeInHalfOpenState`
    * `waitDurationInOpenState`
  * *Fallback Strategy*

    * Defining fallback methods signature and returning defaults
    * Nesting multiple resilience patterns (circuit breaker → retry → fallback)
  * *Metrics and Monitoring*

    * Exposing circuit breaker metrics via Actuator
    * Tracking success/failure rates in Grafana

* **3.6 Caching Strategies**

  * *Cache-aside Pattern*

    * Check cache before reading from DB; populate cache if miss
    * Evict or refresh cache on write operations
  * *Read-through & Write-through*

    * Configuration of cache provider to automatically load data
    * Direct writes to cache then propagate to DB (write‐behind)
  * *Eviction & Expiration*

    * TTL (time‐to‐live) settings in Redis/Caffeine
    * LRU/LFU eviction policies and memory considerations
  * *Choosing In-Memory vs. Distributed*

    * Caffeine or Guava for single-instance, low-latency caching
    * Redis for shared cache across multiple application instances

* **3.7 Asynchronous/Reactive Patterns**

  * *Reactive Programming Basics*

    * Publisher, Subscriber, Subscription interfaces (Reactive Streams)
    * Reactor’s `Mono` vs. `Flux` for 0–1 and 0–N streams
    * Backpressure mechanisms and controlling request demand
  * *Vert.x vs. Spring WebFlux*

    * Vert.x event loop, non-blocking I/O vs. Spring WebFlux on Reactor Netty
    * Defining reactive controllers (`@RestController` returning `Mono` or `Flux`)
    * Data access with reactive repositories (R2DBC for SQL, Reactive MongoRepository)
  * *CompletableFuture vs. RxJava*

    * Chaining asynchronous calls with `thenCompose`, `thenCombine`
    * RxJava’s `Observable`, `Single`, `Maybe`, and backpressure strategies

* **3.8 Messaging Patterns**

  * *Publish-Subscribe (Pub/Sub)*

    * Kafka topics with multiple consumers in different consumer groups
    * RabbitMQ fanout exchanges for broadcast
    * Ensuring message ordering and delivery guarantees
  * *Point-to-Point (Queue)*

    * RabbitMQ direct or topic exchange routing to a queue
    * JMS queues for synchronous or asynchronous processing
  * *Idempotent Consumer Design*

    * Deduplication keys in event payloads
    * Storing processed event IDs in a fast lookup (Redis)
  * *Dead-Letter Queues & Retries*

    * Routing failed messages to DLQ after max retries
    * Configuring TTL and dead‐letter exchange in RabbitMQ

---

**4. Data & Persistence (Relational & NoSQL)**

* **4.1 Relational Databases**

  * *Schema Design Principles*

    * Normalization forms (1NF, 2NF, 3NF) vs. denormalization trade-offs
    * Primary keys (surrogate vs. natural) and foreign keys
    * Relationship cardinalities (1:1, 1\:N, N\:N)
  * *SQL Query Optimization*

    * Using `EXPLAIN ANALYZE` to inspect query plans
    * Creating indexes (B-tree, GIN, GiST) on frequently filtered columns
    * Analyzing slow queries, optimizing joins (using smaller tables first)
  * *PL/SQL Constructs*

    * Writing stored procedures and functions (`CREATE PROCEDURE`, `FUNCTION`)
    * Handling exceptions in PL/SQL blocks (`EXCEPTION WHEN`)
    * Creating triggers for pre‐insert or post‐update actions
  * *Views & Materialized Views*

    * Creating virtual tables with `CREATE VIEW` for reporting
    * Refreshing materialized views (`REFRESH MATERIALIZED VIEW`) for faster read performance
  * *Transaction Management*

    * ACID properties (atomicity, consistency, isolation, durability)
    * Isolation levels (`READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`)
    * Locking mechanisms (row-level vs. table-level locks)

* **4.2 Schema Migration (Flyway/Liquibase)**

  * *Migration Scripting*

    * Writing versioned SQL scripts (`V1__Create_tables.sql`) or YAML/XML change sets
    * Describing incremental changes (adding columns, altering tables)
  * *Version Control & Rollback*

    * Tagging migration versions and maintaining a history table (`flyway_schema_history`)
    * Rolling back changes with `liquibase rollback` or undo scripts
  * *CI/CD Integration*

    * Automatically applying migrations during build/deploy phases
    * Handling destructive changes carefully in production

* **4.3 MongoDB**

  * *Document Modeling*

    * Embedding related data vs. referencing documents
    * Using `_id` field and custom IDs
    * Schema validation rules (JSON Schema validation)
  * *CRUD Operations*

    * Inserting documents (`insertOne`, `save`)
    * Querying with filters (`find(eq("level", "ERROR"))`)
    * Updating (`updateOne`, `findOneAndUpdate`) and deleting (`deleteOne`)
  * *Indexing Strategies*

    * Single‐field indexes vs. compound indexes
    * TTL indexes for expiring documents (logs)
    * Text indexes for full-text search
  * *Aggregation Framework*

    * Stages: `$match`, `$group`, `$project`, `$sort`, `$limit`
    * Pipeline building in Java (`Aggregation.newAggregation(...)`)

* **4.4 Cassandra**

  * *Data Modeling*

    * Wide‐column concept: partition key and clustering key
    * Designing tables for query patterns (query‐driven modeling)
  * *CQL Syntax*

    * `CREATE KEYSPACE IF NOT EXISTS app WITH replication = {...};`
    * `CREATE TABLE metrics (user_id UUID, metric_name text, metric_value double, PRIMARY KEY (user_id, metric_name));`
  * *Consistency Levels*

    * `LOCAL_ONE`, `LOCAL_QUORUM`, `QUORUM`, `ALL` and their trade-offs
    * Reading your own writes and setting appropriate consistency
  * *Secondary Indexes & Materialized Views*

    * Creating and using secondary indexes (`CREATE INDEX ON metrics(metric_name);`)
    * Limitations of materialized views (staleness, performance)
  * *Repair & Maintenance*

    * Running `nodetool repair` to fix inconsistencies
    * Monitoring compaction and tombstones

* **4.5 Redis**

  * *Data Structures*

    * Strings (`SET`, `GET`), Hashes (`HSET`, `HGET`), Lists (`LPUSH`, `LRANGE`), Sets (`SADD`, `SMEMBERS`), Sorted Sets (`ZADD`, `ZRANGE`)
  * *TTL & Eviction Policies*

    * Setting expiration (`EXPIRE key seconds`)
    * Eviction policies: `volatile-lru`, `allkeys-lfu`, etc., in `redis.conf`
  * *Pub/Sub Basics*

    * `PUBLISH channel message` and `SUBSCRIBE channel`
    * Use cases for real‐time notifications
  * *Lua Scripting*

    * Writing atomic Lua scripts (`EVAL`), common patterns (check and set)
    * Using Redis for distributed locks (`SET key value NX EX seconds`)

* **4.6 DynamoDB**

  * *Table Design*

    * Primary key types (partition key only vs. partition + sort key)
    * Using Global Secondary Index (GSI) vs. Local Secondary Index (LSI)
  * *Capacity Modes*

    * Provisioned capacity: read/write capacity units, auto-scaling
    * On-demand capacity mode and cost considerations
  * *CRUD with AWS SDK*

    * `PutItemRequest`, `GetItemRequest`, `QueryRequest`, `ScanRequest`
    * Handling large result sets with pagination (`ExclusiveStartKey`)
  * *Best Practices*

    * Avoid hot partitions (distribute keys evenly)
    * Use BatchWriteItem and BatchGetItem for bulk operations

---

**5. Messaging & Integration**

* **5.1 Apache Kafka**

  * *Topic & Partition Design*

    * Choosing partition count for scalability vs. ordering guarantees
    * Topic retention policies and cleanup policies (delete vs. compact)
  * *Producer Configuration*

    * Acknowledgment levels (`acks=all`, `acks=1`)
    * Retries (`retries`, `retry.backoff.ms`) and idempotence (`enable.idempotence=true`)
    * Batch settings (`batch.size`, `linger.ms`) for throughput tuning
  * *Consumer Configuration*

    * Consumer groups (`group.id`, `auto.offset.reset=earliest` or `latest`)
    * Max poll records (`max.poll.records`), session timeouts (`session.timeout.ms`)
    * Handling rebalancing (`ConsumerRebalanceListener`)
  * *Serialization Formats*

    * StringSerializer vs. JSON Serializer (`JsonSerializer`)
    * Avro/Schema Registry integration for schema evolution
  * *Consumer Rebalancing & Offset Management*

    * Automatic vs. manual commits (`enable.auto.commit=false`)
    * Seeking offsets (`seek()`) for replay or skipping

* **5.2 RabbitMQ**

  * *Exchange Types & Use Cases*

    * Direct exchange (exact matching)
    * Fanout exchange (broadcast to all queues)
    * Topic exchange (pattern matching in routing keys)
    * Headers exchange (matching on header values)
  * *Queue Properties*

    * Durable vs. transient queues (`durable=true`)
    * Exclusive queues and auto-delete queues
  * *Binding Keys & Routing*

    * Binding a queue to an exchange with a specific key (`task.create`)
    * Wildcard routing (`task.*`, `task.#`) in topic exchanges
  * *Acknowledgment Modes*

    * Auto‐ack (`autoAck=true`) vs. manual ack (`channel.basicAck`)
    * Rejecting (`basicReject`) or requeueing (`basicNack`) messages
  * *Prefetch Count & QoS*

    * Setting `channel.basicQos(prefetchCount=10)` to limit unacked messages
    * Impact on consumer throughput and fairness

* **5.3 ActiveMQ / JMS**

  * *JMS API Basics*

    * Creating `ConnectionFactory`, `Connection`, `Session`
    * Sending messages with `MessageProducer` (`TextMessage`, `ObjectMessage`)
    * Receiving messages via `MessageConsumer` and `MessageListener`
  * *Message Types*

    * `TextMessage`, `ObjectMessage`, `BytesMessage`, `MapMessage`, `StreamMessage`
  * *Durable Subscriptions*

    * Configuring `session.createDurableSubscriber(topic, subscriptionName)`
    * Persisting subscriptions across consumer restarts
  * *Message Selectors*

    * Filtering messages on the consumer side (`MessageConsumer consumer = session.createConsumer(queue, "priority > 5")`)
  * *Transactional Sessions & Acknowledgment Modes*

    * Using `Session.SESSION_TRANSACTED` vs. `AUTO_ACKNOWLEDGE` vs. `CLIENT_ACKNOWLEDGE`
    * Committing/rolling back JMS transactions

* **5.4 Debezium CDC**

  * *Connector Setup & Configuration*

    * Defining connector properties (`database.server.name`, `database.whitelist`, `table.whitelist`)
    * Configuring snapshot modes (`initial`, `schema_only`, `never`)
  * *Event Envelope Structure*

    * Decoding `before` vs. `after` fields for change events
    * Using `op` field to determine insert (`c`), update (`u`), or delete (`d`)
  * *Kafka Topic Naming & Serialization*

    * Default topic naming convention (`{serverName}.{databaseName}.{tableName}`)
    * Converters: JSON converter vs. Avro converter with Schema Registry
  * *Handling Schema Evolution*

    * Automatic schema updates vs. manual migrations
    * Dealing with column additions/removals without service downtime
  * *Fault Tolerance & Offsets*

    * Debezium’s offset storage (Kafka or file-based)
    * Resuming connectors after restart

---

**6. Cloud, Containerization & DevOps**

* **6.1 AWS Cloud Services**

  * *EC2 Fundamentals*

    * Launching instances (AMI selection, instance types)
    * Security groups (inbound/outbound rules)
    * Elastic IPs vs. public IP assignment
  * *S3 Usage*

    * Bucket creation and region selection
    * Object upload/download (`PutObjectRequest`, `GetObjectRequest`)
    * Pre‐signed URLs for temporary access
    * Lifecycle policies (transition to Glacier, expiration)
  * *RDS Basics*

    * Selecting engine (MySQL, PostgreSQL), instance classes, storage types
    * Automated backups and point-in-time recovery
    * Read replicas for scaling reads
  * *DynamoDB Integration*

    * Configuring AWS SDK credentials (IAM roles, environment variables)
    * Table creation and key schema definition (partition + sort key)
    * Query vs. Scan operations and Index usage
  * *Lambda Functions*

    * Writing handler methods (`public String handler(Map<String, Object> input, Context ctx)`)
    * Deployment packaging (zip file or container image)
    * Triggering via API Gateway, S3 events, or CloudWatch Events
  * *CloudWatch*

    * Defining custom metrics (publishing with `CloudWatchClient.putMetricData`)
    * Creating alarms (CPUUtilization > threshold)
    * Log groups and log streams (pushing application logs)

* **6.2 Docker & Container Orchestration**

  * *Dockerfile Best Practices*

    * Multi-stage builds: separate build and runtime stages
    * Minimizing image size (using `openjdk:11-jre-slim` vs. `openjdk:11-jdk`)
    * Proper layer ordering to leverage build cache (`COPY pom.xml`, `RUN mvn dependency:go-offline`)
  * *Docker Compose Syntax*

    * Defining services (`service:`, `image:`, `build:`, `ports:`, `volumes:`)
    * Networking (`networks:`) and service dependencies (`depends_on:`)
    * Shared volumes for data persistence
  * *Networking Modes*

    * Bridge network for container isolation
    * Host network for performance (no network namespace)
    * Overlay network in Docker Swarm or Kubernetes
  * *Resource Constraints*

    * Limiting CPU (`--cpus`) and memory (`--memory`) for services
    * Using `ulimits` for file descriptors, process counts
  * *Inter-Service Communication*

    * Linking containers (service discovery via DNS in Docker Compose)
    * Health checks (`healthcheck:`) to verify service readiness

* **6.3 CI/CD & Build Tools**

  * *Maven Project Structure*

    * `pom.xml` sections (dependencies, plugins, build, scm, properties)
    * Dependency scopes (`compile`, `provided`, `runtime`, `test`, `system`)
    * Common plugins (Surefire for tests, JaCoCo for code coverage)
  * *Gradle Build Scripts*

    * `build.gradle` DSL vs. Kotlin DSL
    * Dependency configurations (`implementation`, `compileOnly`, `testImplementation`)
    * Custom tasks and plugins (application plugin, Docker plugin)
  * *Jenkins Pipeline Syntax*

    * Declarative pipeline (`pipeline {`, `agent {`, `stages {`, `steps {`)
    * Scripted pipeline (`node {`, `stage('Build') { … }`)
    * Environment variables and credentials binding (`withCredentials`)
  * *GitHub Actions Workflows*

    * `jobs:` and `steps:` syntax in `.github/workflows/ci.yml`
    * Using official actions (checkout, setup‐java, cache‐maven, actions/upload‐artifact)
    * Matrix builds for multiple JDK versions
  * *Flyway/Liquibase Integration*

    * Configuring Flyway in `pom.xml` (plugins, properties)
    * Liquibase changelog (`db.changelog-master.yaml`) and contexts (dev, prod)
  * *Docker Image Tagging & Registry*

    * Tagging images with `:${{ github.sha }}` or `:${BUILD_NUMBER}`
    * Pushing to Docker Hub (`docker push`) or AWS ECR (`aws ecr create-repository`, `docker push`)
  * *Deployment Strategies*

    * Blue-Green deployments with separate stacks
    * Rolling updates in Kubernetes (Deployment strategy: rollingUpdate)

---

**7. Security & Access Control**

* **7.1 JWT & OAuth 2.0**

  * *JWT Structure*

    * Header (algorithm, token type)
    * Payload/Claims (subject (`sub`), issuer (`iss`), expiration (`exp`), custom claims)
    * Signature (HMAC vs. RSA signing)
  * *Signing Algorithms*

    * HS256 (symmetric, shared secret)
    * RS256 (asymmetric, private/public key pair)
  * *OAuth 2.0 Flows*

    * Authorization Code Flow (for web/mobile apps)
    * Client Credentials Flow (machine-to-machine authentication)
    * Implicit Flow (deprecated, single‐page apps)
    * Refresh Tokens (obtaining new access tokens)
  * *Token Revocation & Blacklisting*

    * Maintaining a revocation list (in-memory or Redis)
    * Shorter token TTL with refresh tokens for security

* **7.2 Spring Security Configuration**

  * *Security Filter Chain*

    * Configuring `HttpSecurity` (CSRF, CORS, permitted URLs, form login vs. JWT)
    * Disabling default security (`http.csrf().disable()`) for REST APIs
  * *Role vs. Authority Mapping*

    * `GrantedAuthority` vs. `SimpleGrantedAuthority("ROLE_USER")`
    * Granting multiple authorities to a single user
  * *Authentication Mechanisms*

    * In‐memory authentication (`AuthenticationManagerBuilder.inMemoryAuthentication()`)
    * JDBC‐based user store (`JdbcUserDetailsManager`)
    * OAuth2 resource server (`http.oauth2ResourceServer().jwt()`)
  * *Custom UserDetailsService*

    * Implement `UserDetails` to wrap domain user object
    * Implement `UserDetailsService.loadUserByUsername(...)` to fetch user from DB
  * *Password Encoding*

    * Using `BCryptPasswordEncoder` for hashing passwords
    * Upgrading encoding algorithms (delegating password encoder)

* **7.3 RBAC & Permission Enforcement**

  * *Method-Level Security*

    * `@PreAuthorize("hasRole('ADMIN')")` vs. `@Secured("ROLE_ADMIN")`
    * `@PostAuthorize("returnObject.owner == authentication.name")` for checking return values
  * *Custom Permission Evaluator*

    * Implementing `PermissionEvaluator` interface
    * Registering custom `PermissionEvaluator` in `MethodSecurityConfigurer`
  * *Scope and Claim Checks in JWT*

    * Extracting scopes from JWT (`"scope": "read write"`)
    * Validating scopes in filters or method annotations
  * *Security Filters*

    * `OncePerRequestFilter` to parse JWT, set `Authentication` in `SecurityContext`
    * `UsernamePasswordAuthenticationFilter` for form-based login

---

**8. Observability, Logging & Monitoring**

* **8.1 Logging Frameworks & Configuration**

  * *SLF4J Facade Usage*

    * Declaring a logger: `private static final Logger log = LoggerFactory.getLogger(MyClass.class);`
    * Logging at levels (`log.info`, `log.debug`, `log.error`)
  * *Logback Configuration*

    * `logback-spring.xml` syntax (appenders: `ConsoleAppender`, `RollingFileAppender`)
    * Defining `PatternLayoutEncoder` for custom log format (`%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n`)
    * Configuring log levels per package (`<logger name="com.example" level="DEBUG"/>`)
  * *JSON Log Formatting*

    * Using `LogstashEncoder` (logstash-logback-encoder dependency) for JSON output
    * Including MDC (Mapped Diagnostic Context) fields like `traceId`, `spanId`
  * *Log4j2 Configuration*

    * `log4j2.xml` appenders (`Console`, `File`, `RollingFile`)
    * Filter conditions (threshold filter, regex filter)

* **8.2 Centralized Log Management & Aggregation**

  * *Logstash Configuration*

    * Input plugins (`beats`, `tcp`, `file`) to ingest logs
    * Filter plugins (`grok`, `mutate`, `date`) to parse JSON or text logs
    * Output plugins (`elasticsearch`, `stdout`) to forward to Elasticsearch
  * *Elasticsearch Indexing*

    * Creating index templates (mappings, settings)
    * Defining index patterns (`logs-*`) in Kibana
    * Using ILM (Index Lifecycle Management) to rollover indices
  * *Kibana Basics*

    * Creating visualizations (bar chart, pie chart, line graph) on log data
    * Building dashboards combining multiple panels (CPU usage, error counts)
    * Setting up alerts and notifications on thresholds (e.g., error rate > 5%)
  * *CloudWatch Logs Agent*

    * Installing CloudWatch Agent on EC2 or containers
    * Configuring `amazon-cloudwatch-agent.json` for log file paths
    * Defining log groups and streams, retention settings

* **8.3 Metrics Collection & Visualization**

  * *Micrometer Integration*

    * Adding `micrometer-registry-prometheus` or `micrometer-registry-cloudwatch` dependency
    * Using `MeterRegistry.counter("counter.name")` and `MeterRegistry.gauge("gauge.name", obj, obj::size)`
    * Configuring `management.metrics.export.prometheus.enabled=true`
  * *Custom Meters*

    * `Counter` for counting events (`taskCreatedCounter.increment()`)
    * `Timer` for tracking durations (`Timer.builder("task.duration").tag("service", "taskService").register(meterRegistry)`)
    * `DistributionSummary` for payload sizes or histogram data
  * *Prometheus Scrape Configuration*

    * `scrape_configs:`

      * `- job_name: 'app'`
      * `static_configs: - targets: ['localhost:8080']`
    * Relabeling and metric relabeling for multi‐environment
  * *Grafana Dashboard Design*

    * Importing dashboards via JSON (single panel to multiple rows)
    * Querying Prometheus metrics (`rate(task_duration_seconds_count[5m])`)
    * Using template variables (e.g., `$instance`, `$service`)
    * Setting up alerts (e.g., if CPU usage > 80% for 5m)

* **8.4 Distributed Tracing**

  * *Spring Sleuth Integration*

    * Adding `spring-cloud-starter-sleuth` dependency
    * Automatic instrumenting of HTTP requests, Kafka messages, RabbitMQ, etc.
    * Using `Tracer` to create custom spans (`Span newSpan = tracer.nextSpan().name("custom-span")`)
  * *Zipkin Setup*

    * Running Zipkin server (`docker run -d -p 9411:9411 openzipkin/zipkin`)
    * Configuring `spring.zipkin.base-url=http://localhost:9411` and `spring.sleuth.sampler.probability=1.0`
    * Viewing distributed traces in Zipkin UI (service graph, trace span timeline)
  * *Correlation of Logs & Traces*

    * Propagating trace IDs to logs via MDC (`%X{traceId}` in log pattern)
    * Using `@NewSpan` or `Tracer.nextSpan()` to annotate methods
    * Visualizing end-to-end request flows across microservices

---

This three‐level hierarchical outline (Level 1 → Level 2 → Level 3) should comprehensively cover all concepts from your resume. You can now use these structured topics to design detailed demos, documentation, or learning modules.
