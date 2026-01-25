# Task 3: H2 Database Integration

**Duration:** 30-60 mins | **Status:** Completed

![](assets/task-3.png)

## Objective

Integrate Midas Core with an H2 in-memory database to validate and persist financial transactions.

## What I Learned

- How to integrate a SQL database into a Spring Boot application using H2 and Spring Data JPA
- How backend systems validate financial transactions and enforce business rules
- How to model relational data using JPA entities with many-to-one relationships
- How to combine Kafka data ingestion with database persistence

## What I Did

### 1. Added H2 Database Configuration

Updated `application.yml` with H2 and JPA settings:

```yaml
spring:
  datasource:
    url: jdbc:h2:mem:midasdb
    driver-class-name: org.h2.Driver
  jpa:
    hibernate:
      ddl-auto: create-drop
```

### 2. Created TransactionRecord Entity

Created JPA entity with many-to-one relationships to sender and recipient users:

```java
@Entity
public class TransactionRecord {
    @Id
    @GeneratedValue
    private long id;

    @ManyToOne
    @JoinColumn(name = "sender_id", nullable = false)
    private UserRecord sender;

    @ManyToOne
    @JoinColumn(name = "recipient_id", nullable = false)
    private UserRecord recipient;

    @Column(nullable = false)
    private float amount;
}
```

### 3. Implemented Transaction Validation

Created `TransactionService` with validation logic:

- Sender ID must be valid
- Recipient ID must be valid
- Sender balance must be >= transaction amount

### 4. Updated Balance Management

Valid transactions update both sender and recipient balances before persisting.

## Quiz Answer

**Q: What is the balance of the "waldorf" user after all transactions are processed (rounded down)?**

**A: 627**

## Pull Request

[PR #3: feat(task-3): add H2 database integration with transaction validation](https://github.com/iamanjali1003/forage-midas/pull/3)

## Skills Practiced

- SQL Database (H2)
- Spring Data JPA
- Java Programming
- Transaction Validation
