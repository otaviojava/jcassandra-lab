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
