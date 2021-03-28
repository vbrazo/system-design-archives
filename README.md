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
