# Scaling NoSQL Databases: A Primer

In today's day and age, organizations have more data than ever. On a smaller scale, developers are building startups serving large amounts of data to customers. All of these use cases require both the efficient storage and transmission of data. If a backend database goes down, a service can't be used, customers can't reach their app, and a myriad of issues appear.

To accommodate for this ever-growing thirst for data, many techniques have been developed to help address these issues. In this article, we mainly discuss two approaches: horizontal and vertical scaling. Before we get started, let's establish what we are referring to when we mention the term `database scaling`. Over the course of this post, database scaling refers to the act of scaling the database to accommodate an increase in read or write capacity.

### Horizontal Scaling

Horizontal scaling, also known as "scaling out," involves adding more machines to your existing pool of resources. Instead of upgrading a single server (as in vertical scaling), you distribute your data and load across multiple servers. This approach is particularly well-suited for NoSQL databases, which are often designed with horizontal scalability in mind.
When you horizontally scale a NoSQL database, you're essentially partitioning your data across multiple nodes. Each node holds a subset of the data, allowing for parallel processing and improved performance. This distribution is typically handled by a process called sharding.

#### Sharding

Sharding is a method of splitting your data into smaller, more manageable pieces called shards. Each shard is then placed on a different server. The key to effective sharding lies in choosing the right shard key—the attribute by which you divide your data.
For example, in a social media application, you might shard user data based on user IDs. Users with IDs 1-1,000,000 might go to Shard A, 1,000,001-2,000,000 to Shard B, and so on. This way, when a request comes in for a specific user, the system knows exactly which shard to query, reducing the amount of data that needs to be scanned.

#### Benefits of Horizontal Scaling

- Improved Availability: With data distributed across multiple nodes, your system becomes more resilient. If one node fails, the others can continue to serve requests.
- Better Performance: By spreading the load across multiple machines, you can handle more concurrent operations and reduce response times.
  Easier to Scale: Adding new nodes to the cluster is often simpler and more cost-effective than upgrading a single, powerful server.

#### Challenges

Despite its advantages, horizontal scaling isn't without its challenges:

- Increased Complexity: Managing a distributed system requires sophisticated tools and expertise. Issues like data consistency and network partitions become more prominent.
- Data Replication: To ensure high availability, data is often replicated across nodes. This replication can introduce latency and consistency issues if not managed properly.
- Cross-Shard Queries: Queries that span multiple shards can be slower and more complex to execute compared to single-shard queries.

### Vertical Scaling

Vertical scaling, often referred to as "scaling up," is the process of increasing the capacity of a single server by adding more resources such as CPU, RAM, or storage. This approach focuses on boosting the power of an individual machine rather than distributing the load across multiple servers.

#### How Vertical Scaling Works

When you vertically scale a database, you're essentially upgrading its hardware. This could mean switching from a dual-core to a quad-core processor, increasing RAM from 16GB to 32GB, or replacing HDDs with SSDs for faster I/O operations. The goal is to enhance the performance of the existing server to handle increased load.

#### Benefits of Vertical Scaling

- Simplicity: Vertical scaling is straightforward—you're dealing with a single server, which means less complexity in terms of data distribution and system architecture.
- Data Consistency: Since all data resides on one machine, maintaining data consistency is easier compared to distributed systems.
- Lower Latency: With all resources in one place, there's no network overhead between nodes, which can lead to lower latency for complex queries.
- Software Compatibility: Many traditional Relational Database Management Systems (RDBMS) are designed with vertical scaling in mind, making it a natural fit for these systems.

#### Limitations

Despite its advantages, vertical scaling has several limitations:

- Hardware Limits: There's a ceiling to how much you can upgrade a single machine. Eventually, you'll hit the maximum available CPU, RAM, or storage capacity.
- Cost: High-end hardware can be expensive, and the cost often increases non-linearly with performance gains.
- Single Point of Failure: Relying on a single server means that if it goes down, your entire system becomes unavailable.
- Downtime for Upgrades: Hardware upgrades often require taking the server offline, which can lead to service interruptions.

### Comparing Horizontal and Vertical Scaling

Both scaling strategies have their place in database management, and the choice often depends on your specific requirements:

- Scalability: Horizontal scaling offers practically limitless scalability by adding more machines to the cluster. Vertical scaling is bound by the maximum capacity of a single server.
- Flexibility: Horizontal scaling allows for incremental, on-demand scaling. You can add or remove nodes as needed. Vertical scaling often involves significant upgrades and can be less granular.
- Application Design: Some applications are better suited for one approach over the other. Horizontal scaling works well for distributed systems and microservices architectures, while vertical scaling might be preferred for monolithic applications with complex transactions.
- Data Model: NoSQL databases are generally designed for horizontal scalability, leveraging techniques like sharding effectively. Traditional SQL databases often start with vertical scaling, though many now support some form of horizontal scaling as well.
- Operational Complexity: Vertical scaling is simpler to manage but has higher downtime risks. Horizontal scaling offers better fault tolerance but requires more sophisticated operational tools and strategies.

In practice, many organizations adopt a hybrid approach, combining both vertical and horizontal scaling strategies. They might vertically scale to a certain point and then begin scaling horizontally when they reach hardware limits or when the cost-benefit ratio shifts.

The key is to understand your application's requirements, growth projections, and the characteristics of your chosen database system. This knowledge will guide you in developing a scaling strategy that ensures optimal performance, availability, and cost-efficiency as your data needs evolve.
