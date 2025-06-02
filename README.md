Below are the nine must-know sections. For each bullet (the “must-know” item), you’ll find one level of deeper explanation—key facts, definitions, or clarifications that you should understand before moving on. No advanced tangents, just the immediate next layer of detail.

---

## 1. Java Core & Backend Development

1. **OOP Fundamentals: Inheritance, Polymorphism, Encapsulation, and Overriding vs. Overloading**

   * **Inheritance:** A subclass (“child”) reuses fields and methods of its parent class. It enables code reuse (e.g., `class Employee extends Person`).
   * **Polymorphism:** A variable of a parent type can hold instances of child types. At runtime, calling `animal.speak()` actually invokes `Dog.speak()` or `Cat.speak()` depending on the object.
   * **Encapsulation:** Keep fields `private` and expose controlled access via getters/setters. This prevents external code from putting an object into an invalid state.
   * **Method Overriding:** A subclass provides its own implementation of a method declared in its superclass (same signature). Enables runtime polymorphism.
   * **Method Overloading:** Multiple methods in the same class share the same name but differ by parameter types or counts. The compiler decides which to call at compile time.

2. **Collections Framework: Differences and Use-Cases for List, Set, Map, and Common Implementations (ArrayList, HashSet, HashMap)**

   * **List (Ordered, Allow Duplicates):**

     * Implementations: `ArrayList` (backed by a resizable array; fast random access, slower inserts/removals in middle), `LinkedList` (doubly linked; fast inserts/removals but slower random access).
     * Use when order matters or you need indexed access (`get(i)`).
   * **Set (Unordered, No Duplicates):**

     * `HashSet`: Backed by a hash table; `add()`, `contains()` are O(1) on average. Ordering is unpredictable.
     * `LinkedHashSet`: Maintains insertion order.
     * `TreeSet`: Sorted order (natural or via comparator); operations O(log n).
   * **Map (Key→Value Association):**

     * `HashMap`: O(1) average lookup/insert; allows one null key.
     * `LinkedHashMap`: Preserves insertion order; useful when you need reproducible iteration.
     * `TreeMap`: Sorted by key; O(log n) for most operations.
   * **Choosing a Collection:** Think about whether you need ordering, duplicates, or fast lookups.

3. **Exception Handling: Checked vs. Unchecked Exceptions, Custom Exceptions, and Try-With-Resources**

   * **Checked Exceptions:** Must declare in method signature (`throws IOException`) or catch them. Used for recoverable conditions (e.g., file not found).
   * **Unchecked Exceptions (RuntimeException):** Don’t need to be declared or caught; used for programming errors (e.g., `NullPointerException`, `IllegalArgumentException`).
   * **Custom Exceptions:** Extend `RuntimeException` or `Exception` to represent domain-specific errors (e.g., `InvalidUserInputException`). Choose checked vs. unchecked based on whether callers are expected to recover.
   * **Try-With-Resources:** Simplifies closing resources (e.g., files, database connections). Any `AutoCloseable` opened in the `try(...)` header is closed automatically. Prevents resource leaks.

4. **Concurrency Basics: Creating Threads (Runnable vs. Callable), synchronized, and Thread Pools via ExecutorService**

   * **Runnable vs. Callable:**

     * `Runnable`: Has `run()` returning `void`. Submit to a `Thread` or executor for fire-and-forget tasks.
     * `Callable<V>`: Defines `call()` that returns a value and can throw checked exceptions. Submit to an executor to get a `Future<V>`.
   * **synchronized Keyword:** Locks the object or class monitor to prevent multiple threads from executing a block or method concurrently. Use sparingly—overuse can cause contention.
   * **ExecutorService:** A higher-level API to manage thread pools. Common methods:

     * `Executors.newFixedThreadPool(n)`: Creates a pool of `n` threads.
     * `submit(Runnable)`/`submit(Callable)`: Schedules tasks for execution.
     * `shutdown()`: Initiates an orderly shutdown, not accepting new tasks.

5. **Java 8+ Features: Lambda Expressions, Stream API for Collections, and Optional Usage**

   * **Lambda Syntax:** `(parameters) -> expression` or `(parameters) -> { statements; }`. Replaces anonymous inner classes for single-method interfaces (functional interfaces).
   * **Stream API:**

     * `collection.stream()` creates a pipeline.
     * Intermediate operations (`filter`, `map`, `sorted`) are lazy and return another Stream.
     * Terminal operations (`collect`, `forEach`, `reduce`) trigger the execution and produce results.
   * **Optional:** A container object that may or may not contain a non-null value. Methods like `isPresent()`, `orElse()`, `map()` help avoid explicit null checks and `NullPointerException`.

6. **JVM Memory & GC: Heap vs. Stack, Purpose of Garbage Collection, and Basics of Tuning (-Xms, -Xmx)**

   * **Stack vs. Heap:**

     * **Stack:** Stores method frames and local variables. Each thread has its own stack. Methods push/pop frames as they call/return.
     * **Heap:** Shared among threads; stores all Java objects and arrays. Garbage collector reclaims unreachable objects.
   * **Garbage Collection:** Automatically frees memory for objects no longer referenced. Common collectors: G1 (default), Parallel, CMS. GC events can cause pauses; understanding them is crucial for performance tuning.
   * **JVM Options:**

     * `-Xms<size>` sets initial heap size.
     * `-Xmx<size>` sets maximum heap size.
     * Keeping `-Xms` and `-Xmx` equal can reduce resizing overhead.
     * Additional tuning flags (e.g., `-XX:+UseG1GC`) can be learned later.

7. **Design Patterns (Core): Singleton, Factory, Strategy—Why and When to Use Them**

   * **Singleton:** Ensures only one instance of a class exists (e.g., a configuration manager). Common implementation uses a private constructor and a static `getInstance()` method. Be aware of threading issues—use `enum` singleton or double-checked locking with `volatile`.
   * **Factory Pattern:** Encapsulates object creation. Instead of calling `new Car()`, you call `VehicleFactory.create("car")`. Improves flexibility when you need to switch implementations without changing client code.
   * **Strategy Pattern:** Defines a family of interchangeable algorithms. E.g., `PaymentStrategy` interface with `CreditCardStrategy` and `PaypalStrategy`. Use `context.setStrategy(new CreditCardStrategy())`. Good for varying behavior at runtime.

8. **Unit Testing with JUnit: Writing Simple Tests, Using Assertions, and Understanding Test Lifecycle Annotations (@BeforeEach, @Test)**

   * **@Test Annotation:** Indicates a method is a test case. JUnit will run it and report success/failure.
   * **Assertions:**

     * `assertEquals(expected, actual)`, `assertTrue(condition)`, `assertThrows(Exception.class, () -> ...)`.
     * Provide clear failure messages to make debugging easier.
   * **Test Lifecycle:**

     * `@BeforeEach`: Runs before every test; use to set up common test data or mocks.
     * `@AfterEach`: Runs after every test; use to clean up or reset static state.
     * `@BeforeAll`/`@AfterAll`: Static methods that run once per test class, e.g., starting an embedded database.

---

## 2. Spring Boot & Microservices

