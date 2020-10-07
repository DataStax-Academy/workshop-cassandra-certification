## 🎓🔥 Apache Cassandra™ Certification Workshop 🔥🎓

[![License Apache2](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)
[![Discord](https://img.shields.io/discord/685554030159593522)](https://discord.com/widget?id=685554030159593522&theme=dark)

This section will run you through a set of practice exam questions. We will split them into a set from DS201 (Developer), DS220 (Data Modeling), and DS210 (Administrator). 

## Table of Contents

| Title  | Description
|---|---|
| **1. CQL - upserts** | [CQL - upserts](#1-cql---upserts) |
| **2. CQL - partition keys** | [CQL - partition keys](#2-cql---partition-keys) |
| **3. CQL - clustering keys** | [CQL - clustering keys](#3-cql---clustering-keys) |

## 1. CQL - upserts
#### Consider the CQL statements:
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

#### How many rows will the roller_coasters table have after executing all the CQL statements?

**A.** none

**B.** 2

**C.** 3

**D.** 4


[🏠 Back to Table of Contents](#table-of-contents)


## 2. CQL - partition keys
#### Consider the CQL statements:
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

#### What is the result of executing all the CQL statements?

**A.** A table with 1 partition. 

**B.** A table with 2 partitions.

**C.** A table with 3 partitions.

**D.** A table with 4 partitions.


[🏠 Back to Table of Contents](#table-of-contents)


## 3. CQL - clustering keys
#### Consider the CQL statement:
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

#### Which of the following is a valid query for the cars table?

**A.** 
```
SELECT * from cars 
  where make='Ford';
```

**B.** 
```
SELECT * from cars 
  where make='Ford' 
  and model = 'Mustang';
```

**C.** 
```
SELECT * from cars 
  where make='Ford' 
  and model = 'Mustang' 
  and year = 1969;
```

**D.** 
```
SELECT * from cars 
  where make='Ford' 
  and model = 'Mustang' 
  and color = 'Red';
```

[🏠 Back to Table of Contents](#table-of-contents)