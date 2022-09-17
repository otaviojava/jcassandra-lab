# BATCH

`BATCH` allows multiple change operations (INSERT, UPDATE, and DELETE). The operations within a `BATCH` aim to perform several operations in an atomic way, that is, the operation happens or not.


```sql
BEGIN BATCH
INSERT INTO library.librarian JSON '{"name": "Ivar", "id": "ivar"}';
INSERT INTO library.librarian JSON '{"name": "Daniel Dias", "id": "dani"}';
INSERT INTO library.librarian JSON '{"name": "Gabriela Santana", "id": "gabriela"}';
DELETE FROM library.librarian where id = 'dani';
APPLY BATCH;
```

## List


```sql
CREATE TABLE IF NOT EXISTS library.reader (
    name text,
    books list <text>,
    PRIMARY KEY (name)
);

INSERT INTO library.reader (name, books) VALUES ('Poliana', ['The Shack', 'The Love', 'Clean Code']);
INSERT INTO library.reader (name, books) VALUES ('David', ['Clean Code', 'Effectove Java', 'Clean Code']);

SELECT * FROM library.reader;
```

## Set

Set is similar to List, however, it does not allow duplicate values. Thus, the same example mentioned above, but with Set, would be:

Creation of the column family of readers (this time, it is possible to see that the book “Clean Code” by reader “David” will not appear).

```sql
DROP TABLE IF EXISTS library.reader;

CREATE TABLE IF NOT EXISTS library.reader (
    name text,
    books set <text>,
    PRIMARY KEY (name)
);

INSERT INTO library.reader (name, books) VALUES ('Poliana', {'The Shack', 'The Love', 'Clean Code'});
INSERT INTO library.reader (name, books) VALUES ('David', {'Clean Code', 'Effectove Java', 'Clean Code'});

SELECT * FROM library.reader;
```

## Map

The map follows the line of a data dictionary or a `java.util.Map`, if the reader is from the Java world. Given the previous example from readers, let's assume that you want to add contact information. See the code below.

```sql
DROP TABLE IF EXISTS library.reader;

CREATE TABLE IF NOT EXISTS library.reader (
    name text,
    books set <text>,
    contacts map <text, text>,
    PRIMARY KEY (name)
);
INSERT INTO library.reader (name, books, contacts) VALUES ('Poliana', {'The Shack', 'The Love', 'Clean Code'},
{'email': 'poliana@email.com', 'phone': '+1 55 486848635', 'twitter': 'polianatwitter', 'facebook': 'polianafacebook'});
INSERT INTO library.reader (name, books, contacts) VALUES ('David', {'Clean Code'}, {'email': 'david@email.com'
, 'phone': '+1 55 48684865', 'twitter': 'davidtwitter'});

SELECT * FROM library.reader;

```