1. **Auto-Configuration & Starters: How spring-boot-starter-* Dependencies Bring in MVC, JPA, Actuator, etc., Without XML*\*

   * **Starter POMs:** For example, `spring-boot-starter-web` bundles Spring MVC, Jackson JSON, and an embedded Tomcat server. You don’t have to specify each dependency manually.
   * **@SpringBootApplication:** Combines `@EnableAutoConfiguration` (activates all auto-config classes), `@Configuration`, and `@ComponentScan` (scans your base package for `@Component`, `@Service`, `@Repository`).
   * **Conditional Configuration:** Auto-configuration classes check for the presence of certain classes on the classpath. If you add `spring-boot-starter-data-jpa`, Spring Boot auto-configures a `DataSource` and `EntityManagerFactory`.

2. **REST Controller Basics: @RestController, @RequestMapping/@GetMapping, Handling Path Variables and Request Bodies**

   * **@RestController:** A specialization of `@Controller` + `@ResponseBody`. All methods return JSON (or XML) by default without additional annotations.
   * **@GetMapping("/users/{id}")**: Shortcut for `@RequestMapping(method=RequestMethod.GET)`. Use `@PathVariable("id") Long id` to extract the `{id}` segment from the URL.
   * **@RequestBody:** Binds the HTTP request body (JSON) to a Java object. For example, `public ResponseEntity<User> createUser(@RequestBody CreateUserRequest req)`.
   * **Error Handling:** By default, Spring returns 400 if JSON is invalid. You can define `@ControllerAdvice` to handle exceptions globally.

3. **Dependency Injection: Constructor vs. Field Injection, and @Autowired vs. @Qualifier**

   * **Constructor Injection (Preferred):**

     ```java
     @Service
     public class UserService {
         private final UserRepository repo;
         public UserService(UserRepository repo) {
             this.repo = repo;
         }
     }
     ```

     Guarantees the dependency is not null and makes the class easier to test.
   * **Field Injection:**

     ```java
     @Autowired
     private UserRepository repo;
     ```

     Simple, but harder to unit-test and hides required dependencies.
   * **@Qualifier:** When multiple beans implement the same interface, use `@Qualifier("beanName")` to specify which one to inject.

4. **Spring Data JPA Fundamentals: Defining @Entity, @Id, Simple Repository Methods (findById, save)**

   * **@Entity:** Marks a POJO as a JPA entity, which maps to a database table. You must annotate a field with `@Id` to indicate the primary key.
   * **Repository Interface:**

     ```java
     public interface UserRepository extends JpaRepository<User, Long> { }
     ```

     Gives you CRUD methods like `findById(id)`, `save(entity)`, `deleteById(id)` without writing any SQL.
   * **Method Naming Convention:** Spring Data parses method names: `findByEmail(String email)` generates `SELECT * FROM user WHERE email = :email`.

5. **Application Properties & Profiles: Overriding Config via application-dev.properties, @ConfigurationProperties Binding**

   * **application.properties (or .yml):** Place default settings (e.g., `server.port=8080`, `spring.datasource.url=...`).
   * **Profiles:** Create `application-dev.properties` or `application-prod.properties`. Activate a profile with `-Dspring.profiles.active=dev` or in `application.properties` set `spring.profiles.active=dev`. This allows you to have environment-specific DB URLs, logging levels, etc.
   * **@ConfigurationProperties:**

     ```java
     @Component
     @ConfigurationProperties(prefix="app.mail")
     public class MailProperties {
         private String host;
         private int port;
         // getters/setters
     }
     ```

     Binds `app.mail.host` and `app.mail.port` from properties into the POJO.

6. **Spring Boot Actuator: Enabling /actuator/health and /metrics, and Why Health Checks Matter in Microservices**

   * **Dependency:** Add `spring-boot-starter-actuator`. By default, only `/actuator/health` and `/actuator/info` are exposed on port 8080.
   * **Health Indicators:** Spring automatically checks common subsystems (DS, RabbitMQ, Kafka). You can add a custom `HealthIndicator` bean to include application-specific checks.
   * **/metrics Endpoint:** Exposes Micrometer metrics (e.g., `jvm.memory.used`, `process.cpu.usage`). Useful for scraping by Prometheus.
   * **Why Health Matters:** In a cluster, orchestration platforms (Kubernetes, ECS) poll `/health` to decide if a container is “ready” or “healthy.” If it fails, the platform can restart it or remove it from load-balancer rotation.

7. **Basic Security: Securing Endpoints with spring-boot-starter-security, Configuring In-Memory Users, and Securing a Single Endpoint**

   * **Dependency:** Add `spring-boot-starter-security`. By default, all endpoints require authentication.
   * **In-Memory User Setup:**

     ```java
     @Bean
     public UserDetailsService users() {
         UserDetails user = User.withDefaultPasswordEncoder()
             .username("user")
             .password("password")
             .roles("USER")
             .build();
         return new InMemoryUserDetailsManager(user);
     }
     ```
   * **Securing a Single Endpoint:**

     ```java
     @Configuration
     public class SecurityConfig {
         @Bean
         public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
             http.authorizeRequests()
                 .antMatchers("/public/**").permitAll()
                 .anyRequest().authenticated()
                 .and().httpBasic();
             return http.build();
         }
     }
     ```

     Now, `/public/**` is open; everything else requires HTTP Basic auth.

8. **Service-to-Service Calls: Using RestTemplate or WebClient to Call Another Service and How to Configure Timeouts**

   * **RestTemplate Example:**

     ```java
     RestTemplate rest = new RestTemplate();
     String response = rest.getForObject("http://inventory-service/inventory/123", String.class);
     ```
   * **WebClient Example (Reactive):**

     ```java
     WebClient client = WebClient.create("http://inventory-service");
     Mono<String> respMono = client.get().uri("/inventory/{id}", 123)
         .retrieve().bodyToMono(String.class);
     String response = respMono.block(); // blocking for simplicity
     ```
   * **Timeouts:**

     * For `RestTemplate`, set `ClientHttpRequestFactory`:

       ```java
       HttpComponentsClientHttpRequestFactory factory = new HttpComponentsClientHttpRequestFactory();
       factory.setConnectTimeout(5000);
       factory.setReadTimeout(5000);
       return new RestTemplate(factory);
       ```
     * For `WebClient`, configure `TcpClient` with `readTimeout` and `connectTimeout`:

       ```java
       TcpClient tcp = TcpClient.create()
           .option(ChannelOption.CONNECT_TIMEOUT_MILLIS, 5000)
           .doOnConnected(conn -> conn.addHandlerLast(new ReadTimeoutHandler(5)));
       HttpClient httpClient = HttpClient.from(tcp);
       WebClient webClient = WebClient.builder().clientConnector(new ReactorClientHttpConnector(httpClient)).build();
       ```

---

## 3. Distributed Systems & Messaging

1. **CAP Theorem Essentials: Understanding Trade-Offs Between Consistency, Availability, and Partition Tolerance**

   * **Consistency (C):** All nodes see the same data at the same time—reads always return the latest write.
   * **Availability (A):** Every request receives a non-error response (not necessarily the latest data).
   * **Partition Tolerance (P):** The system continues to function despite arbitrary partitioning (network failures) between nodes.
   * **Real-World Implication:** In the presence of a network partition, you must choose between being available (serve possibly stale data) or consistent (reject requests until partition heals). Most large systems choose “AP” (eventual consistency) for higher availability.

