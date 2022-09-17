# Knowing the CQL

Communication with the database is certainly the most trivial thing in a database.
Cassandra offers its language for communicating with the database, *Cassandra Query language,* or CQL. CQL has a syntax close to SQL, however, in a simpler way since there are no concepts like *joins* (*inner join*, *left join*, among others) within Cassandra's searches. A developer who already knows SQL will have a much smaller learning curve to learn this Cassandra language.
This chapter will aim to talk a little about this language.


## Keyspace

```sql
CREATE KEYSPACE library WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};
```

## Column family

```sql
CREATE TABLE library.book (
    name text PRIMARY KEY,
       year int
);
```

```sql
DROP TABLE IF EXISTS library.book;
```

```sql
CREATE TABLE IF NOT EXISTS library.book (
    name text PRIMARY KEY,
       year int
);
INSERT INTO library.book JSON '{"name": "Effective Java", "year": 2001}';
INSERT INTO library.book JSON '{"name": "Clean Code", "year": 2008}';

SELECT * FROM library.book;
```



