# Scalability in System Design

## Vertical Scaling

- Increasing the capacity of the components of the system.
- Example: Increasing the number of cpu core, ram, storage.
- It has limit in hardwards capcity, power supple etc.
- Possibility of Single Point of failure.
- Possibility of downtime during maintainance.

## Horizontal Scaling

- Adding more machines/servers in the system
- Example: adding extra number of servers and distributing load across the servers.
- No physical limitations.
- No Single point of failure.
- It's a fault tolerant scaling.
- No downtime required during adding and removing servers.
- Its costy to operatere, maintain and monitor. Use kubernetes to manage, deploy and maintain apps across multiple servers.

## Difference betwen Horizontal and Verticle Scalablity

- Horizational scalaing is cost effective due to elastic scaling.
- Horizontal scalaing is flexible due to easy to add and remove servers.
- Horizational scaling enhances fault tolerance of the system but in vertical system, system is prone to Single point of failture.
- Horizontal Scalability is required for system that receive very high traffics.

## Scaling Bottlnecks

1. Database Bottlenects
2. Network Bottlenects
3. Server Bottlenects
4. Authentication Bottlenects
5. Third-Party Services Bottlenecks
6. Code Execution Bottlenecks
7. Data Storage Bottlenects