2. **Message Broker Roles: Purpose of Brokers Like Kafka or RabbitMQ for Decoupling Services**

   * **Decoupling:** Producers send messages to a broker; consumers retrieve messages independently. Neither needs to know about the other’s existence or availability.
   * **Buffering:** If a consumer is down or slow, the broker retains messages until the consumer can process them. This prevents producer failures from cascading.
   * **Scalability:** You can scale producers and consumers independently. Brokers handle distributing messages across partitions or queues to achieve parallelism.

3. **Producer & Consumer Basics: Sending a Message to a Topic/Queue and Simple Consumer Polling**

   * **Producer (Pseudo-Code):**

     ```java
     Properties props = new Properties();
     props.put("bootstrap.servers", "localhost:9092");
     props.put("key.serializer", "StringSerializer");
     props.put("value.serializer", "StringSerializer");
     KafkaProducer<String, String> producer = new KafkaProducer<>(props);
     ProducerRecord<String, String> record = new ProducerRecord<>("orders", "order123", "OrderCreatedPayload");
     producer.send(record);
     producer.close();
     ```
   * **Consumer (Pseudo-Code):**

     ```java
     Properties props = new Properties();
     props.put("bootstrap.servers", "localhost:9092");
     props.put("group.id", "order-service-group");
     props.put("key.deserializer", "StringDeserializer");
     props.put("value.deserializer", "StringDeserializer");
     KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
     consumer.subscribe(Arrays.asList("orders"));
     while (true) {
         ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
         for (ConsumerRecord<String, String> rec : records) {
             // process rec.value()
         }
         consumer.commitSync();
     }
     ```

4. **Delivery Semantics: The Difference Between “At-Least-Once” and “Exactly-Once” Delivery, and Why Idempotency Matters**

   * **At-Least-Once:** The broker retry logic may deliver the same message more than once if it doesn’t receive an acknowledgment quickly. Consumers must handle duplicates (idempotent processing).
   * **Exactly-Once:** In Kafka, use idempotent producers (`enable.idempotence=true`) plus transactional APIs to ensure no duplicates—more complex setup.
   * **Idempotency:** If a consumer’s operation (e.g., inserting into DB) can run multiple times without changing the final outcome, you avoid data corruption. Common techniques include checking a unique event ID before writing or using `INSERT ... ON CONFLICT DO NOTHING`.

5. **Partitioning & Consumer Groups: How a Key Maps to a Partition in Kafka and How Consumer Groups Distribute Work**

   * **Partitioning:** If you specify a key when producing, Kafka hashes that key (e.g., `userId`) and modulates by partition count to pick a partition: `hash(key) % numPartitions`. Messages with the same key always go to the same partition (ensuring order).
   * **Consumer Groups:** All consumers sharing the same `group.id` coordinate so that each partition is consumed by only one consumer in the group. If you have 3 partitions and 3 consumers in a group, each consumer gets one partition. If you add a 4th consumer, one consumer will be idle.

6. **Serialization Formats: Why JSON or Avro Are Used, and Basic Pros/Cons**

   * **JSON:** Human-readable, flexible (no strict schema), but larger payloads and slower to parse. Good for debugging and low-throughput use cases.
   * **Avro:** Binary format with a schema stored in Schema Registry. Smaller, faster, and enforces a schema at compile time. Supports backward/forward compatibility rules in the registry. Ideal for high-volume pipelines.

7. **Dead-Letter Queues: What They Are and Why You Would Route Failed Messages There**

   * **DLQ Purpose:** If a consumer repeatedly fails to process a message (e.g., invalid format or downstream service down), after a configured number of retries it’s moved to a DLQ topic. This prevents the entire consumer from being stuck on that one bad message.
   * **Operational Workflow:**

     1. Consumer reads message.
     2. Processing fails; service retries a fixed number of times with backoff.
     3. After max retries, consumer produces the same message to `topic-name-DLQ` (with metadata about the error).
     4. Operators inspect DLQ regularly to fix or reprocess bad messages.

8. **Monitoring Lag: How to Detect If Consumers Are Falling Behind and Why It’s Critical**

   * **Consumer Lag Metric:**

     * Lag = (Latest offset in partition) − (Committed offset by consumer).
     * If lag grows unbounded, consumers aren’t keeping up with producers, leading to delays in downstream processing.
   * **Prometheus Exporter:** Use a Kafka exporter that exposes `kafka_consumergroup_current_offset` and `kafka_consumergroup_committed_offset` metrics; alert if lag > threshold.
   * **Why Critical:** High lag can mean stale data driving business logic (e.g., stale inventory data), missed SLAs, or buffers filling up and possibly data loss if retention policies expire.

---

## 4. Database & Data Access

1. **Relational Modeling Basics: Primary/Foreign Keys and the Concept of Normalized Tables**

   * **Primary Key (PK):** Unique identifier for each row (e.g., `user_id`). Generally numeric or UUID.
   * **Foreign Key (FK):** A column (or group) in one table that references a PK in another table, enforcing referential integrity (e.g., `orders.user_id` references `users.user_id`).
   * **Normalization:** Organizing tables to reduce redundancy:

     * **1NF:** Eliminate repeating groups; each column holds atomic values.
     * **2NF:** Remove partial dependencies—every non-key column depends on the entire primary key.
     * **3NF:** Remove transitive dependencies—non-key columns depend only on the primary key.
   * Normalized design avoids update anomalies but can require joins that impact performance.

2. **SQL CRUD & Joins: Writing Simple SELECT, INSERT, UPDATE, DELETE, and INNER JOIN Queries**

   * **SELECT Example:**

     ```sql
     SELECT id, name, email  
     FROM users  
     WHERE status = 'ACTIVE';
     ```
   * **INSERT Example:**

     ```sql
     INSERT INTO users (name, email, status)  
     VALUES ('Alice', 'alice@example.com', 'ACTIVE');
     ```
   * **UPDATE Example:**

     ```sql
     UPDATE users  
     SET status = 'INACTIVE'  
     WHERE last_login < '2024-01-01';
     ```
   * **DELETE Example:**

     ```sql
     DELETE FROM sessions  
     WHERE expires_at < NOW();
     ```
   * **INNER JOIN Example:**

     ```sql
     SELECT o.id AS order_id, u.name AS customer_name  
     FROM orders o  
     INNER JOIN users u ON o.user_id = u.id  
     WHERE o.status = 'PENDING';
     ```

3. **Transaction Management: ACID Properties, commit() vs. rollback(), and Isolation Levels (e.g., READ\_COMMITTED)**

   * **ACID:**

     * **Atomicity:** All operations in a transaction succeed or none do.
     * **Consistency:** DB constraints (FK, unique) are preserved after transaction.
     * **Isolation:** Concurrent transactions don’t interfere; depends on isolation level.
     * **Durability:** Once committed, data persists even on crash.
   * **commit() vs. rollback():**

     * `commit()` permanently saves all changes.
     * `rollback()` undoes all changes since the last commit, leaving the DB in its previous state.
   * **Isolation Levels:**

     * **READ\_UNCOMMITTED:** Dirty reads allowed (poor consistency).
     * **READ\_COMMITTED:** Prevents dirty reads; only committed data is visible.
     * **REPEATABLE\_READ:** Prevents nonrepeatable reads; phantom reads still possible.
     * **SERIALIZABLE:** Full isolation; transactions appear as if executed serially, highest overhead.

