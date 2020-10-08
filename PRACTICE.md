## 🎓🔥 Apache Cassandra™ Certification Workshop 🔥🎓

[![License Apache2](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)
[![Discord](https://img.shields.io/discord/685554030159593522)](https://discord.com/widget?id=685554030159593522&theme=dark)

This section will run you through a set of practice exam questions. We will split them into a set from DS201 (Developer), DS220 (Data Modeling), and DS210 (Administrator). 

## Sample Questions

| Question/Topic | Exam(s)
|---|---|
| **[1. CQL](#1-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[2. CQL](#2-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[3. CQL](#3-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[4. CQL](#4-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[5. CQL](#5-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[6. CQL](#6-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[7. CQL](#7-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[8. CQL](#8-cql---developer-and-administrator-exams)** | Developer and Adminisrator |
| **[9. CQL](#9-cql---developer-and-administrator-exams)** | Developer and Adminisrator |

### 1. CQL - Developer and Administrator Exams
Consider the CQL statements:
```
CREATE TABLE roller_coasters (
    name TEXT,
    park TEXT,
    rating INT,
    PRIMARY KEY((name))
);

INSERT INTO roller_coasters (name, park, rating) 
  VALUES ('Millenium Force', 'Cedar Point', 8 );

INSERT INTO roller_coasters (name, park, rating) 
  VALUES ('Formula Rossa', 'Ferrari World', 9 );

INSERT INTO roller_coasters (name, park, rating) 
  VALUES ('Steel Dragon 2000', 'Nagashima Spa Land', 10 );

INSERT INTO roller_coasters (name, park, rating) 
  VALUES ('Millenium Force', 'Cedar Point', 7 );
```

How many rows will the ``roller_coasters`` table have after executing all the CQL statements?

**A.** none

**B.** 2

**C.** 3

**D.** 4

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is C |
| :--- |
| The first and fourth ``INSERTS`` use the same primary key so they cause an *upsert*. Therefore only 3 rows are created. |
</p>
</details>

[⬆️ Top](#sample-questions)

### 2. CQL - Developer and Administrator Exams
Consider the CQL statements:
```
CREATE TABLE songs (
    artist TEXT,
    title TEXT,
    length_seconds INT,
    PRIMARY KEY((artist, title))
);

INSERT INTO songs (artist, title, length_seconds) 
  VALUES ('The Beatles', 'Yesterday', 123 );

INSERT INTO songs (artist, title, length_seconds) 
  VALUES ('The Beatles', 'Let It Be', 243 );

INSERT INTO songs (artist, title, length_seconds) 
  VALUES ('Abba', 'Fernando', 255 );

INSERT INTO songs (artist, title, length_seconds) 
  VALUES ('Frank Sinatra', 'Yesterday', 235 );
```

What is the result of executing all the CQL statements?

**A.** A table with 1 partition. 

**B.** A table with 2 partitions.

**C.** A table with 3 partitions.

**D.** A table with 4 partitions.

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is D |
| :--- |
| The primary key consists of ``artist`` *and* ``title``. Each ``INSERT`` has a unique ``artist``/``title`` pair so there are no *upserts* and each ``INSERT`` results in a unique partition. |
</p>
</details>

[⬆️ Top](#sample-questions)

### 3. CQL - Developer and Administrator Exams
Consider the CQL statement:
```
CREATE TABLE cars (
    make TEXT,
    model TEXT,
    year INT,
    color TEXT,
    cost INT,
    PRIMARY KEY ((make, model), year, color)
);
```

Which of the following is a valid query for the cars table?

**A.** 
```
SELECT * FROM cars 
  WHERE make='Ford';
```

**B.** 
```
SELECT * FROM cars 
  WHERE year = 1969 
  AND color = 'Red';
```

**C.** 
```
SELECT * FROM cars 
  WHERE make='Ford' 
  AND model = 'Mustang' 
  AND year = 1969;
```

**D.** 
```
SELECT * FROM cars 
  WHERE make='Ford' 
  AND model = 'Mustang' 
  AND color = 'Red';
```

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is C |
| :--- |
| The primary key consists of ``make`` *and* ``model`` so **A** and **B** are excluded because the ``WHERE`` clause does not include the primary key. **C** and **D** both include the primary key but clustering columns can only be *constrained* L-R in the order they appear in the primary key. Since ``year`` appears before ``color``, **C** is correct and **D** is excluded. |
</p>
</details>

[⬆️ Top](#sample-questions)

### 4. CQL - Developer and Administrator Exams
Consider the CQL statements:
```
CREATE TABLE employees (
    id TEXT,
    name TEXT,
    department TEXT,
    PRIMARY KEY ((id))
);

CREATE TABLE employees_by_department (
    id TEXT,
    name TEXT,
    department TEXT,
    PRIMARY KEY ((department), id)
);

BEGIN BATCH
    INSERT INTO employees (id, name, department) 
      VALUES ('AC1123', 'Joe', 'legal');

    INSERT INTO employees_by_department (id, name, department)
      VALUES ('AC1123', 'Joe', 'legal');
APPLY BATCH;
```
What is a valid statement about this atomic batch?

**A.** It is a single-partition batch that can be applied.

**B.** It is a single-partition batch that cannot be applied.

**C.** It is a multi-partition batch that can be applied.

**D.** It is a multi-partition batch that cannot be applied.

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is C |
| :--- |
| The two ``INSERTS`` are into different tables which makes them different partitions. Even if one or both result in *upserts* there is nothing preventing this batch from being applied. Inserting the same data into *de-normalized* tables is a common use case for CQL Batches. |
</p>
</details>

[⬆️ Top](#sample-questions)

### 5. CQL - Developer and Administrator Exams
Consider the table definition with a primary key ommitted:
```
CREATE TABLE restaurant_reviews {
    name TEXT,
    city TEXT,
    reviewer TEXT,
    rating INT,
    comments TEXT,
    review_date TIMEUUID,
    PRIMARY KEY (...)
}
```
It is known that:
- Restaurant Reviews are uniquely identified by a combination of ``name``, ``city`` and ``reviewer``
- Restaurant Reviews are retrieved from the table using combination of ``name``, ``city``
- The table has multi-row partitions

What primary key does this table have?

**A.** 
```PRIMARY KEY((name), city, reviewer)```

**B.** 
```PRIMARY KEY((name, city), reviewer)```

**C.** 
```PRIMARY KEY((name, reviewer), city)```

**D.** 
```PRIMARY KEY(name, city, reviewer)```

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is B |
| :--- |
| Since Restaurant Reviews are uniquely identified by a combination of ``name``, ``city`` and ``reviewer`` the primary key must include all three fields. Since Restaurant Reviews are retrieved from the table using combination of ``name``, ``city``, these two fields must comprise the *partition key*. Since this table has multi-row partitionsand ``reviewer`` is part of the primary key, it must be a clustering column.|
</p>
</details>

[⬆️ Top](#sample-questions)

### 6. CQL - Developer and Administrator Exams
Consider the table definition and the CQL query:
```
CREATE TABLE teams (
    name TEXT,
    wins INT,
    losses INT,
    ties INT,
);

SELECT * FROM teams_by_wins WHERE wins = 4;
```
Which materialized view definition can be used to support the qeury?

**A.** 
```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * FROM teams
      PRIMARY KEY((name), wins);
```
**B.**
```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * FROM teams
      PRIMARY KEY((wins), name);
```
**C.**

```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * FROM teams
      WHERE name IS NOT NULL AND wins IS NOT NULL
      PRIMARY KEY((name), wins);
```
**D.**
```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * FROM teams
      WHERE name IS NOT NULL AND name IS NOT NULL
      PRIMARY KEY((wins), name);
```

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is D |
|:---|
| Since primary key fields cannot be NULL the ``WHERE`` clause must include a *NULL check*. Since the ``WHERE`` clause in the ``SELECT`` is based on ``wins``, ``wins`` must be the partition key. |
</p>
</details>

[⬆️ Top](#sample-questions)

### 7. CQL - Developer and Administrator Exams
Consider the table definition and the CQL query:
```
CREATE TABLE restaurants_by_city (
    name TEXT,
    city TEXT,
    cuisine TEXT,
    price int,
    PRIMARY KEY ((city), name)
);

SELECT * FROM restaurants_by_city
  WHERE city = 'Sydney'
  AND cuisine = 'sushi';
```  
Which secondary index can be used to support the query?

**A.** 
```
CREATE INDEX cuisine_restaurants_by_city_2i
  ON restaurants_by_city (cuisine);
```
**B.**

```
CREATE INDEX cuisine_restaurants_by_city_2i
  ON restaurants_by_city (city, cuisine);
```
**C.**

```
CREATE INDEX cuisine_restaurants_by_city_2i
  ON restaurants_by_city (cuisine, city);
```
**D.**

```
CREATE INDEX cuisine_restaurants_by_city_2i
  ON restaurants_by_city (city, name, cuisine);
```
<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is A |
|:---|
| The secondary index only needs to specify the field(s) (besides the partition key) that will appear in the ``WHERE`` clause. |
</p>
</details>

[⬆️ Top](#sample-questions)

### 8. CQL - Developer and Administrator Exams
Which statement describes the ``WHERE`` clause in a query?

**A.** ``WHERE`` clauses must reference all the fields of the partition key.

**B.** ``WHERE`` clauses must reference all the fields of the clustering key.

**C.** ``WHERE`` clauses must reference all the fields of the primary key.

**D.** ``WHERE`` clauses must reference all the fields of the primary key and clustering key.

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is A |
|:---|
| Only the fields of the partition key are required. This insures the *partition-per-query* pattern. |
</p>
</details>

[⬆️ Top](#sample-questions)

### 9. CQL - Developer and Administrator Exams
Consider the CQL statements:
```
CREATE TYPE name (
    first TEXT,
    last TEXT
);

CREATE TABLE people (
    id UUID,
    name NAME,
    email TEXT,
    PRIMARY KEY(id, email)
);
```
Which ``INSERT`` statement can be used to insert a row in the ``people`` table?
**A.**
```
INSERT INTO people (id, name, email) 
  VALUES (UUID(), {first:'foo', last:'bar'}, 'foo@datastax.com' );
```
**B.**
```
INSERT INTO people (id, name, email) 
  VALUES (UUID(), name: {'foo', 'bar'}, 'foo@datastax.com' );
```
**C.**
```
INSERT INTO people (id, name, email) 
  VALUES (UUID(), 'foo', 'bar', 'foo@datastax.com' );
```
**D.**
```
INSERT INTO people (id, name, email) 
  VALUES (UUID(), ('foo', 'bar), 'foo@datastax.com' );
```

| The correct answer is A |
|:---|
| The fields of the userdefined type are passed using JSON. |
</p>
</details>

[⬆️ Top](#sample-questions)

