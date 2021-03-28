# System Design Archives

This is my personal system design archives and it's where I store my system design research that aims to provide resources to better interview developers in my engineering management journey.

- [System Design](#system-design)
  - [Client-Server Model](#client-server-model)
    - [Client](#client)
    - [Server](#server)
    - [Client-Server](#client-server)
    - [IP Address](#ip-address)
    - [Port](#port)
    - [DNS](#dns)
  - [Network Protocols](#network-protocols)
    - [IP](#ip)
    - [TCP](#tcp)
    - [HTTP](#http)
    - [IP Packet](#ip-packet)
  - [Storage](#storage)
    - [Database](#database)
    - [Disk](#disk)
    - [Memory](#memory)
    - [Persistence Storage](#persistence-storage)
  - [Latency and Throughput](#latency-and-throughput)
    - [Latency](#latency)
    - [Throughput](#throughput)
  - [Availability](#availability)
    - [High availability](#high-availability)
    - [Nines](#nines)
    - [redundancy](#redundancy)
    - [SLA](#sla)
    - [SLO](#slo)
  - [Caching](#caching)
    - [Cache](#cache)
    - [Cache Hit](#cache-hit)
    - [Cache Miss](#cache-miss)
    - [Cache Eviction Policy](#cache-eviction-policy)
    - [Content Delivery Network](#content-delivery-network)
  - [Proxies](#proxies)
    - [Forward Proxy](#forward-proxy)
    - [Reverse Proxy](#reverse-proxy)
    - [Nginx](#nginx)
  - [Load Balancers](#load-balancers)
    - [Load balancer](#load-balancer)
    - [Server-selection strategy](#server-selection-strategy)
    - [Hot Spot](#Hot-spot)
  - [Hashing](#hashing)
    - [Eventual consistency](#eventual-consistency)
    - [Strong consistency](#strong-consistency)
    - [Rendezvous Hashing](#rendezvous-hashing)
    - [SHA](#sha)
  - [Relational Databases](#relational-databases)
    - [Relational database](#relational-database)
    - [Non-relational database](#Non-relational database)
    - [SQL](#sql)
    - [SQL database](#sql-database)
    - [NoSQL database](#nosql-database)
    - [ACID Transaction](#acid-transaction)
    - [Database index](#database-index)
    - [Strong consistency](#strong-consistency)
    - [Eventual consistency](#eventual-consistency)
    - [Postgres](#postgres)
  - [Key-Value Stores](#key-value-stores)
    - [Key-value store](#key-value-store)
    - [Etcd](#etcd)
    - [Redis](#redis)
    - [ZooKeeper](#zookeeper)
  - [Specialized Storage Paradigms](#specialized-storage-paradigms)
    - [Blob storage](#blob-storage)
    - [Time Series Database](#time-series-database)
    - [Graph database](#graph-database)
    - [Cypher](#cypher)
    - [Spatial Database](#spartial-database)
    - [Quadtree](#quadtree)
    - [Google Storage](#google-storage)
    - [S3](#s3)
    - [InfluxDB](#influxdb)
    - [Prometheus](#prometheus)
    - [Neo4j](#neo4j)
  - [Replication And Sharding](#replication-and-sharding)
    - [Replication](#replication)
    - [Sharding](#sharding)
    - [Hot spot](#hot-spot)
  - [Leader Election](#leader-election)
    - [Leader election](#leader-election)
    - [Consensus algorithm](#consensus-algorithm)
    - [Paxos & Raft](#paxos-&-raft)
    - [Etcd](#etcd)
    - [ZooKeeper](#zookeeper)
  - [Peer-To-Peer Networks](#peer-to-peer-networks)
    - [Peer-to-peer network](#peer-to-peer-network)
    - [Gossip protocol](#gossip-protocol)
  - [Polling And Streaming](#polling-and-streaming)
    - [Polling](#polling)
    - [Streaming](#streaming)
  - [Configuration](#configuration)
    - [Configuration](#configuration)
  - [Rate Limiting](#rate-limiting)
    - [DoS attack](#dos-attack)
    - [DDoS attack](#ddos-attack)
    - [Redis](#redis)
  - [Logging And Monitoring](#logging-and-monitoring)
    - [Logging](#logging)
    - [Monitoring](#monitoring)
    - [Alerting](#alerting)
  - [Publish-Subscribe Pattern](#publish-subscribe-pattern)
    - [Pub-Sub Pattern](#pub-sub-pattern)
    - [Idempotent operation](#idempotent-operation)
    - [Apache Kafka](#apache-kafka)
    - [Cloud Pub/Sub](#cloud-pub-sub)
  - [MapReduce](#mapreduce)
    - [Distributed File System](#distributed-file-system)
    - [Hadoop](#hadoop)
  - [Security And HTTPS](#security-and-https)
    - [Main-in-the-middle attack](#)
    - [Symmetric encryption](#)
    - [Asymmetric encryption](#)
    - [AES](#aes)
    - [HTTPS](#https)
    - [TLS](#tls)
    - [SSL Certificate](#ssl-certificate)
    - [Certificate Authority](#certificate-authority)
    - [TLS Handshake](#tls-handshake)
  - [API Design](#api-design)
    - [Pagination](#pagination)
    - [CRUD Operations](#crud-operations)

# System Design

## Client-Server Model

A client is a thing that talks to servers. A server is a thing that talks to clients. The client—server model is a thing made up of a bunch of clients and servers talking to one another.

And that, kids, is how the Internet works!

### Client

A machine or process that requests data or service from a server.

Note that a single machine or piece of software can be both a client and a
server at the same time. For instance, a single machine could act as a server
for end users and as a client for a database.

### Server

A machine or process that provides data or service for a client, usually by
listening for incoming network calls.

Note that a single machine or piece of software can be both a client and a
server at the same time. For instance, a single machine could act as a server
for end users and as a client for a database.

### Client-Server

The paradigm by which modern systems are designed, which consists of clients
requesting data or service from servers and servers providing data or service
to clients.

### IP Address

An address given to each machine connected to the public internet. IPv4
addresses consist of four numbers separated by dots: `a.b.c.d` where all
four numbers are between 0 and 255. Special values include:

- 127.0.0.1: Your own local machine. Also referred to as
- 192.168.x.y: Your private network. For instance, your machine and all
machines on your private wifi network will usually have the `192.168` prefix.

### Port

In order for multiple programs to listen for new network connections on the
same machine without colliding, they pick a `port` to listen on. A port
is an integer between 0 and 65,535 (2^16 ports total).

Typically, ports 0-1023 are reserved for `system ports` (also called `well-known`
ports) and shouldn't be used by user-level processes.
Certain ports have pre-defined uses, and although you usually won't be
required to have them memorized, they can sometimes come in handy. Below are
some examples:

- 22: Secure Shell
- 53: DNS lookup
- 80: HTTP
- 443: HTTPS

### DNS

Short for Domain Name System, it describes the entities and protocols involved in the
translation from domain names to IP Addresses. Typically, machines make a DNS query to
a well known entity which is responsible for returning the IP address (or multiple ones)
of the requested domain name in the response.

## Network Protocols

IP packets. TCP headers. HTTP requests.

As daunting as they may seem, these low-level networking concepts are essential
to understanding how machines in a system communicate with one another. And as
we all know, proper communication is key for thriving relationships!

### IP

Stands for `Internet Protocol`. This network protocol outlines how almost
all machine-to-machine communications should happen in the world. Other
protocols like `TCP`, `UDP` and `HTTP` are built on top of IP.

### TCP

Network protocol built on top of the Internet Protocol (IP). Allows for
ordered, reliable data delivery between machines over the public internet by
creating a `connection`.

TCP is usually implemented in the kernel, which exposes `sockets` to
applications that they can use to stream data through an open connection.

### HTTP

The `H`yper`T`ext `T`ransfer `P`rotocol is a very common network protocol
implemented on top of TCP. Clients make HTTP requests, and servers respond with
a response.

Requests typically have the following schema:
```
host: string (example: domaintest.io)
port: integer (example: 80 or 443)
method: string (example: GET, PUT, POST, DELETE, OPTIONS or PATCH)
headers: pair list (example: "Content-Type" => "application/json")
body: opaque sequence of bytes
```

Responses typically have the following schema:

```
status code: integer (example: 200, 401)
headers: pair list (example: "Content-Length" => 1238)
body: opaque sequence of bytes.
```

### IP Packet

Sometimes more broadly referred to as just a (network) `packet`, an IP
packet is effectively the smallest unit used to describe data being sent over
`IP`, aside from bytes. An IP packet consists of:

- an `IP header`, which contains the source and destination `IP addresses` as well
as other information related to the network a `payload`, which is just the data
being sent over the network.

## Storage

As it turns out, information storage is an incredibly complex topic that is of
vital importance to systems design.

### Databases

Databases are programs that either use disk or memory to do 2 core things:
`record` data and `query` data. In general, they are themselves
servers that are long lived and interact with the rest of your application
through network calls, with protocols on top of TCP or even HTTP.

Some databases only keep records in memory, and the users of such databases
are aware of the fact that those records may be lost forever if the machine or
process dies.

For the most part though, databases need persistence of those records, and
thus cannot use memory. This means that you have to write your data to disk.
Anything written to disk will remain through power loss or network partitions,
so that’s what is used to keep permanent records.

Since machines die often in a large scale system, special disk partitions or
volumes are used by the database processes, and those volumes can get
recovered even if the machine were to go down permanently.

### Disk

Usually refers to either `HDD (hard-disk drive)` or `SSD (solid-state drive)`.
Data written to disk will persist through power failures and general machine
crashes. Disk is also referred to as `non-volatile storage`.

SSD is far faster than HDD (see latencies of accessing data from SSD and HDD)
but also far more expensive from a financial point of view. Because of that,
HDD will typically be used for data that's rarely accessed or updated, but
that's stored for a long time, and SSD will be used for data that's frequently
accessed and updated.

### Memory

Short for `Random Access Memory (RAM)`. Data stored in memory will be
`lost` when the process that has written that data dies.

### Persistence Storage

Usually refers to disk, but in general it is any form of storage that persists
if the process in charge of managing it dies.

## Latency and Throughput

### Latency

If you've ever experienced lag in a video game, it was most likely due to a
combination of high latency and low throughput. And lag sucks.

It is therefore your Call of Duty to master these two concepts and to join the
crusade against high ping.

The time it takes for a certain operation to complete in a system. Most often
this measure is a time duration, like milliseconds or seconds. You should know
these orders of magnitude:

```
Reading 1 MB from RAM: 250 μs (0.25 ms)
Reading 1 MB from SSD: 1,000 μs (1 ms)
Transfer 1 MB over Network: 10,000 μs (10 ms)
Reading 1MB from HDD: 20,000 μs (20 ms)
Inter-Continental Round Trip: 150,000 μs (150 ms)
```

### Throughput

The number of operations that a system can handle properly per time unit. For
instance the throughput of a server can often be measured in requests per
second (RPS or QPS).

## Availability

The odds of a particular server or service being up and running at any point
in time, usually measured in percentages. A server that has 99% availability
will be operational 99% of the time (this would be described as having two
`nines` of availability).

### High availability

Used to describe systems that have particularly high levels of availability,
typically 5 nines or more; sometimes abbreviated "HA".

### Nines

Typically refers to percentages of uptime. For example, 5 nines of
availability means an uptime of 99.999% of the time. Below are the downtimes
expected per year depending on those 9s:

```
- 99% (two 9s): 87.7 hours
- 99.9% (three 9s): 8.8 hours
- 99.99%: 52.6 minutes
- 99.999%: 5.3 minutes
```

### Redundancy

The process of replicating parts of a system in an effort to make it more
reliable.

### SLA

Short for "service-level agreement", an SLA is a collection of guarantees
given to a customer by a service provider. SLAs typically make guarantees on a
system's availability, amongst other things. SLAs are made up of one or
multiple SLOs.

### SLO

Short for "service-level objective", an SLO is a guarantee given to a customer
by a service provider. SLOs typically make guarantees on a system's
availability, amongst other things. SLOs constitute an SLA.

## Caching

### Cache

A piece of hardware or software that stores data, typically meant to retrieve
that data faster than otherwise.

Caches are often used to store responses to network requests as well as
results of computationally-long operations.

Note that data in a cache can become `stale` if the main source of truth
for that data (i.e., the main database behind the cache) gets updated and the
cache doesn't.

### Cache Hit

When requested data could have been found in a cache but isn't.

### Cache Miss

This is typically used to refer to a negative consequence of a system failure or of a
poor design choice. For example:

If a server goes down, our load balancer will have to forward requests to a
new server, which will result in cache misses.

### Cache Eviction Policy

The policy by which values get evicted or removed from a cache. Popular cache
eviction policies include `LRU` (least-recently used), `FIFO` (first
in first out), and `LFU` (least-frequently used).

### Content Delivery Network

A `CDN` is a third-party service that acts like a cache for your servers.
Sometimes, web applications can be slow for users in a particular region if
your servers are located only in another region. A CDN has servers all around
the world, meaning that the latency to a CDN's servers will almost always be
far better than the latency to your servers. A CDN's servers are often referred
to as `PoPs` (Points of Presence). Two of the most popular CDNs are `Cloudflare`
and `Google Cloud CDN`.

## Proxies

### Forward Proxy

A server that sits between a client and servers and acts on behalf of the
client, typically used to mask the client's identity (IP address). Note that
forward proxies are often referred to as just proxies.

### Reverse Proxy

A server that sits between clients and servers and acts on behalf of the
servers, typically used for logging, load balancing, or caching.

### Nginx

Pronounced "engine X"—not "N jinx", Nginx is a very popular webserver that's
often used as a `reverse proxy` and `load balancer`.

## Load Balancers

Relentlessly distributing network requests across multiple servers, these digital
traffic cops act as watchful guardians for your system, ensuring that it operates
at peak performance day and night.

### Load balancer

A type of `reverse proxy` that distributes traffic across servers. Load
balancers can be found in many parts of a system, from the DNS layer all the
way to the database layer.

### Server-selection strategy

How a `load balancer` chooses servers when distributing traffic amongst
multiple servers. Commonly used strategies include round-robin, random
selection, performance-based selection (choosing the server with the best
performance metrics, like the fastest response time or the least amount of
traffic), and IP-based routing.

### Hot Spot

When distributing a workload across a set of servers, that workload might be
spread unevenly. This can happen if your `sharding key` or your `hashing function`
are suboptimal, or if your workload is naturally skewed: some servers will
receive a lot more traffic than others, thus creating a "hot spot".

## Hashing

Hashing? Like from hash tables? Should be simple enough, right?

The good news is that, yes, hashing like from hash tables.

The bad news is that, no, not simple enough. The video duration and thumbnail should be ominously indicative.

### Consistent hashing

A type of hashing that minimizes the number of keys that need to be remapped
when a hash table gets resized. It's often used by load balancers to
distribute traffic to servers; it minimizes the number of requests that get
forwarded to different servers when new servers are added or when existing
servers are brought down.

### Rendezvous Hashing

A type of hashing also coined `highest random weight` hashing. Allows for
minimal re-distribution of mappings when a server goes down.

### SHA

Short for "Secure Hash Algorithms", the SHA is a collection of cryptographic
hash functions used in the industry. These days, SHA-3 is a popular choice to
use in a system.

## Relational Databases

Tables and ACID.

No, we're not describing a drug lord's desk, but rather referring to key properties of relational databases. There's a lot of material to cover here, so hit the play button, kick back, and get ready to store tons of knowledge in the biggest database of them all: your brain.

### Relational database

A type of structured database in which data is stored following a tabular
format; often supports powerful querying using SQL.

### Non-relational database

In contrast with relational database (SQL databases), a type of database that
is free of imposed, tabular-like structure. Non-relational databases are often
referred to as NoSQL databases.

### SQL

Structured Query Language. Relational databases can be used using a derivative
of SQL such as PostgreSQL in the case of Postgres.

### SQL database

Any database that supports SQL. This term is often used synonymously with
"Relational Database", though in practice, not `every` relational
database supports SQL.

### NoSQL database

Any database that is not SQL-compatible is called NoSQL.

### ACID Transaction

A type of database transaction that has four important properties:

- Atomicity: The operations that constitute the transaction will either
all succeed or all fail. There is no in-between state.

- Consistency: The transaction cannot bring the database to an invalid
state. After the transaction is committed or rolled back, the rules for each
record will still apply, and all future transactions will see the effect of
the transaction. Also named `Strong Consistency`.

- Isolation: The execution of multiple transactions concurrently will
  have the same effect as if they had been executed sequentially.

- Durability: Any committed transaction is written to non-volatile
storage. It will not be undone by a crash, power loss, or network partition.

### Database index

A special auxiliary data structure that allows your database to perform
certain queries much faster. Indexes can typically only exist to reference
structured data, like data stored in relational databases. In practice, you
create an index on one or multiple columns in your database to greatly speed
up `read` queries that you run very often, with the downside of slightly
longer `writes` to your database, since writes have to also take place in
the relevant index.

### Strong consistency

Strong Consistency usually refers to the consistency of ACID transactions,
as opposed to `Eventual Consistency`.

### Eventual consistency

A consistency model which is unlike `Strong Consistency`. In this model,
reads might return a view of the system that is stale. An eventually
consistent datastore will give guarantees that the state of the database will
eventually reflect writes within a time period (could be 10 seconds, or
minutes).

### Postgres

A relational database that uses a dialect of SQL called PostgreSQL. Provides
ACID transactions.

## Key-Value Stores

One of the most commonly used NoSQL paradigms today, the key-value store bases its data model on the associative array data type.

The result? A fast, flexible storage machine that resembles a hash table. That's right folks, our favorite friendly neighborhood data structure strikes again!

### Key-value store

A Key-Value Store is a flexible NoSQL database that's often used for caching
and dynamic configuration. Popular options include DynamoDB, Etcd, Redis, and
ZooKeeper.

### Etcd

Etcd is a strongly consistent and highly available key-value store that's
often used to implement leader election in a system.

### Redis

An in-memory key-value store. Does offer some persistent storage options but is
typically used as a really fast, best-effort caching solution. Redis is also often
used to implement `rate limiting`.

### ZooKeeper

ZooKeeper is a strongly consistent, highly available key-value store. It's
often used to store important configuration or to perform leader election.

## Specialized Storage Paradigms

### Blob storage

Widely used kind of storage, in small and large scale systems. They don’t
really count as databases per se, partially because they only allow the user
to store and retrieve data based on the name of the blob. This is sort of like
a key-value store but usually blob stores have different guarantees. They
might be slower than KV stores but values can be megabytes large (or sometimes
gigabytes large). Usually people use this to store things like
`large binaries, database snapshots, or images` and other static assets
that a website might have.

Blob storage is rather complicated to have on premise, and only giant
companies like Google and Amazon have infrastructure that supports it. So
usually in the context of System Design interviews you can assume that you
will be able to use `GCS` or `S3`. These are blob storage services
hosted by Google and Amazon respectively, that cost money depending on how
much storage you use and how often you store and retrieve blobs from that
storage.

### Time Series Database

A `TSDB` is a special kind of database optimized for storing and
analyzing time-indexed data: data points that specifically occur at a given
moment in time. Examples of TSDBs are InfluxDB, Prometheus, and Graphite.

### Graph database

A type of database that stores data following the graph data model. Data
entries in a graph database can have explicitly defined relationships, much
like nodes in a graph can have edges.

Graph databases take advantage of their underlying graph structure to perform
complex queries on deeply connected data very fast.

Graph databases are thus often preferred to relational databases when dealing
with systems where data points naturally form a graph and have multiple levels
of relationships—for example, social networks.

### Cypher

A `graph query language` that was originally developed for the Neo4j
graph database, but that has since been standardized to be used with other
graph databases in an effort to make it the "SQL for graphs."

Cypher queries are often much simpler than their SQL counterparts. Example
Cypher query to find data in `Neo4j`, a popular graph database:

```
MATCH (some_node:SomeLabel)-[:SOME_RELATIONSHIP]-&gt;(some_other_node:SomeLabel {some_property:'value'})
```

### Spatial Database

A type of database optimized for storing and querying spatial data like
locations on a map. Spatial databases rely on spatial indexes like
`quadtrees` to quickly perform spatial queries like finding all
locations in the vicinity of a region.

### Quadtree

A tree data structure most commonly used to index two-dimensional spatial
data. Each node in a quadtree has either zero children nodes (and is therefore
a leaf node) or exactly four children nodes.

A quadtree lends itself well to storing spatial data because it can be
represented as a grid filled with rectangles that are recursively subdivided
into four sub-rectangles, where each quadtree node is represented by a
rectangle and each rectangle represents a spatial region. Assuming we're
storing locations in the world, we can imagine a quadtree with a maximum
node-capacity `n` as follows:

The root node, which represents the entire world, is the outermost
rectangle.

If the entire world has more than `n` locations, the outermost
rectangle is divided into four quadrants, each representing a region of the
world.

So long as a region has more than `n` locations, its corresponding
rectangle is subdivided into four quadrants (the corresponding node in the
quadtree is given four children nodes).

Regions that have fewer than `n` locations are undivided rectangles
(leaf nodes).

The parts of the grid that have many subdivided rectangles represent densely
populated areas (like cities), while the parts of the grid that have few
subdivided rectangles represent sparsely populated areas (like rural areas).

Finding a given location in a perfect quadtree is an extremely fast operation
that runs in `log4(x)` time (where `x` is the total
number of locations), since quadtree nodes have four children nodes.

### Google Storage

GCS is a blob storage service provided by Google.

### S3

S3 is a blob storage service provided by Amazon through `Amazon Web Services (AWS)`.

### InfluxDB

A popular open-source time series database.

### Prometheus

A popular open-source time series database, typically used for monitoring purposes.

### Neo4j

A popular graph database that consists of `nodes`, `relationships`,
`properties`, and `labels`.

## Replication And Sharding

A system's performance is often only as good as its database's; optimize the
latter, and watch as the former improves in tandem!

On that note, in this video we'll examine how data redundancy and data partitioning
techniques can be used to enhance a system's fault tolerance, throughput, and
overall reliability.

### Replication

The act of duplicating the data from one database server to others. This
is sometimes used to increase the redundancy of your system and
tolerate regional failures for instance. Other times you can use
replication to move data closer to your clients, thus decreasing
the latency of accessing specific data.

### Sharding

Sometimes called `data partitioning`, sharding is the
act of splitting a database into two or more pieces called
`shards` and is typically done to increase the throughput
of your database. Popular sharding strategies include:

- Sharding based on a client's region.
- Sharding based on the type of data being stored (e.g: user data gets
stored in one shard, payments data gets stored in another shard)
- Sharding based on the hash of a column (only for structured data).

### Hot spot

When distributing a workload across a set of servers, that workload might be
spread unevenly. This can happen if your `sharding key` or your `hashing function`
are suboptimal, or if your workload is naturally skewed: some servers will
receive a lot more traffic than others, thus creating a "hot spot".