4. **JDBC vs. ORM: When to Use Plain JdbcTemplate/JDBC and When to Use JPA/Hibernate, Plus Basic Annotations (@Entity, @Table, @Id)**

   * **JDBC/JdbcTemplate:**

     * Write raw SQL queries.
     * Pros: Fine-grained control, predictable performance.
     * Cons: Boilerplate code for mapping rows to objects.
     * Use when you need highly optimized queries or complex joins that aren’t easy in an ORM.
   * **JPA/Hibernate:**

     * Annotate POJOs with `@Entity` (marks as table), `@Table(name="users")`, and `@Id` (primary key).
     * Pros: Automatic mapping, caching, lazy loading.
     * Cons: Potential for unexpected queries (N+1), overhead if misconfigured.
     * Use when you want to model domain entities and let the framework handle basic CRUD.

5. **Query Methods in Spring Data JPA: How Method Names Like findByUsername Translate into SQL**

   * **Naming Convention:**

     * `User findByEmail(String email)` generates `SELECT * FROM user WHERE email = ?`.
     * `List<Order> findByStatusAndCreatedAtAfter(String status, LocalDateTime date)` → `WHERE status = ? AND created_at > ?`.
   * **Keywords:** Supports `And`, `Or`, `Between`, `LessThan`, `GreaterThan`, `Like`, `OrderBy`, `Distinct`, etc.
   * **Limitations:** Complex queries may need `@Query("... JPQL ...")` or Criteria API if method name gets unwieldy.

6. **Lazy vs. Eager Fetching: The N+1 Problem and How to Avoid It with JOIN FETCH or Proper Fetch Type**

   * **Lazy (default for @OneToMany, @ManyToMany):** Associated entities load only when accessed. If you iterate over a list of users and call `user.getOrders()`, each call may trigger a separate query (N+1).
   * **Eager:** Loads associated entities immediately with parent. E.g., `@ManyToOne(fetch=FetchType.EAGER)` fetches related data in the same query or via a join. Can retrieve too much data upfront.
   * **JOIN FETCH in JPQL:**

     ```java
     @Query("SELECT u FROM User u JOIN FETCH u.orders WHERE u.id = :id")  
     User findByIdWithOrders(@Param("id") Long id);
     ```

     Forces Hibernate to fetch orders in the same query, avoiding multiple round trips.

7. **Connection Pooling Basics: Why a Pool (e.g., HikariCP) Matters and How to Configure Min/Max Pool Size**

   * **Why Pool?** Creating a new DB connection is expensive (handshake, authentication). A pool reuses connections to reduce latency.
   * **HikariCP:** The default in Spring Boot. Very high performance. Key settings:

     * `spring.datasource.hikari.maximum-pool-size=20`: Maximum simultaneous connections.
     * `spring.datasource.hikari.minimum-idle=5`: Minimum idle connections to keep alive.
     * `spring.datasource.hikari.connection-timeout=30000`: Max milliseconds to wait for a connection from the pool before timing out.
   * **Monitoring:** Hikari exposes metrics (`hikaricp.connections.active`) that you can monitor via Micrometer.

8. **Database Migrations: The Role of Flyway or Liquibase for Versioning Schema Changes**

   * **Flyway:**

     * Place SQL scripts in `db/migration` named `V1__init.sql`, `V2__add_users_table.sql`.
     * On application startup, Flyway scans that folder, checks which scripts have been applied (in a `flyway_schema_history` table), and runs any new ones in order.
   * **Liquibase:**

     * Define changesets in XML/YAML/JSON (e.g., `<changeSet id="1" author="dev"> <createTable tableName="users">...</createTable> </changeSet>`).
     * Liquibase tracks executed changesets in `DATABASECHANGELOG` table.
   * **Benefits:** Ensures all environments (dev, test, prod) have the same schema version. Rollback scripts can undo changes if needed.

---

## 5. Observability & Monitoring

1. **Three Pillars Overview: Metrics (Numeric), Logs (Text/JSON), and Traces (Span-Based)**

   * **Metrics:** Represent aggregated numeric data over time (e.g., “250 requests/minute,” “heapMemoryUsed bytes”). They are stored as time-series and answer “how many” or “how long.”
   * **Logs:** Textual or structured entries that record discrete events (“User 123 logged in,” “NullPointerException at line 45”). They answer “what happened” and include rich context (timestamps, stack traces).
   * **Traces:** A trace shows the end-to-end path of a single request across services. It’s composed of spans: each span represents one unit of work (e.g., “DB query,” “HTTP call to Inventory Service”). Spans have a traceId to link them together. Traces answer “where time was spent.”

2. **Spring Boot Actuator + Micrometer: Exposing /actuator/prometheus for Basic JVM and HTTP Request Metrics**

   * **Add Dependencies:**

     ```xml
     <dependency>
       <groupId>io.micrometer</groupId>
       <artifactId>micrometer-registry-prometheus</artifactId>
     </dependency>
     <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-actuator</artifactId>
     </dependency>
     ```
   * **application.properties:**

     ```
     management.endpoints.web.exposure.include=health,metrics,prometheus
     management.endpoint.prometheus.enabled=true
     ```
   * **What /actuator/prometheus Provides:**

     * JVM metrics: `jvm_memory_used_bytes`, `jvm_gc_pause_seconds`.
     * HTTP server metrics: `http_server_requests_seconds_count{method="GET",uri="/api/hello",status="200"}`.
   * **Micrometer Tags:** You can annotate methods with `@Timed("my.method.timer")` so that Micrometer creates a timer metric automatically.

3. **Prometheus Fundamentals: Scrape Configs, Endpoints, and Why Pull-Based Monitoring Is Common**

   * **Scrape Config:**

     ```yaml
     scrape_configs:
       - job_name: 'my-service'
         metrics_path: '/actuator/prometheus'
         static_configs:
           - targets: ['localhost:8080']
     ```
   * **Why Pull Model:** Prometheus server periodically “scrapes” (pulls) metrics from each service. This ensures a single source of truth for collection intervals and simplifies service discovery (e.g., via Kubernetes service discovery).
   * **Time-Series Database (TSDB):** Prometheus stores scraped metrics in a local TSDB. You can query them via PromQL to build graphs or alerts.

4. **Grafana Basics: Adding Prometheus as a Data Source and Creating a Simple Dashboard Panel (e.g., HTTP Request Rate)**

   * **Add Data Source:**

     1. Go to Grafana UI → Configuration → Data Sources → Add data source → Prometheus.
     2. Enter Prometheus URL (e.g., `http://prometheus:9090`) and click “Save & Test.”
   * **Create a Dashboard:**

     1. * → Dashboard → Add new panel.
     2. In “Query,” select Prometheus and enter `rate(http_server_requests_seconds_count[1m])` to show requests per second.
     3. Choose “Time series” visualization; give panel a title like “Requests/sec.”
   * **Templating (Optional at interview level):** Create variables (e.g., `${service}`) to switch between multiple services on one dashboard.

