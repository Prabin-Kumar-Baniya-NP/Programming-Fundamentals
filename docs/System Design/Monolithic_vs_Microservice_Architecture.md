# Monolithic Vs Microservice Architecture

## Monolithic Architecture

### Defintion

- Single Codebase
- Tighly Coupled and Shared Memory
- Centralized Database
- Components
    - User Interface (UI)
    - Application Layer (Business Logic)
    - Data Access Layer (ORM)
    - Database (PostgresSQL, MySQL)
    - External Dependency (API Integration)
    - Middleware

- Good for small teams and startups.
- Easy to setup and economical in comparision to distributed system
- Easy to perform End-to-end testing and catch issues and bugs.

### Disadvantages

- A minor change in code requires re-deployment of entire system.
- Limited Scalability - Need to scale even the idle and less used components.
- High resource consumption
- Single Point of Failure

### Scaling Strategy

- Verticle Scaling but has practicle limitations.
- Performance Optimizations
- Caching
- Load Balancing
- Database Sharding

## Microservice Architecture

- Independent deployable service and each service has its own business logics
- Decouples business logics
- Allow best tool for each business problem

### Advantages

- It promotes agility in team work.
- Flexible Scaling for individual services
- Continuos Deployment Cycle
- Highly Maintanable and testable
- High Reliability
- Technology Flexibility

### Disadvantages

- Increased Complexity
- Exponential Infastructure Cost
- Added Organization Overhead
- Debugging Challenges due to distributed logs
- Lack of clear ownership
- Increased latency due to inter-communication between system (think about every network call, serialization, deserialization of data)