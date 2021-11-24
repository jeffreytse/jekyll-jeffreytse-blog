---
layout: post
title: The handbook of Redis
author: Jeffrey Tse
banner:
  image: https://apihoard.webit.com/api/v1/Image/1DD1AE6BFD1B4DFBF98B39813C5C3FF9/1DD1AE6BFD1B4DFBF98B39813C5C3FF9.png?size=1920x1440
  opacity: 0.76
categories: computer
tags:
  - computer
  - software
  - note
---

Redis is an in-memory data structure store, used as a distributed, in-memory
key–value database. Here is an easy handbook for your reference to quickly
start it.

## Setup

You can configure Redis Server by below configuration file.

```bash
sudo vi /etc/redis.conf
```

Redis CLI arguments:

```bash
# Connect to a Redis server (e.g. Default is DB 0)
$ redis-cli [-n db_no]

# Get the version of Redis Client
$ redis-cli -v

# Enable keyspace events notification feature (It consumes lots of CPU resources)
$ redis-cli config set notify-keyspace-events KEA

# Monitor all events notification by CLI
#
#   K     Keyspace events, published with __keyspace@<db>__ prefix.
#   E     Keyevent events, published with __keyevent@<db>__ prefix.
#   g     Generic commands (non-type specific) like DEL, EXPIRE, RENAME, ...
#   $     String commands
#   l     List commands
#   s     Set commands
#   h     Hash commands
#   z     Sorted set commands
#   x     Expired events (events generated every time a key expires)
#   e     Evicted events (events generated when a key is evicted for maxmemory)
#   A     Alias for g$lshzxe, so that the "AKE" string means all the events.
#
$ redis-cli --csv psubscribe '__key*__:*'
Reading messages... (press Ctrl-C to quit)
"psubscribe","__key*__:*",1

# Show statistic of clients
$ redis-cli --stat

# Show keys, the same as `keys *` but it supports Regular Expression
$ redis-cli --scan

# Scanning the entire keyspace to find biggest keys as well as
# average sizes per key type.  You can use -i 0.1 to sleep 0.1 sec
# per 100 SCAN commands (not usually needed).
$ redis-cli --bigkeys

# Monitor all received redis commands
$ redis-cli monitor
```

Redis commands:

```bash
# Test heart beat
127.0.0.1:6379> ping
PONG

# Flush current database (i.e. Delete all keys of current database)
127.0.0.1:6379> flushdb

# Flush all databases (i.e. Delete all keys of all database)
127.0.0.1:6379> flushall

# Get all information of Redis server
127.0.0.1:6379> info

# Get the information of server
127.0.0.1:6379> info server

# Get all configurations
127.0.0.1:6379> config get *

# Get the configuraion of dir
127.0.0.1:6379> config get dir

# Get all keys
127.0.0.1:6379> keys *

# Set expiration for a key
127.0.0.1:6379> expire <key> 3

# Delete a specific key
127.0.0.1:6379> del <key>

# Get the the amount of keys
127.0.0.1:6379> dbsize

# Exit Redis Client
127.0.0.1:6379> exit
```

## Data Operations

### String

```bash
127.0.0.1:6379> set name foo
OK

127.0.0.1:6379> get name
"foo"
```

### Hash

```bash
# Set a new hash (M for multi)
127.0.0.1:6379> hmset king username foo password 12345 age 18
OK

# Get the value of a specific key
127.0.0.1:6379> hget king username
"foo"

# Set a key-value pair (Auto create the key if it doesn't exist)
127.0.0.1:6379> hset king alias "bar"
(integer) 1

# Get all key-value
127.0.0.1:6379> hgetall king
1) "username"
2) "foo"
3) "password"
4) "12345"
5) "age"
6) "18"
7) "alias"
8) "bar

# Delete a key-value pair
127.0.0.1:6379> hdel king alias
(integer) 1
```

### List

```bash
# Push an element to the end of list
127.0.0.1:6379> lpush users foo
(integer) 1

127.0.0.1:6379> lpush users bar
(integer) 2

127.0.0.1:6379> lpush users baz
(integer) 3

# Get the length of list
127.0.0.1:6379> llen users
(integer) 3

# Get a range of elements of list
127.0.0.1:6379> lrange users 0 10
1) "foo"
2) "bar"
3) "baz"
```

### Set

```bash
# Add an element to users set
127.0.0.1:6379> sadd users foo
(integer) 1

127.0.0.1:6379> sadd users bar
(integer) 1

127.0.0.1:6379> sadd users baz
(integer) 1

127.0.0.1:6379> sadd users bar
(integer) 0

# Is a member of the set
127.0.0.1:6379> sismember users bar
(integer) 1

# Get amount of a set
127.0.0.1:6379> scard users
(integer) 3

# List members of a set
127.0.0.1:6379> smembers users
1) "foo"
2) "bar"
3) "baz"

# Remove one or more elements
127.0.0.1:6379> srem users bar baz
(integer) 1
```

### Sorted Set

```bash
# Add an element to users sorted set
127.0.0.1:6379> zadd users 1 foo
(integer) 1

127.0.0.1:6379> zadd users 2 bar
(integer) 1

127.0.0.1:6379> zadd users 3 baz
(integer) 1

127.0.0.1:6379> zadd users 4 baz
(integer) 0

# Get score of an member --> O(1)
127.0.0.1:6379> zscore users bar
(integer) 2

# Check if it's a member of the sorted set
127.0.0.1:6379> zscore users zoo
(nil)

# Get amount of a sorted set
128.0.0.1:6379> scount users
(integer) 3

# List members of a sorted set
127.0.0.1:6379> zrange users 0 10
1) "foo"
2) "bar"
3) "baz"

# List members of a sorted set with scores
127.0.0.1:6379> zrange users 0 10 withscores
1) "foo"
2) "1"
3) "bar"
4) "2"
5) "baz"
6) "4"

# Remove one or more elements
127.0.0.1:6379> zrem users bar baz
(integer) 1
```