5. **Structured Logging: Configuring Logback to Emit JSON Logs that Include Timestamp, Log Level, and a Request ID**

   * **Add Dependency:**

     ```xml
     <dependency>
       <groupId>net.logstash.logback</groupId>
       <artifactId>logstash-logback-encoder</artifactId>
       <version>7.4</version>
     </dependency>
     ```
   * **logback-spring.xml Example:**

     ```xml
     <configuration>
       <appender name="JSON_CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
         <encoder class="net.logstash.logback.encoder.LogstashEncoder">
           <includeContext>true</includeContext>
           <fields>
             <field name="app" value="order-service" />
           </fields>
         </encoder>
       </appender>
       <root level="INFO">
         <appender-ref ref="JSON_CONSOLE"/>
       </root>
     </configuration>
     ```
   * **Request ID Propagation:** Use Sleuth or a filter to generate a `X-Request-ID` header and include it in each log line via `%X{X-Request-ID}` in the pattern. This lets you tie logs to a particular request.

6. **Logstash Pipeline (High-Level): How Logstash Ingests JSON Logs Over TCP/UDP and Pushes Them into Elasticsearch**

   * **Input Section:**

     ```conf
     input {
       tcp {
         port => 5000
         codec => json
       }
     }
     ```

     Listens on TCP 5000 for JSON-encoded log lines.
   * **Filter Section (Optional):**

     ```conf
     filter {
       date {
         match => [ "timestamp", "ISO8601" ]
       }
     }
     ```

     Parses the `timestamp` field into Elasticsearch’s `@timestamp`.
   * **Output Section:**

     ```conf
     output {
       elasticsearch {
         hosts => ["elasticsearch:9200"]
         index => "app-logs-%{+YYYY.MM.dd}"
       }
     }
     ```

     Sends parsed events into Elasticsearch under daily indices. Kibana can then visualize and search logs.

7. **Distributed Tracing with Sleuth + Zipkin: Auto-Instrumentation of HTTP Calls, Propagating traceId/spanId**

   * **Add Dependencies:**

     ```xml
     <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-sleuth</artifactId>
     </dependency>
     <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-sleuth-zipkin</artifactId>
     </dependency>
     ```
   * **Configuration (application.properties):**

     ```
     spring.zipkin.base-url=http://localhost:9411
     spring.sleuth.sampler.probability=1.0
     ```

     Sends all spans to a Zipkin server at `localhost:9411`.
   * **What Happens Under the Hood:**

     * Every incoming HTTP request gets a new `traceId`.
     * Outgoing RestTemplate or WebClient calls automatically include `X-B3-TraceId` and `X-B3-SpanId` headers.
     * Zipkin UI shows a timeline of spans across services, letting you identify which service is slow.

8. **Correlating Logs & Traces: Including traceId in Every Log Line So You Can Filter Kibana by That ID**

   * **Sleuth Injects traceId/spanId into MDC:** Logback’s encoder can reference `%X{traceId}` and `%X{spanId}` to include these in JSON fields.
   * **Kibana Search Example:** In Kibana’s Discover tab, set filter `traceId:"abcd1234ef56"`. All logs tagged with that `traceId` show up, helping you trace the request’s path.
   * **End-to-End Debugging:** If a request is slow, you:

     1. View the trace in Zipkin to see which service or span took longest.
     2. Note the `traceId` and search Kibana for log entries with that same ID to see detailed error messages or warnings.

---

## 6. Caching & Performance Optimization

1. **Cache-Aside Pattern: Check Cache First, Fallback to DB, Then Populate Cache; Use @Cacheable in Spring**

   * **Basic Flow:**

     1. Method call annotated with `@Cacheable("users")`: Spring checks Redis (or configured cache) for key `users::123`.
     2. If present (cache hit), return value immediately—no DB call.
     3. If absent (cache miss), execute method logic (e.g., `userRepository.findById(123)`), then store result in cache under that key.
   * **Code Example:**

     ```java
     @Cacheable(cacheNames = "users", key = "#userId")
     public User getUser(Long userId) {
         return userRepository.findById(userId).orElse(null);
     }
     ```
   * **Why It Helps:** Reduces database load for frequently accessed data; subsequent reads are served from fast in-memory store.

2. **TTL & Eviction: Why Setting a Time-To-Live Is Important to Prevent Stale Data**

   * **TTL (Time-To-Live):** Cache entries expire automatically after a specified duration (e.g., 10 minutes). Prevents serving outdated information if the underlying DB row changes.
   * **Configuration Example (Redis in Spring):**

     ```java
     @Bean
     public RedisCacheManager cacheManager(RedisConnectionFactory factory) {
         RedisCacheConfiguration config = RedisCacheConfiguration.defaultCacheConfig()
             .entryTtl(Duration.ofMinutes(10));
         return RedisCacheManager.builder(factory).cacheDefaults(config).build();
     }
     ```
   * **Eviction Policies:** If the cache is full or reaches max size, entries are removed based on policy (e.g., LRU—least recently used). TTL ensures eventual consistency with the source of truth.

3. **Redis Basics: Storing Simple Key–Value Pairs, Using GET/SET, and Common Data Structures (Strings, Hashes)**

   * **Core Commands:**

     * `SET user:123 {"id":123,"name":"Alice"}` stores a JSON string.
     * `GET user:123` retrieves it.
   * **Hashes:** Ideal for storing object fields without serializing entire JSON:

     ```shell
     HSET user:123 id "123" name "Alice"
     HGETALL user:123  # returns all fields
     ```
   * **Other Structures (Not Must-Know):** Lists, Sets, Sorted Sets exist, but a simple String or Hash is often sufficient for basic caching.

4. **Local In-Memory Caches: When to Use Ehcache or Caffeine for Simple, Single-Node Caching**

   * **Ehcache Example:**

     ```xml
     <cache alias="users">
       <heap unit="entries">1000</heap>
       <expiry>
         <ttl unit="minutes">10</ttl>
       </expiry>
     </cache>
     ```

     Add `<dependency>` for `org.ehcache:ehcache`.
   * **Caffeine Example:**

     ```java
     Caffeine.newBuilder()
             .maximumSize(500)
             .expireAfterWrite(10, TimeUnit.MINUTES)
             .build();
     ```
   * **When to Choose:** If your application runs on a single node or you don’t need distributed caching, in-memory caches are simpler and avoid network overhead. But they won’t share data across instances.

5. **Cache Key Design: Choosing Meaningful, Concise Keys (e.g., user:123) and Avoiding Large Composite Keys**

   * **Key Format:** Always prefix keys with a logical namespace (e.g., `user:123`, `product:456`). This avoids collisions and makes operations like “flush all user entries” easier (e.g., `DEL user:*`).
   * **Avoid Overly Complex Keys:** Don’t include entire objects or large JSON as a key—just use the unique identifier.
   * **Consistency:** Make sure your code uses the same key-building logic everywhere (e.g., a method `buildUserCacheKey(Long userId)` that always returns `user:<id>`).

