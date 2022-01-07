---
layout: post
title: My Database Theory Handbook
author: Jeffrey Tse
banner:
  image: https://wallpaperbat.com/img/397879-building-wallpaper-top-free-building-background.jpg
  opacity: 0.418
categories: computer
tags:
  - computer
  - database
  - note
---

## History

### SQL-92 Standard

It's tied to the relational idea, and consists of 2 important sub ideas.

1.Relational Data Model (Schema Design)

- "Atomic" types (Domain)
  - Table with rows and columns consist of cells
  - Each cell is one value of an atomic type (string, number, date...)
- Schema independent of processing purposes
  - "Normalization" (Very crucial)
    - It should be normalized away from what you want to do with the data,
      because quite often you don't know yet what you gonna to do with the data

Following these two rules makes you end up with a schema design where you have
your data spread across many tables.

2.Relational operations

- Transform data for each particular processing purposes
  - JOIN, UNION, Nesting...

These transformation steps help you to transform the normalized persistent data
into something that is more suitable in our client application for different
business.This is the important idea of what SQL is actually the key idea behind
SQL.

### SQL-99 Standard

It escaped the relational cage, SQL is not limited to the relational model
anymore. This SQL:1999 extensions are mere "extended interpretations" of the
relational data model is like saying that an intercontinental ballistic missile
is merely an "extended interpretation" of a spear.

With SQL/99 you can get the best of both worlds and of course, you can get the
worst of both worlds. It's up to the the database practitioners to do the right
thing.

![Christopher J. Date](https://upload.wikimedia.org/wikipedia/commons/8/81/Cdate2.jpg)

Writings 2000-2006 by Christopher J. Date (Date on Database)

> I was as confused as anyone else. By the early 1990s, however, I'd seen the
> light.
> Domain can contain everything!

1.Relational Data Model?

- Introduced rich types

  - Arrays
  - Nested tables (multiset)
  - Composite types (objects)

    2.Non-relational Operations

- Introduced recursive queries that process their own output
  - Transitive closure

### SQL-2016 Standard

1.Json type

- SQL/JSON Path
  - Query language to select elements from a JSON document (a very same purpose
    like XPath for XML or CSS selectors for HTML)
  - Defined in the SQL standard

### What's more?

- A lot has happened since SQL-92
- SQL has evolved beyond the relational idea
- If you use SQL for CRUD operations only, you are doing it wrong

## Index

### Clustered and Non-clustered Index

By the storage structure, there are only two types of indices.

1. Clustered Index
2. Non-clustered Index (Similar to the index of a book)

There are the following differences between clustered and non-clustered indexes.

- A table can have only one clustered index. However, you can have multiple
  non-clustered indexes.
- Clustered indexes are faster than non-clustered indexes since they don’t
  involve any extra lookup step.
- Clustered indexes require less memory for operations than non-clustered index.
- In clustered indexes, indexes are the main data. In non-clustered indexes,
  indexes are the copy of data.
- Clustered indexes have inherent ability of storing data on the disk, but
  non-clustered indexes don't have the ability.
- Clustered indexes store pointers to block not data. Non-clustered indexes
  store both value and a pointer to actual row that holds data.
- In clustered indexes leaf nodes are actual data itself. In non-clustered
  indexes leaf nodes are not the actual data itself rather they only contain
  included columns.
- In clustered indexes, a clustered key define order of data within table. In
  non-clustered indexes, a index key defines order of data within index.
- A clustered index is a type of index in which table records are physically
  reordered to match the index. A non-clustered index is a special type of
  index in which logical order of index does not match physical stored order
  of the rows on disk.
- Clustered indexes only sort tables. Therefore, they do not consume extra
  storage. Non-clustered indexes are stored in a separate place from the
  actual table claiming more storage space.

...

## Database Replication

By scale:

- Incremental table replication
- Full table

By method:

- Log-based
- Trigger-based
- Key-based

## References

- [Use the index, luke! A Guide to Database Performance for Developers](https://use-the-index-luke.com/)
- [Difference between Clustered and Non-clustered index](https://www.geeksforgeeks.org/difference-between-clustered-and-non-clustered-index/)
