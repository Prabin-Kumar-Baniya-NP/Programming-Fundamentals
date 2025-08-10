# Basics of System Design

- System Design is the process of defining architecture, components, modules, interfaces and data for system to satisfy the requirements.

## Requirement Analysis

### Functional Requirement
- What system should do !
- Defines action.
- Directly Visible and Testable
- Example: User should login using username and password, User should be able to order and make payment in app.

### Non Functional Requirement
- How well the system should perform !
- Define constraint under which that action should happen.
- Portablity, Scalablity, Security, Maintanable, Quality.
- Example: User should get response within 2 seconds, App should respond well when high traffic is received.

## System Design Life Cycle

- The SDLC is typically divided into seven phases: 
    - Planning
    - Feasibility Study
    - System Design
    - Implementation
    - Testing
    - Deployment
    - Maintenance and Support

### Different working models in SDLC

- The Waterfall Model is a linear and sequential model used in the System Design Life Cycle (SDLC). In this model, each phase of development must be completed before moving on to the next. It is considered a straightforward approach, though it can be inflexible when faced with changing requirements.

- The Iterative Model is a software development approach within the System Design Life Cycle (SDLC) characterized by repeating cycles. In this model, the system is refined and improved through each iteration based on feedback.

- The Prototyping Model is a model used in the System Design Life Cycle (SDLC). This model involves building a prototype, which is a preliminary version of the system, to gather feedback and refine the design before the final product is built.

- The Spiral Model is a model used in the System Design Life Cycle (SDLC) that incorporates elements from both the iterative and prototyping models. It operates through cycles of planning, designing, constructing, and evaluating.

- The Agile Model is a model used in the System Design Life Cycle (SDLC) that emphasizes flexibility and collaboration, utilizing frequent iterations and continuous feedback. It is particularly well-suited for projects where requirements may evolve.


### Components of System Design

1. Load Balancers
    - Distribute incoming requests to best available servers based on the configurations.
    - Example:
        - Global load balancers (for distributed systems across geographic regions)
        - Application load balancers (specialized for specific application types like HTTP/HTTPS).

2. Caching
    - Temporarily storing frequently access data to speed up the retrieval.

3. Content Delivery Network
    - When a user requests content, a nearby CDN server handles the request with a cached copy, reducing the data travel distance and speeding up load times
    - Serving static files(images/js/css) through cdn.

4. API Gateways

    - Traffic Controller for multiple backend services in microservice architecture.
    - It also handles authentication, authorization, security, rate limiting and much more.

5. Rate Limiting
    - Limits number of request which a user can make in a ceratin time period.
    - Strategy:
        - Request rate limiters: These are used to limit the total number of requests that a system or application processes within a given time period.
        - User rate limiters: This strategy focuses on limiting the rate at which a specific user or group of users can make requests to a system or application.
        - Token bucket rate limiters: This method limits the rate at which requests are processed by a system. It functions by allowing a certain number of requests to be processed in each time period, while any excess requests are held in a "bucket" until the next time period.


## Data Storage Strategy

### Key Value Store

- Its a type of NOSQL Database.
- Many caching system uses in-memory key value store to store data.
- Its horizontally scalable.
- Less suitable for complex relationship betwen data.

### Blob Storage

- BLOB Full Form: Binary Large Object
- Its a object storage.
- Stores unstructured data like video, audio files.
- Example: S3, Azure Blob Storage

### Database System
- RDMS like Postgres, MySQL

### Distributed Database System
- Database is stored in multiple nodes and servers.

## Monitoring System

- Collect, track and monitor the system and their performance.
- Systems:
    - Network monitoring systems: These are used to monitor the performance of a network and its components, such as routers, switches, and servers.
    - System monitoring systems: These monitor the performance of a computer system and its components, including CPU, memory, and disk usage.
    - Application monitoring systems: These are used to monitor the performance of specific applications or services, like web servers or databases.
- Example: Grafana

## Logging System

- Collect, log and store the centralized logs of the events of the distributed system
- Example: Elastic Search, Cloudwatch

### Messaging Queues

- Used to Build losely coupled system
- To enable asynchronous mesasging between system
- Implemented using Publisher, Consumer Architecture, Publisher Subscriber Arcitecture.
- Example: Rabbitmq, apache kafka.

### Distributed Task System

- Schedules and process task in distributed way.
- Example: Celery, Apache Airflow, Kubernetes CronJob

## System Architecture Styles

1. Client Server Architecture
2. Event Driven Architecture
3. Microkernel Architecture (plugin architecture)
4. Microservice Architecture

## Scaling the System
1. Vertical Scaling (Increase capacity of server)
2. Horizontal Scaling (Use multiple servers)

