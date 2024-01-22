---
layout: post
title: "Titan DB vs Neo4J"
---

This comparison is an outdated comparison. I think `Neo4J` has improved a lot with the time. But I'm posting this because a person who wants to compare both of these technologies, can get an idea about the aspects they need to focus. If you know something is outdated please feel free to suggest using comments. I'll update the blog post accordingly.

| Feature                            | Neo4J                                                                         | Titan                                                                                                                                                        |
|------------------------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| License                            | GPL/AGPL/Commercial                                                           | Apache 2 License                                                                                                                                             |
| Commercial Support                 | Available Advanced: Email 5x10 USD 6000/yr Enterprise: Phone 7x24 USD 24,000/yr | Available \(Prices and availability of support not published officially\.\)                                                                                  |
| Graph Type                         | Property Graph                                                                | Property Graph                                                                                                                                               |
| Storage Backend                    | Native Storage Engine                                                         | Cassandra, Hbase, Berkeley DB                                                                                                                                |
|                                    |                                                                               | Depending on the requirement we should select Database Backend \(eg: Cassandra for Availability and Partitionable, Hbase for Consistency and Partitionable\) |
| ACID Support                       | Yes                                                                           | ACID is supported on BerkeleyDB Storage Backend                                                                                                              |
|                                    | Has Transactions in Java API\.                                                | On Cassandra Eventually consistent                                                                                                                           |
| Scalability                        | Can't Scale\-out like Titan                                                   | Owns very good scalability                                                                                                                                   |
|                                    |                                                                               | can scale like Cassandra if storage backend is cassandra                                                                                                     |
| High Availability                  | Replication is the only way to have high scalability                          | Titan is like API because of that Availability of Storage backend is the availability for graph database                                                     |
|                                    | Failover is not smooth                                                        | If we are using Cassandra with Titan No\-Single\-Point of failure\. Extremely Available                                                                      |
| Query Language                     | Cypher and Gremlin                                                            | Gremlin                                                                                                                                                      |
|                                    | Cypher easy to learn but only suitable for simple queries\.                   | Gremlin has good algorithms to retrieve data in an optimal way\. \(\+ More generic\)                                                                         |
| Graph Sharding                     | Not Available, under development                                              | Not Available, under development                                                                                                                             |
| Support for languages              | Java/\.NET/Python/PHP/NodeJS/Scala/GO                                         | Java                                                                                                                                                         |
| Written in                         | Java                                                                          | Java                                                                                                                                                         |
| Protocol                           | HTTP/REST                                                                     | Can expose REST using Rexster                                                                                                                                |
| Use cases                          | more than 10 available                                                        | 0 use cases exposed officially                                                                                                                               |
| Number of edges vertices supported | 2^35 \(~34 Billion\) Nodes \(Vertices\)                                       | 2^59 Vertices                                                                                                                                                |
|                                    | 2^35 \(~34 Billion\) Relationships \(edges\)                                  | 2^60 \(quintillion\) edges                                                                                                                                   |
|                                    | 2^36 \(~68 Billion\) Properties                                               |                                                                                                                                                              |
|                                    | 2^15 \(~32 000\) Relationship types                                           |                                                                                                                                                              |
| Limitations                        |                                                                               | Key Index must be created prior to the key being used                                                                                                        |
|                                    |                                                                               | Unable to drop key indices                                                                                                                                   |
|                                    |                                                                               | For bulk graph operations we have to use Faunus otherwise storage backends get OutOfMemoryException                                                          |
|                                    |                                                                               | Types cannot be changed once created                                                                                                                         |
| Web Admin                          | Available                                                                     | Not Available                                                                                                                                                |
| Embeddable                         | Yes                                                                           | Yes                                                                                                                                                          |
| MapReduce                          | \-                                                                            | Yes with Faunus                                                                                                                                              |
| Lucene Indexing Support            | Yes                                                                           | Yes                                                                                                                                                          |
| Backups                            | Yes                                                                           | Yes \(\+Titan Parallel backup\)                                                                                                                              |


This link is also very useful - [http://db-engines.com/en/system/Neo4j%3BTitan](http://db-engines.com/en/system/Neo4j%3BTitan)

### Tags

- Titan DB
- neo4j
- Graph DB
- Graph database
- NoSQL
- Titan