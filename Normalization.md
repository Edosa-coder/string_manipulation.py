# SQL Database Normalization and Data Types

## 1. What is Normalization?

**Database normalization** is the process of organizing data in a database to:

- Reduce **duplicate/repeated data**
- Prevent **data inconsistency**
- Make the database easier to **maintain**
- Make it easier to **insert, update, and delete** data correctly

### Example of an Unnormalized Table



| Student | Course | Lecturer |
|---|---|---|
| John | Database | Mr. Ade |
| John | JavaScript | Mr. Mike |
| Mary | Database | Mr. Ade |



Instead of storing everything in one large table, it can be separated.

### Students

| student_id | name |
|---|---|
| 1 | John |
| 2 | Mary |

### Courses

| course_id | course_name | lecturer |
|---|---|---|
| 1 | Database | Mr. Ade |
| 2 | JavaScript | Mr. Mike |

### Student_Courses

| student_id | course_id |
|---|---|
| 1 | 1 |
| 1 | 2 |
| 2 | 1 |

Now each piece of information is stored in the appropriate place.

### Common Normal Forms

#### 1NF — First Normal Form

- Each column contains a single/atomic value.
- No repeating groups.

#### 2NF — Second Normal Form

- Must already be in 1NF.
- Every non-key column must depend on the **whole primary key**.

#### 3NF — Third Normal Form

- Must already be in 2NF.
- Non-key columns should depend only on the primary key, not on another non-key column.

For most beginner database work, **1NF → 2NF → 3NF** is the main progression to understand.

---

# 2. SQL Data Types

A **data type** tells the database what kind of information a column is allowed to store.

For example:

```sql
name VARCHAR(100)
age INT
price DECIMAL(10,2)
is_active BOOLEAN
```

Here are the major SQL data types.

## A. String/Text Types

Used for text.

### VARCHAR

```sql
name VARCHAR(100)
```

Stores variable-length text.

Examples:

```text
"Samuel"
"John Doe"
```

### CHAR

```sql
gender CHAR(1)
```

Stores fixed-length text.

Examples:

```text
"M"
"F"
```

### TEXT

Used for larger amounts of text.

```sql
description TEXT
```

---

## B. Integer/Numeric Types

Used for whole numbers.

### INT

```sql
age INT
```

Examples:

```text
18
25
40
100
```

Other numeric types include:

- `TINYINT`
- `SMALLINT`
- `MEDIUMINT`
- `INT`
- `BIGINT`

The main difference is the range of numbers they can store.

---

## C. Decimal Types

Used when you need numbers with decimal places.

### DECIMAL

```sql
price DECIMAL(10,2)
```

This means:

- Maximum **10 digits**
- **2 digits** after the decimal point

Examples:

```text
1500.50
250.75
99.99
```

`DECIMAL` is particularly useful for **money** because it provides exact decimal precision.

---

## D. Floating-Point Types

### FLOAT

```sql
temperature FLOAT
```

### DOUBLE

```sql
distance DOUBLE
```

These are useful for approximate decimal values, scientific calculations, measurements, etc.

---

## E. Date and Time Types

### DATE

```sql
date_of_birth DATE
```

Example:

```text
2000-05-15
```

### TIME

```sql
start_time TIME
```

Example:

```text
14:30:00
```

### DATETIME

```sql
created_at DATETIME
```

Example:

```text
2026-09-07 14:30:00
```

### TIMESTAMP

Also stores date and time and is commonly used for things such as:

```sql
created_at TIMESTAMP
updated_at TIMESTAMP
```

---

## F. Boolean

Used for true/false values.

```sql
is_verified BOOLEAN
```

Values can conceptually be:

```text
TRUE
FALSE
```

In MySQL, `BOOLEAN` is essentially an alias for `TINYINT(1)`.

---

## G. Binary Types

Used for binary data.

Examples include:

```sql
BINARY
VARBINARY
BLOB
```

`BLOB` can be used for binary data such as images or files, although applications often store the **file URL/path** in the database instead.

---

# Quick Cheat Sheet

| Data Type | Used For | Example |
|---|---|---|
| `INT` | Whole numbers | `25` |
| `BIGINT` | Very large whole numbers | `9000000000` |
| `VARCHAR` | Short/medium text | `"Samuel"` |
| `CHAR` | Fixed-length text | `"M"` |
| `TEXT` | Long text | `"This is a description..."` |
| `DECIMAL` | Exact decimals/money | `2500.50` |
| `FLOAT` | Approximate decimals | `3.14` |
| `DOUBLE` | Larger floating values | `3.141592` |
| `DATE` | Date | `2026-09-07` |
| `TIME` | Time | `14:30:00` |
| `DATETIME` | Date + time | `2026-09-07 14:30:00` |
| `TIMESTAMP` | Date + time, often for records | `2026-09-07 14:30:00` |
| `BOOLEAN` | True/false | `TRUE` |
| `BLOB` | Binary data | File/image data |

---

# 3. Example: Pulse Point Database

For a Pulse Point database, you might have something like:

```sql
CREATE TABLE donors (
    id INT PRIMARY KEY AUTO_INCREMENT,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    blood_type VARCHAR(5),
    phone_number VARCHAR(20),
    city VARCHAR(100),
    state VARCHAR(100),
    country VARCHAR(100),
    is_available BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Notice how the **data type is chosen based on the kind of data**:

- `id` → `INT`
- `full_name` → `VARCHAR`
- `email` → `VARCHAR`
- `password` → `VARCHAR`
- `blood_type` → `VARCHAR`
- `phone_number` → `VARCHAR`
- `is_available` → `BOOLEAN`
- `created_at` → `TIMESTAMP`

## Key Takeaway

**Normalization** is about **how you organize your tables and relationships** to reduce duplication and maintain data integrity.

**Data types** are about **what kind of values each column can store**.
