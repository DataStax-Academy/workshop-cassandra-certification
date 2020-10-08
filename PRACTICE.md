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
|---|
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
|---|
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
  AND coolor = 'Red';
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
|---|
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
|---|
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
|---|
</p>
</details>

[⬆️ Top](#sample-questions)

### 6. CQL - Developer and Administrator Exams
Consider the table definition and ``SELECT`` statement:
```
CREATE TABLE teams (
    name TEXT,
    wins INT,
    losses INT,
    ties INT,
);

SELECT * FROM teams_by_wins WHERE wins = 4;
```
Which materialized view definition can be used to support this ``SELECT``?

**A.** 
```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * from teams
      PRIMARY KEY((wins), name);
```
**B.**
```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * from teams
      PRIMARY KEY((name), wins);
```
**C.**

```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * from teams
      WHERE name IS NOT NULL AND wins IS NOT NULL
      PRIMARY KEY((wins), name);
```
**D.**
```
CREATE MATERIALIZED VIEW IF NOT EXISTS
    teams_by_wins AS
    SELECT * from teams
      WHERE name IS NOT NULL AND name IS NOT NULL
      PRIMARY KEY((name), wins);
```

<details><summary>Click to view the correct answer</summary>
<p>

| The correct answer is D |
|---|
</p>
</details>

[⬆️ Top](#sample-questions)
