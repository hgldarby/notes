# Designing Distributed Systems

## Key words

- **Proxy server** - A server that acts as an intermediary for requests from clients seeking resources from other servers
- **Cache** - A hardware or software component that stores data so that future requests for that data can be served faster



### 1. Single-Node Patterns

- Goal of a container - to establish boundaries between specific resources
- What is a **container** - any object that holds an arbitrary number of other objects. eg tuple, list, set, dictionary.
- The boundary portrays team ownership i.e. the team owns this image
- Boundary - intended to provide separation of concerns i.e. this image does this one thing
- **Separation of concerns** allows for:
	- Easier understanding
	- Easier testing
	- Easier updating
	- Easier deployment



### 2. The Sidecar Pattern

##### Introduction

- **API** - a set of functions and procedures allowing the creation of applications that access the features or data of an operating system, application, or other service.

- **HTTPS** - Hypertext Transfer Protocol Secure is an extension of the Hypertext Transfer Protocol. It is used for secure communication over a computer network, and is widely used on the Internet.
- **NGINX** - *NGINX* is open source software for web serving, reverse proxying, caching, load balancing, media streaming, and more.

- Made up of two containers:
- First - application container
  - Contains core logic for the application
- Second - sidecar container
  - Role - to augment and improve the application container, often without the application containers knowledge.
  - In simplest form, can be used to add functionality to a container that might otherwise be difficult to improve.
- Scheduled on same machine
- Share resource - including parts of filesystem, hostname and network and many other namespaces

##### Dynamic Configuration with Sidecars

- Use for sidecar - proxying traffic into an existing application

- Another use - Configuration synchronisation:

  - Many existing applications assume this config file was present on the filesystem

- In cloud native environments it is often useful to use an API for updating configs.

- This allows dynamic push of config info via an API instead of manually logging into every server to update the config file.

- API is driven by ease of use and ability to add automation like rollback which makes configuring and reconfiguring safer and easier

##### Modular Application Containers

- **HTTP/topz** - interface that provides a readout of resource usage
- **PID** - Process id

- Use for sidecar - adapt legacy applications where you no longer want to make modifications to original source code
- Advantage - Modularity and ability to reuse of components used as sidecars.
- Trade offs between Modular container-based pattern and rolling your own code into the application.
- Library based approach - Less tailored which could mean it is less efficient and API might need adaptation to fit into your environment.
- Own code - More tailored but will take longer to complete.
- **Docker** - Docker is a set of coupled software-as-a-service and platform-as-a-service products that use operating-system-level virtualization to develop and deliver software in packages called containers

##### Building a Simple PaaS with Sidecars

- **PaaS** - Platform as a service
- **Git** - Git is a distributed version-control system for tracking changes in source code during software development
- **Nodemon** - a way to restart your code whenever file changes have been made
- Sidecar can be used as a means to implement the complete logic for your application in a simplified, modular manner.

##### Designing Sidecars for Modularity and Reusability

- To be successful - sidecar should be reusable across a wide variety or applications and deployments

- Achieving modular reuse means sidecars can speed up the building of the application.

- Three areas to focus on 

  - Parameterising your containers
  - Creating the API surface of your container
  - Documenting the operation of your container

##### Parameterising your containers

- **SSL** - (Secure Sockets Layer) is the standard security technology for establishing an encrypted link between a web server and a browser
- **Legacy application** - outdated or obsolete software program

- Most important thing to do to make containers modular and reusable
- Consider your container as a function - how many parameters does it have
- Each parameter represents an input that can customise a generic container to a specific situation
- Two ways to pass parameters to your container:
  - Through environment variables
  - Through the command line
- A shell script is used to load the environment variables supplied with the sidecar container and either adjust the config files or parameterise the underlying application.

##### Define Each Container's API

- Given you're parameterising your containers, they are clearly "functions" that are called when the container is executed.

- This function is part of the API defined by the container

- Calls the container makes to other services are a part of the API

- Traditional HTTP or other APIs that the container provides are a part of the API

- All aspects of how the container interacts with its world are part of the API

- Micro-containers rely on APIs to ensure a clean separation between main application and the sidecar

- API exists to ensure all consumers of the sidecar continue to work correctly as new versions are released

- Clean API allows development to move faster

  

### 3. Ambassadors

