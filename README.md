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