6. **Connection Pool Tuning: Basic HikariCP Settings (maxPoolSize, connectionTimeout) to Prevent DB Exhaustion**

   * **Key Settings in application.properties:**

     ```
     spring.datasource.hikari.maximum-pool-size=20  
     spring.datasource.hikari.connection-timeout=30000  
     spring.datasource.hikari.idle-timeout=600000  
     spring.datasource.hikari.minimum-idle=5
     ```
   * **What They Mean:**

     * **maximum-pool-size:** Maximum number of simultaneous connections in the pool. If all are in use, further requests wait up to `connection-timeout` ms before failing.
     * **connection-timeout:** How long to wait for a connection before throwing an error.
     * **idle-timeout:** How long a connection can sit idle before the pool closes it.
   * **Monitoring:** Expose Hikari metrics through Micrometer (e.g., `hikaricp.connections.active`, `hikaricp.connections.idle`) to ensure you aren’t leaking connections.

7. **Profiling Essentials: How to Take a Simple Heap or CPU Snapshot in VisualVM to Spot Bottlenecks**

   * **VisualVM Usage:**

     1. Launch VisualVM (bundled with JDK or download separately).
     2. Under “Local,” find your running Java process, double-click to open.
     3. Go to the “Sampler” tab. Choose CPU or Memory. Click “Start.”
     4. Exercise your application (e.g., hit an endpoint). VisualVM shows which methods consume most CPU or where objects pile up on the heap.
   * **When to Use:** If your application feels slow or runs out of memory, a quick VisualVM profile can highlight hotspots (e.g., a tight loop, a huge data structure).

8. **SQL Query Optimization: Using EXPLAIN to Check If an Index Is Being Used, and Adding an Index to Speed Up Joins**

   * **EXPLAIN (PostgreSQL/ MySQL):**

     ```sql
     EXPLAIN SELECT * FROM orders o  
     JOIN users u ON o.user_id = u.id  
     WHERE u.email = 'alice@example.com';
     ```

     The output shows whether it uses a sequential scan (slow for large tables) or an index scan.
   * **Creating an Index:**

     ```sql
     CREATE INDEX idx_users_email ON users(email);
     ```

     Now queries filtering `users.email = ...` can use `idx_users_email` to find rows quickly.
   * **Why It Matters:** Table scans on large tables can be thousands of times slower than index scans. Always check `EXPLAIN` for slow queries.

---

## 7. Security & Access Control

1. **Authentication vs. Authorization: JWT Flow Basics—Creating a Token on Login and Verifying It on Each Request**

   * **Authentication (Login):**

     1. Client sends credentials (`username`/`password`) to an auth endpoint.
     2. Server validates credentials, creates a JWT containing claims (e.g., `sub=user123`, `roles=["USER"]`), signs it with a secret or private key, and returns it.
   * **Authorization (Subsequent Requests):**

     1. Client includes `Authorization: Bearer <JWT>` header in HTTP requests.
     2. Server verifies the JWT signature and expiry, extracts claims, and checks if the user’s roles allow the requested action (e.g., `hasRole("ADMIN")`).
   * **JWT Structure:** Header (algorithm info), payload (claims), signature. Common libraries (e.g., `jjwt`) handle generation and verification.

2. **Spring Security Config: Securing All Endpoints by Default, Permitting /login or /signup, and Requiring Role Checks (hasRole("USER"))**

   * **Default Behavior:** With `spring-boot-starter-security` on the classpath and no custom config, all endpoints (except `/error`) require authentication via HTTP Basic.
   * **Custom Securing Example:**

     ```java
     @Configuration
     public class SecurityConfig {
         @Bean
         public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
             http
               .csrf().disable()
               .authorizeRequests()
                 .antMatchers("/login", "/signup").permitAll()
                 .antMatchers("/user/**").hasRole("USER")
                 .antMatchers("/admin/**").hasRole("ADMIN")
                 .anyRequest().authenticated()
               .and()
                 .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
               .and()
                 .addFilter(new JwtAuthenticationFilter(authenticationManager()))
                 .addFilter(new JwtAuthorizationFilter(authenticationManager()));
             return http.build();
         }
     }
     ```
   * **Role Prefix:** By default, Spring Security expects roles to be prefixed with `ROLE_`. So `hasRole("USER")` checks for authority `ROLE_USER`.

3. **Password Encoding: Why You Must Store Passwords with BCryptPasswordEncoder Instead of Plain Text**

   * **BCrypt Strengths:**

     * Salted automatically—prevents rainbow table attacks.
     * Adaptive work factor: You can increase the strength over time as hardware improves.
   * **Example Usage:**

     ```java
     @Bean
     public PasswordEncoder passwordEncoder() {
         return new BCryptPasswordEncoder(10); // strength 10
     }
     ```

     Then, when saving a new user:

     ```java
     String hashed = passwordEncoder.encode(plainPassword);
     user.setPassword(hashed);
     userRepository.save(user);
     ```
   * **Verification:** `passwordEncoder.matches(enteredPassword, storedHash)` returns `true` if they match. Never store or log the plain password.

4. **CSRF for Browser Apps: When to Keep CSRF Enabled and When to Disable It for Stateless REST APIs**

   * **CSRF Attack:** A malicious site can cause a user’s browser to submit requests (e.g., a hidden POST form) to your site using the user’s credentials (cookies).
   * **CSRF Token:** The server sends a token in the HTML form or a cookie. The client must include that token in a header or hidden field; the server verifies it.
   * **When to Disable:** If your API is strictly stateless and uses JWT (no cookies), CSRF is not needed because the browser does not automatically send JWT. In Spring Security config:

     ```java
     http.csrf().disable();
     ```
   * **When to Keep:** If your app uses sessions and cookies for authentication (traditional web app), you should keep CSRF protection enabled.

5. **CORS Configuration: Allowing Specific Origins, Methods, and Headers via @CrossOrigin or Global Config**

   * **Global Configuration Example:**

     ```java
     @Configuration
     public class CorsConfig implements WebMvcConfigurer {
         @Override
         public void addCorsMappings(CorsRegistry registry) {
             registry.addMapping("/**")
                     .allowedOrigins("https://frontend.example.com")
                     .allowedMethods("GET", "POST", "PUT", "DELETE")
                     .allowedHeaders("Authorization", "Content-Type")
                     .allowCredentials(true);
         }
     }
     ```
   * **Controller-Level Example:**

     ```java
     @RestController
     @RequestMapping("/api")
     public class ApiController {
         @CrossOrigin(origins = "https://frontend.example.com")
         @GetMapping("/data")
         public Data getData() { … }
     }
     ```
   * **Preflight Requests:** The browser sends an `OPTIONS` request to check if CORS is allowed. The server must respond with `Access-Control-Allow-Methods`, `Access-Control-Allow-Origins`, and `Access-Control-Allow-Headers`.

6. **Method-Level Security: Using @PreAuthorize("hasRole('ADMIN')") to Lock Down Service Methods**

   * **Enable Global Method Security:** Add `@EnableGlobalMethodSecurity(prePostEnabled = true)` to a config class.
   * **Usage Example:**

     ```java
     @Service
     public class OrderService {
         @PreAuthorize("hasRole('ADMIN')")
         public void deleteAllOrders() { … }
     }
     ```
   * **How It Works:** Before invoking `deleteAllOrders()`, Spring evaluates the SpEL expression `hasRole('ADMIN')` against the current user’s authorities. If false, a 403 Forbidden is returned.