- **Ambassador container** - brokers interactions between the application container and the rest of the world.
- Made up of modular containers

##### Using an Ambassador to Shard a Service

- If data is too large for one machine to handle you shard your storage layer
- **Sharding** - splits up the storage layer into multiple disjointed pieces, each hosted by a separate machine.
- **Middleware** - software that acts as a bridge between an operating system or database and applications, especially on a network.
- Sharded services make it difficult to share configs between development (usually single storage shard) and production (often many storage shards)
- Result of applying ambassador pattern - separation of concerns between application container, simply knows it needs to talk to a storage service and discovers that service on localhost, and the sharding ambassador proxy, which only contains the code necessary to perform appropriate sharding.
- **Redis** - a fast key-value store that can be used as a cache or for more persistent storage

##### Using and Ambassador for Service Brokering

- Primary challenge when trying to render an application portable across multiple environments is service discovery and configuration.
- e.g. - frontend relies on MySQL database to store data. In public cloud this might be provided as a SaaS whereas in private it may be necessary to dynamically spin up a new virtual machine or container running MySQL
- **SaaS** - Software as a service
- **Service Discovery** - requirement that the application know how to introspect its environment and find the appropriate MySQL service to connect to.
- **Service Broker** - the system that performs the discovery and linking

##### Using and Ambassador to do Experimentation or Request Splitting

- **Request splitting** - some fraction of all requests are not serviced by the main production but are redirected to a different implementation of the service

- Often used to perform experiments with beta versions of the service to assess if the new version is reliable.

- Can be used to split traffic so it goes to both production and newer undeployed systems.

- Responses from production are returned to user but ignored from beta

  

### 4. Adapters

- **Adapter Container** - used to modify the interface of the application container so that it conforms to some predefined interface that is expected of all apps
- Made up of modular containers

##### Monitoring

- Applying adapter pattern means the application container is the application we want to monitor
- **Prometheus** - Monitoring aggregator which collects metrics and aggregates them into a single time-series database

##### Logging

- Wide variety of heterogeneity in how systems log data to an output stream. 
- Information logged generally has structured information which varies widely between different logging libraries
- Ensure, regardless of different structures for the data, every log ends up with the appropriate timestamp
- Adapter container can transform data which can be in different formats, into a single structured representation which can be consumed by the log aggregator
- The adapter is taking a heterogeneous world of apps and creating a homogeneous world of common interfaces

- **fluentd** - one of the more popular open source logging agents

##### Adding a Health Monitor

- Adapter container would contain the shell script for determining the health of the database if one is added.

#### Serving Patterns

- Symbiotic systems - They depend on local, shared resources like disk, network interface, or inter-process communications
- These are important, and are building blocks for larger systems.
- Reliability, Scalability and separation of concerns dictate that real-world systems are built from many different components spread over multiple machines

##### Introduction to Microservices

- **Microservices** - a system built out of many different components running in different processes and communicating over defined APIs
- Stand in contrast to **monolithic systems** which tend to place all functionality for a service within a single tightly coordinated application.
- Microservices allow for better scaling
- As each component is broken into its own service, it can be scaled independently
- Debugging is more difficult 

### 5. Replicated Load-Balanced Services

- In this, every server is identical to every other server - all are capable of supporting traffic
- **Kubernetes** - an open-source container-orchestration system for automating application deployment, scaling, and management

##### Stateless Services

- **Stateless Services** - a service that doesn't require a saved state to operate correctly
- Examples - static content servers and complex middleware systems that receive and aggregate responses from numerous different backend systems
- Replicated to provide redundancy and scale
- Need two replicas to provide a highly available SLA
- **SLA** - Service Level Agreement
- Instead, could have two replicas with a load balancer so that while doing a rollout or if the software crashes, the users can use the other replica

##### Readiness Probes for Load Balancing

- **Readiness Probe** - determines when an application is ready to serve user requests

##### Session Tracked Services

- Often reasons to ensure a particular users requests end up on the same machine
- Reason could be that you're caching users data in memory so landing on the same machine ensures a higher cache hit rate
- Could be that the interaction is long-running in nature so some amount of state is maintained between requests
- Session tracking is performed by hashing the source and destination IP addresses and using that key to identify the server that should service the request
- If the IP addresses stay constant, all requests are sent to the same replica
- Session tracking accomplished via a **consistent hashing function**
- Benefit of this - evident when service is scaled up or down
- **Consistent hashing function** - minimise the number of users that actually change which replica they are mapped to which reduces the impact of scaling on the app

