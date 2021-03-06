# My learning notes about SaaS

SaaS stands for "software as a service" It can be described as a software distribution model.

There are two main varieties of SaaS  
1. Vertical SaaS  
   A Software which answers the needs of a specific industry
2. Horizontal SaaS  
   The products which focus on a software category (marketing, sales, developer tools, HR) but are industry agnostic.

A nice to have features that distinguish a SaaS product from standard software:  
1. Multi-tenancy model.  
2. Automated provisioning.  
3. Single sign-on.  
4. Subscription-based billing.  
5. High availability.  
6. Elastic infrastructure.  
7. Data security.  
8. Application security.  
9. Rate limiting/QoS.  
10. Audit.

SaaS architecture can be divided by two categories:  
1. Single tenant  
2. Multi tenant

![single vs multi](https://github.com/bluething/learnsaas/blob/main/images/singlevsmulti.png?raw=true)

## Single tenant Architecture

Like having a whole building for an office area. Single tenant architecture uses a software application and a database for each tenant (client).  
With this model we have a specific design, making it unique, since it allows only one instance per every SaaS server.

The benefit:  
1. Reliable. Allows clients to continue using their software even if another client is experiencing downtime during some cumbersome integrations.  
2. Secure. Client’s data will ultimately be isolated from all others customers
3. If the client want to move from SaaS environment, they can do it easily because all the information is already stored in one space.

The disadvantage:  
1. Requires much more resources and time for maintenance and customization.  
2. Requires more maintenance.  
3. Single-tenancy is much more expensive.

## Multi Tenant Architecture

Like rent a building (floor or unit) together with other tenant. A multi tenancy is an architecture in which every instance of software application is serving more than one tenant (client). The multi-client architecture means that all clients will share the same database and application information.

The benefit:  
1. Maintenance costs are much cheaper.  
2. The multi tenant architecture gives organizations the possibility of staying within the same infrastructure and data center.  
3. Multi tenant architecture has very efficient resource usage and potentially has much larger computing capacities.  
4. One single source of trust.  
5. Cost reductions of development and time-to-market.

The disadvantage:  
1. Multi tenant structure is much more vulnerable to a security standpoint since it leaves behind a significant number of access points that are suitable for cyberattacks.  
2. Multi tenant structures don’t offer as many options for customization as single tenant structures do. This means that the multi tenant architecture users will have less control when it comes to environmental quality.

The multi tenant approach models are divided into:  
1. Logical data separation.  
2. Physical data separation.

The multi tenant application structures are divided into:  
1. Virtualization-based SaaS (containers)
2. Multi Tenant SaaS
3. URL-based SaaS. It uses a single database and domain.

When designing multi-tenant applications, we should consider:
1. The number of tenants and their isolation.  
Isolation types is siloed, pool, and bridge.
2. Policy management mechanisms.  
   For example available features, performance, limitations and SLAs (Service Level Agreements)

## What stack technology do we need to think about?

1. Programming language.  
2. Cloud provider.  
3. Monolithic, microservices, or serverless ecosystem.  
4. Container orchestration platform.  
5. Database.  
6. Restful vs GraphQL.  
7. Automation.  
8. Message queue system.  
9. Caching system.
10. Cloud storage system.

### Programming language

### Cloud provider

### Architectural types

#### Monolithic Architecture

![monolith](https://github.com/bluething/learnsaas/blob/main/images/monolith.png?raw=true)  
Example of monolith architectural style

#### Microservices

![mircoservices](https://github.com/bluething/learnsaas/blob/main/images/microservices.png?raw=true)  
Example of microservices architectural style

#### Kubernetes Architecture

![kubernetes](https://github.com/bluething/learnsaas/blob/main/images/kubernetes.png?raw=true)  
Example of kubernetes architectural style

#### Serverless Architecture

![serverless](https://github.com/bluething/learnsaas/blob/main/images/serverless.png?raw=true)  
Example of serverless architectural style

### Container orchestration platform

### Database

#### How to choose the appropriate tenancy model

##### Scalability

- Number of tenants.  
- Storage per-tenant.  
- Storage in aggregate.  
- Workload.

##### Tenant Isolation

Data isolation and performance (whether one tenant's workload impacts others).

##### Per-tenant cost

Database costs.

##### Development complexity

- Changes to schema.  
- Changes to queries (required by the pattern).

##### Operational complexity

- Monitoring and managing performance.  
- Schema management.  
- Restoring a tenant.  
- Disaster recovery.

##### Customizability

Ease of supporting schema customizations that are either tenant-specific or tenant class-specific.

| Measurement                           | Standalone app                                  | Database-per-tenant                              | Sharded multi-tenant                                          |
|---------------------------------------|-------------------------------------------------|--------------------------------------------------|---------------------------------------------------------------|
| Scale                                 | Medium 1-100s                                   | Very high 1-100000s                              | Unlimited 1-1000000s                                          |
| Tenant isolation                      | Very high                                       | High                                             | Low; except for any single tenant (that is alone in an MT db) |
| Database cost per tenant	             | High; is sized for peaks                        | Low; pools used                                  | Lowest, for small tenants in MT DBs                           |
| Performance monitoring and management | Per-tenant only                                 | Aggregate + per-tenant                           | Aggregate; although is per-tenant only for singles            |
| Development complexity                | Low                                             | Low                                              | Medium; due to sharding                                       |
| Operational complexity                | Low-High. Individually simple, complex at scale | Low-Medium. Patterns address complexity at scale | Low-High. Individual tenant management is complex             |

#### Tenancy model

###### Database-per-tenant

Also call the Siloed model, where you need a database instance per customer. Expensive, but the best for isolation and security compliance.

###### Multi-tenant database

One important distinction to notice is that with more than 100 schemas or tenants within a database, it can provoke a _lag in our database performance_.  
Hence, it is recommended to split the database into two (add the second database as a replica). However, the best database tool for this approach is PostgreSQL, which supports multiple schemas without much complexity.  
And lastly, this strategy of shares resources, compute, and storage across all its tenants. As a result, it provokes noisy tenants that utilize more resources than expected.

###### Single multi-tenant database

A table per each organization within a database schema. There are specific trade-offs for this architecture, including the sacrifice of data isolation, noise among tenants, and performance degradation, meaning that one tenant can overuse compute and ram resources from another.  
This architecture model is _not recommended_. Alternatively use sharded multi-tenant database.

###### Sharded multi-tenant database

This model facilitates tenant data to be distributed across multiple databases (shards), with all the data for a particular tenant is all contained in a single shard. A sharding key/tenant identifier is managed and imposed by the database schema.  
Designing of the shard architecture can be _complex_ due to the need to maintain a mapping between tenants and databases. Also, the application has to maintain a catalogue of the shards and respective tenants.

###### The options

![database option](https://github.com/bluething/learnsaas/blob/main/images/databaseoptions.jpg?raw=true)

### Restful vs GraphQL

### Automation

### Message queue system

### Caching system

### Cloud storage system

## Application security

### Security assessments

#### Employee level

1. Employees are on the same page concerning the recommended security practices.  
2. The sharing of user accounts is prohibited.  
3. Assets like phones and laptops are encrypted.  
4. Two-factor authentication and the use of password managers are being enforced.  
5. User logins are being monitored.  
6. Dedicated or partially dedicated security engineers are available to handle crucial security tasks.

#### Code level

1. A Secure Development Lifecycle (SDL) is being used.  
2. Security within the Software Development Life Cycle (SDLC) is automated.  
3. A secure code review checklist is being enforced.  
4. Security-oriented test sessions are being performed.  
5. The coding environment integrates identity and access management (IAM) and account provisioning systems.  
6. The project includes event and log notifications.  
7. The project includes fault-tolerance and scalability

#### Application level

Application should have:  
1. Security is automated.  
2. Real-time protection services are being used.  
3. Dependencies are being tracked.  
4. The application supports Security Assertion Markup Language (SAML).  
5. Application support includes System for Cross-domain Identity Management (SCIM) or Service Provisioning Markup Language (SPML), multi-factor authentication, OAuth, and more.  
6. A desktop client is available for data synchronization.  
7. The application supports automated identity importing.  
8. The application supports authentication filtering

The test cases covers the following types of vulnerability:  
1. Information gathering vulnerabilities.  
2. Configuration management vulnerabilities.  
3. Authentication and authorization vulnerabilities.  
4. Data validation vulnerabilities

#### Infrastructure level

1. Backups are carried out and tested.  
2. The application’s underlying security is in place.  
3. Internal services are being monitored.  
4. Exposed services are being monitored.  
5. Applications and APIs use encryption

#### Users level

1. The use of two-factor authentication is being encouraged.  
2. A password policy is being enforced.  
3. Suspicious activities are being monitored.

### SaaS security issues

Beware of [OWASP Top Ten](https://owasp.org/www-project-top-ten/)

### Authorization

The challenge is the mingling of data and user activities in the collaborative environment.  
We can use RBAC, but falls short when it comes to managing the kind of collaboration in a multi-tenant setup.  
The alternative is use Multi tenancy authorization system (MTAS)  
![MTAS](https://github.com/bluething/learnsaas/blob/main/images/MTAS-system.jpeg.webp?raw=true)

### Isolation

The options are siloed (fully isolated) and pool (through authentication policy) model.  
![isolation type](https://github.com/bluething/learnsaas/blob/main/images/isolation-types.jpeg.webp?raw=true)

Test our model for cross boundary access.

### Things to watch out

- Stay compliant with certifications and audits.  
- Enforce data retention.  
  We need to have a clear understanding of which data needs to be retained.
- Implement transmission data encryption.  
Also applied for data in storage.
- Integrate real-time protection.

## Starting Point

![saas landscape](https://github.com/bluething/learnsaas/blob/main/images/saaslandscape.png?raw=true)

1. Think about identity and onboarding on day one.  
2. Limit developer awareness of multi-tenancy.  
3. Find the data partitioning model that fit each microservice.  
4. Tenant isolation != authentication/authorization.  
5. Don't overlook metrics, operations, and agility.

### Onboarding

1. How new tenant get introduced to our environment?  
2. How the tenant select the tiers?  
3. How the tenant sign up? 
4. How the infrastructure get configured?

![tenant onboarding](https://github.com/bluething/learnsaas/blob/main/images/tenantonboarding.png?raw=true)

### Authentication

1. Association between tenant and identity.  
2. How the identity and policy flow through the system? _Tenant context everywhere!_

![tenant context](https://github.com/bluething/learnsaas/blob/main/images/tenantcontexteverywhere.png?raw=true)

### Application Service

Our microservices. When design the microservices don't think about multi tenant, code like we build single tenant.  
The key to achieve this is _tenant context everywhere_. Use tenant data (identity) to get their data.

![tenant microservices](https://github.com/bluething/learnsaas/blob/main/images/tenantmicroservices.png?raw=true)

### Storage Partitioning

1. How we represent the tenant data?  
2. How we isolate the tenant data?

The option are silo or pool. Pool based isolation have a challenge, how we ensure the tenant data (or resources) can't be accessed by other tenant?  
The solution is using _tenant context_.  
![runtime scope](https://github.com/bluething/learnsaas/blob/main/images/runtimescope.png?raw=true)

The decision influenced by  
1. Compliance and security.  
2. Performance.  
3. Data footprint.  
4. Noisy neighbor.  
5. Data distribution.

### Matrics/analytics

### Management

### Billing

## References

[Single Tenant vs Multi Tenant: SaaS Architecture](https://www.clickittech.com/aws/single-tenant-multi-tenant/)  
[Multi tenant Architecture for a SaaS Application on AWS](https://www.clickittech.com/saas/multi-tenant-architecture/)  
[How to Design and Develop Successful SaaS Application](https://devcom.com/tech-blog/how-to-design-and-develop-saas-application/)  
[Multi-tenant SaaS database tenancy patterns](https://docs.microsoft.com/en-us/azure/azure-sql/database/saas-tenancy-app-design-patterns)  
[Multi-tenant Application Database Design](https://blakebhowe.medium.com/multi-tenant-application-database-design-e4c2d161f3dd)  
[SaaS Application Security Guide: Issues, Best Practices, and Examples](https://relevant.software/blog/saas-application-security-guide/)  
[Multi-Tenancy Authorization System with Federated Identity for Cloud-Based Environments Using Shibboleth](https://www.researchgate.net/publication/257200931_Multi-Tenancy_Authorization_System_with_Federated_Identity_for_Cloud-Based_Environments_Using_Shibboleth)  
[Towards a Multi-tenancy Authorization System for Cloud Services](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.475.2413&rep=rep1&type=pdf)  
[Multi-Tenancy Authorization Models for Collaborative Cloud Services](https://profsandhu.com/confrnc/misconf/cts13-paper-preprint.pdf)  
[SaaS Deep Dive: Designing and Building Multi-Tenant Solutions • Tod Golding • GOTO 2020](https://youtu.be/joz0DoSQDNw)