7. **Secure HTTP Headers: Enabling HSTS and X-Content-Type-Options: nosniff to Harden Web Responses**

   * **HSTS (Strict-Transport-Security):**

     * Instructs browsers to only use HTTPS for your domain for a given period.
     * Example header: `Strict-Transport-Security: max-age=31536000; includeSubDomains`.
     * In Spring Boot, add:

       ```java
       http.headers()
           .httpStrictTransportSecurity()
           .maxAgeInSeconds(31536000)
           .includeSubDomains(true);
       ```
   * **X-Content-Type-Options: nosniff:** Prevents the browser from guessing MIME types (e.g., treating a .txt file as .html). In Spring Security:

     ```java
     http.headers()
         .contentTypeOptions();
     ```

8. **Basic OAuth2 Concepts: Difference Between Authorization Code and Client Credentials Flows, and When Each Is Used**

   * **Authorization Code Flow:**

     * Used by web or mobile applications on behalf of a user.
     * Steps:

       1. Redirect user to Auth Server’s `/authorize?response_type=code&client_id=...&redirect_uri=...`.
       2. User authenticates and consents; Auth Server redirects back with `code`.
       3. Client exchanges `code` + `client_secret` at `/token` endpoint for `access_token` and `refresh_token`.
   * **Client Credentials Flow:**

     * Used for machine-to-machine (M2M) calls without user context.
     * Client sends `client_id` and `client_secret` to `/token` with `grant_type=client_credentials`, gets an `access_token` representing the application itself.
   * **When to Use:**

     * **Auth Code:** When you need user identity and delegated permissions (e.g., “Alice” uses an app to access her data).
     * **Client Credentials:** When service A calls service B in the backend to perform tasks (no user involved).

---

## 8. Cloud & AWS Services

1. **AWS Shared Responsibility Model: What AWS Secures vs. What You Must Secure (IAM Policies, VPC)**

   * **AWS Responsibility (“Security of the Cloud”):** Physical security of data centers, network infrastructure, hypervisor, foundational services.
   * **Customer Responsibility (“Security in the Cloud”):** Everything you deploy or configure: OS patches, application security, identity and access management (IAM), network configuration (VPC, Security Groups), data encryption.
   * **Practical Implications:** Even though AWS encrypts data at rest for S3 by default, you still need to configure proper S3 bucket policies and KMS key management. AWS doesn’t automatically prevent you from making a bucket public; that’s your responsibility.

2. **IAM Basics: Creating a Role for an EC2 Instance and Attaching an S3 “ReadOnly” Policy—Principle of Least Privilege**

   * **Role vs. User vs. Group:**

     * **User:** Represents a human or service account with long-term credentials.
     * **Role:** AWS resource (EC2, Lambda) or IAM user temporarily assumes the role to get permissions via temporary credentials.
     * **Group:** A collection of users with shared policies.
   * **Creating a Role for EC2:**

     1. In AWS Console, go to IAM → Roles → Create role → AWS service → EC2.
     2. Attach AWS managed policy `AmazonS3ReadOnlyAccess`.
     3. Launch EC2 instance with this role.
   * **Why Least Privilege:** If your instance only needs to read from a bucket, don’t give full S3 or DynamoDB access. This limits blast radius if credentials are compromised.

3. **S3 Fundamental Operations: Uploading/Downloading an Object and Setting Bucket Permissions to Avoid Public Access**

   * **Uploading via Console:** Drag-and-drop a file into S3 bucket. Click the file, choose “Copy URL,” and note whether it’s public or private.
   * **Uploading via AWS CLI:**

     ```bash
     aws s3 cp localfile.txt s3://my-bucket/my-key.txt
     ```
   * **Downloading via CLI:**

     ```bash
     aws s3 cp s3://my-bucket/my-key.txt ./localfile.txt
     ```
   * **Bucket Permissions:**

     * In bucket’s “Permissions” tab, ensure “Block all public access” is checked.
     * Avoid setting a bucket policy that allows `"Principal": "*"`, `"Action": "s3:GetObject"`, unless you truly want a public website.

4. **Lambda + API Gateway: Simple Function Triggered by an HTTP GET Request; Understanding Cold Starts and Timeouts**

   * **Creating a Lambda Function (Console):**

     1. Go to Lambda → Create function → Author from scratch.
     2. Choose a runtime (e.g., Java 11), configure handler (e.g., `com.example.Handler::handleRequest`).
   * **Connecting to API Gateway:**

     1. Create a new HTTP API (v2) or REST API (v1).
     2. Add an integration pointing to your Lambda function.
     3. Deploy to a stage (`prod`) and note the endpoint URL.
   * **Cold Start:** The first invocation of a Lambda after being idle causes AWS to spin up a fresh container and load your code. In Java, this can take hundreds of milliseconds. Subsequent invocations “warm” the container, running faster.
   * **Timeouts:** Default is 3 seconds; you can extend up to 15 minutes. Important to keep short for synchronous endpoints (`200–300ms`) unless you have a known long-running process.

5. **DynamoDB Key Design: Partition Key vs. Composite Key and Why You Choose One Over the Other**

   * **Partition Key Only (HASH):** One attribute serves as the primary key (e.g., `userId`). Queries are simply `GetItem(Key: userId)`. Ideal when you always fetch by that single attribute.
   * **Composite Primary Key (HASH + RANGE):** Use partition key (e.g., `userId`) and sort key (e.g., `orderDate`). Allows range queries like “all orders for user 123 between Jan and Feb.”
   * **Choosing Strategy:**

     * If you have simple key-value lookups, partition key alone is enough.
     * If you need to query by a range or ordering, add a sort key.
   * **Scaling Considerations:** Each partition can handle a certain throughput. Design partition keys so that requests distribute evenly (high cardinality). Avoid “hot” keys.

6. **CloudFormation vs. Terraform Overview: Why IaC Matters; Recognizing a Basic S3 Bucket Resource in YAML or HCL**

   * **Why IaC:**

     * Ensures repeatable, version-controlled infrastructure deployments.
     * Avoids manual console steps that may differ across environments.
   * **CloudFormation (YAML) Example:**

     ```yaml
     Resources:
       MyBucket:
         Type: AWS::S3::Bucket
         Properties:
           BucketName: my-demo-bucket
     ```

     Apply with `aws cloudformation deploy --template-file template.yaml --stack-name demo-stack`.
   * **Terraform (HCL) Example:**

     ```hcl
     resource "aws_s3_bucket" "demo" {
       bucket = "my-demo-bucket"
       acl    = "private"
     }
     ```

     Apply with `terraform init && terraform apply`.
   * **Key Difference:** CloudFormation is AWS-native; Terraform is multi-cloud and has its own state file. Both track resource drift and can update existing infrastructure.

7. **CloudWatch Monitoring: Setting Up a CPUUtilization Alarm on an EC2 Instance That Sends SNS Notifications**

   * **Metric to Monitor:** `CPUUtilization` (percentage of CPU in use).
   * **Alarm Creation (Console):**

     1. Navigate to CloudWatch → Alarms → Create alarm.
     2. Select “EC2 Metrics” → “Per-Instance Metrics” → Choose your instance → CPUUtilization.
     3. Set threshold (e.g., CPU > 80% for 5 consecutive 1-minute periods).
     4. Choose an SNS topic (or create one) for notifications (email or SMS).
   * **Why It’s Important:** Early detection of high CPU usage helps you scale out or investigate runaway processes before user experience suffers.