##### Application-Layer Replicated Services

- In preceeding examples, replication and load balancing takes place in the network layer of the service
- Many apps use HTTP as the protocol for speaking with each other

##### Introducing a Caching Layer

- Code can be expensive despite being stateless
- Might make queries to a database to service requests or do significant amounts of rendering or data mixing to service the request
- For these reasons a caching layer can make a great deal of sense
- Cache exists between stateless app and the end-user request
- caching proxy - a HTTP server that maintains user requests in memory state.
- If two users request the same web page, only one request goes to the backend, the other is serviced from memory in the cache
- **Varnish** - an open source web cache

##### Deploying your cache

- Simplest way - alongside each instance of the web server using the sidecar pattern
- Disadvantage - you have to scale your cache at the same scale as the web servers
- For the cache, you want as few replicas as possible with lots of resources for each replica

##### Expanding the Caching Layer

- http reverse proxies like Varnish can provide a number of advanced features useful beyond caching.

##### Rate Limiting and Denial-of-Service Defence

- **Denial of service** - An interruption in an authorised user's access to a computer network
- Can usually come from developer misconfiguring a client or a site-reliability engineer accidentally running a load test against a production installation
- If you're deploying an API, using a small rate limit for anonymous access and then forcing users to login to obtain a higher rate limit is best practice.
- When users hits rate limit, code 429 is returned indicating - too many requests have been issued

##### SSL Termination

- Additionally to caching for performance, the edge layer also performs SSL Termination
- Using SSL for communication should still use different certificates for the edge and your internal services



### 6. Sharded Services

- In contrast to replicated services, each replica in a sharded service is only capable of serving a subset of all requests

- Example - in replicated services requests A, B and C go to all of #1, #2 and #3 whereas in sharded services #1 only gets request A, #2 only gets request B and #3 only gets request C

- Replicated services - used for building stateless services

- Sharded services - used for building stateful services

- Reason for sharding data - the size of the state is too large to be served by a single machine

- Sharding enables you to scale a service in response to the size of the state that needs to be served

##### Sharded caching

- Sharded cache - a cache that sits between the user requests and the frontend implementation

  ##### Why you might need a sharded cache

- Primary reason for sharding a service is to increase the size of the data being stored in the service
- **RPS** - Requests per second
- For an example, look on page 60

##### The role of the cache in system performance

- Important question - if the cache were to fail, what would the impact be for your users and your service?

- In replicated cache this question isn't as applicable as the cache itself was horizontally scalable and failures of specific replicas would only lead to transient failures

- Different in sharded caches. If a shard fails and a user or request is always mapped to the same shard, the user or request will always miss the cache until the shard is restored

- As the nature of a cache is transient, it is not inherently a problem

- System must know how to recalculate the data but this is slower than using the cache directly

- Performance of the cache is defined in terms of its **hit rate**

- **Hit rate** - the percentage of the time that you cache contains the data for a user request

- The hit rate ultimately determines the overall capacity of the distributed system and affects the overall capacity and performance of the system

- For an example see page 61

- System end user performance not only defined by number of requests it can process but also by the latency of requests.

- **Latency** - The delay before a transfer of data begins following an instruction for its transfer

- Cache can improve the speed as well as total number of requests processed.

- Needing to upgrade or redeploy a sharded cache cannot be done by just deploying a new replica and assume it will take the load. Deploying new version of a sharded cache will generally result in temporarily losing some capacity.

##### Replicated, Sharded caches

- Sometimes the system is too dependent upon a cache for latency or load that it is not acceptable to lose an entire cache shard if there is a failure or a rollout is being done.
- Alternatively, there may be so much load on a particular cache shard that it needs to be scaled to handle the load
- For the above reasons, a **sharded replicated service** may be chosen to be deployed
- **Sharded Replicated Service** - Combines replicated service pattern with the sharded pattern. i.e. rather than having a single server implement each shard in the cache, a replicated service is used to implement each cache shard.
- This is more complicated but has many advantages
- By replacing a single server with a replicated service, each cache shard is resilient to failure and is always present during failures.
- As each replicated cache shard is an independent replicated service, each cache shard can be scaled in response to its load
- 