8. **ECS vs. EKS Choice Factors: When to Pick Serverless Containers (Fargate/ECS) vs. Full Kubernetes (EKS) Based on Team Expertise and Workload**

   * **ECS (Elastic Container Service):**

     * AWS-managed container orchestration; simpler to set up if you’re already in AWS.
     * You can choose Fargate (serverless, AWS manages nodes) or EC2 launch type (you manage the EC2 instances).
     * Good for small teams or simpler microservice architectures.
   * **EKS (Elastic Kubernetes Service):**

     * Fully managed Kubernetes control plane; you still manage worker nodes (or use managed node groups).
     * Offers the full Kubernetes API ecosystem—Ingress controllers, Helm charts, Operators.
     * Suitable if you already have Kubernetes expertise or need advanced features (like custom scheduling, complex networking).
   * **Key Factors:**

     * **Team Skillset:** Do you know Kubernetes, or is learning curve too steep?
     * **Feature Requirements:** Do you need features like custom CRDs, advanced pod scheduling, or multi-cluster federation?
     * **Operational Overhead:** ECS/Fargate reduces operational tasks; EKS offers more flexibility but requires more maintenance.

---

## 9. Event-Driven Architecture & Pipelines

1. **Event vs. Command Distinction: Why “OrderCreated” (Event) Differs from “CreateOrder” (Command), and How That Affects Coupling**

   * **Command (“CreateOrder”):** Imperative: “Do this action.” The sender expects the system to perform the action (and possibly return a result). Often synchronous or blocking. Tightly couples sender to the receiver’s implementation.
   * **Event (“OrderCreated”):** Declarative: “This happened.” The publisher does not expect any direct response. Consumers subscribe and react independently. This decouples services, because the producer doesn’t know who (or even if) anyone is listening.

2. **Kafka Basics: Creating a Topic, Sending a Message with kafka-console-producer, and Reading It with kafka-console-consumer**

   * **Create Topic:**

     ```bash
     kafka-topics.sh --create \
       --topic orders \
       --bootstrap-server localhost:9092 \
       --partitions 3 \
       --replication-factor 1
     ```
   * **Producer CLI:**

     ```bash
     kafka-console-producer.sh --topic orders --bootstrap-server localhost:9092
     > {"orderId":123,"status":"CREATED"}
     > ^C
     ```
   * **Consumer CLI:**

     ```bash
     kafka-console-consumer.sh --topic orders --bootstrap-server localhost:9092 --from-beginning
     {"orderId":123,"status":"CREATED"}
     ```
   * **Why It Matters:** You can quickly verify connectivity, see messages in real time, and confirm correct serialization.

3. **Consumer Groups: How Multiple Consumers in the Same Group Share Partitions and Achieve Parallelism**

   * **Group ID:** All consumers specifying the same `group.id` coordinate so that each partition in the topic is consumed by exactly one consumer instance in that group.
   * **Example:** Topic “orders” has 3 partitions and ConsumerGroup “order-service-group” has 3 instances. Each instance reads from one partition. If you add a fourth instance, it remains idle until a partition becomes available.
   * **Rebalance:** When a consumer instance joins or leaves the group, Kafka reassigns partitions among active consumers. During rebalance, consumption pauses briefly for that group.

4. **At-Least-Once Delivery: Why Your Consumer Must Be Idempotent to Handle Duplicate Messages**

   * **Producer Retries:** If a producer doesn’t receive an ack (e.g., due to a network glitch), it may resend the same message. This results in duplicates.
   * **Consumer-Side Duplicates:** If a consumer crashes after processing a message but before committing its offset, on restart it will reprocess that same message.
   * **Idempotent Processing:** Writing to DB with `INSERT ... ON CONFLICT DO NOTHING` or checking a unique event ID table before processing ensures duplicates do not produce incorrect state.

5. **Schema Registry Purpose: Using Avro with a Registry So Producers and Consumers Share a Contract and Support Schema Evolution**

   * **Schema Registry:** A centralized repository for Avro (or Protobuf) schemas. Each schema is stored under a subject (usually `<topic>-value`).
   * **Compatibility Rules:**

     * **BACKWARD:** New consumers can read data produced with older schemas.
     * **FORWARD:** Older consumers can read data produced with newer schemas (fields removed are safe).
     * **FULL:** Both backward and forward compatibility.
   * **Producer/Consumer Workflow:**

     1. Producer serializes data to Avro and registers schema in registry if not already present.
     2. Producer embeds schema ID in the message payload.
     3. Consumer retrieves schema by ID, deserializes payload accordingly.
   * **Why It Matters:** Avoids runtime class mismatch errors and allows you to evolve data structures safely over time.

6. **Dead-Letter Queue Pattern: Automatically Routing Failed Messages to a DLQ After Configurable Retries**

   * **Retry Logic Flow:**

     1. Consumer tries to process a message.
     2. If processing fails (e.g., exception), it retries N times with backoff.
     3. After N retries, the consumer publishes the message to a DLQ topic (e.g., `orders-DLQ`) along with error metadata.
     4. Operators can inspect `orders-DLQ` to diagnose and fix malformed or unprocessable messages.
   * **Implementation Tip:** Use a header or wrapper that carries the original offset, timestamp, and failure reason—this context helps debugging.

7. **Simple Saga Example: “ReserveInventory” → “ChargePayment” → “ShipOrder” with Compensating Actions if Billing Fails**

   * **Choreography Style (No Central Coordinator):**

     1. Order Service publishes `OrderCreated`.
     2. Inventory Service consumes, reserves stock, publishes `InventoryReserved`.
     3. Billing Service consumes `InventoryReserved`, attempts charge, publishes `PaymentSuccessful` or `PaymentFailed`.
     4. If `PaymentFailed` arrives, Inventory Service listens and publishes `InventoryReleased`.
     5. Shipping Service listens to `PaymentSuccessful` → `ShipOrder`.
   * **Compensation:** Each service must define how to undo its action: if payment fails, inventory must be released (compensation).
   * **Key Point:** There is no single transaction; each step is its own local transaction, and if later steps fail, you trigger compensating messages.

8. **Monitoring Lag & Throughput: Checking Consumer Lag via Kafka’s Built-In JMX Metrics and Why Low Lag Is Critical for Real-Time Processing**

   * **Lag Metrics Exposed via JMX:**

     * `kafka.consumer:type=consumer-fetch-manager-metrics,client-id=*` → `records-lag-max` gauge for each partition.
     * `kafka.consumer:type=consumer-fetch-manager-metrics,client-id=*` → `records-consumed-total` counter for throughput.
   * **Prometheus Exporter:** Use `jmx_exporter` or `kafka_exporter` to scrape these metrics into Prometheus.
   * **Grafana Panel Example:**

     ```promql
     sum(kafka_consumergroup_current_offset - kafka_consumergroup_committed_offset) by (group)
     ```

     Shows total lag per consumer group.
   * **Why Low Lag Matters:** High lag means your consumer can’t keep up with the data rate. Downstream services relying on that data get stale information, potentially causing stale inventory info or late alerts.

---
