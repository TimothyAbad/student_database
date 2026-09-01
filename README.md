# Student Relational Database Management System

A robust relational database schema designed to track and manage institutional student registrations, course assignments, and enrollment metrics. This project outlines clean relational structures, data integrity constraints, and multi-table query executions using SQLite.

## 📖 Project Origins
The foundational architecture, business rules, and relational tracking principles utilized in this schema were learned and adapted from the structural methodologies taught by **Alps Academy** (*How to Design a Database Using an ERD*).

## 🛠️ Tech Stack & Concepts
*   **Database Engine:** SQLite (Relational Database Model)
*   **Design Paradigm:** Entity-Relationship Modeling (ERD), Table Normalization, Data Integrity
*   **Core Concepts:** Primary Keys, Foreign Keys, Referential Integrity, Data Type Constraints

---

## 📐 Database Schema & Architecture

The database is normalized to eliminate data redundancy and prevent operational anomalies. It is engineered around three primary entities:

### 1. `students` Table
Tracks unique student identities and profiles.
*   `student_id` (INTEGER, Primary Key): Unique institutional identifier.
*   `student_name` (TEXT): Full name of the registered student.

### 2. `courses` Table
Maintains catalog data for available academic tracks.
*   `course_code` (INTEGER, Primary Key): Unique identifier for the course.
*   `course_name` (TEXT): Academic title of the class.

### 3. `registrations` Table
An associative (junction) table managing the many-to-many relationship between students and courses.
*   `student_id` (INTEGER, Foreign Key REFERENCES `students`)
*   `course_code` (INTEGER, Foreign Key REFERENCES `courses`)
*   `registration_date` (TEXT): Tracks timestamp/semester records.

---

## 💻 Sample SQL Implementations

### Table Creation (DDL)
```sql
CREATE TABLE students (
    student_id INTEGER PRIMARY KEY,
    student_name TEXT NOT NULL
);

CREATE TABLE courses (
    course_code INTEGER PRIMARY KEY,
    course_name TEXT NOT NULL
);

CREATE TABLE registrations (
    student_id INTEGER,
    course_code INTEGER,
    registration_date TEXT NOT NULL,
    PRIMARY KEY (student_id, course_code),
    FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE,
    FOREIGN KEY (course_code) REFERENCES courses(course_code) ON DELETE CASCADE
);
```

### Advanced Query: Relational Data Fetch (DML)
To aggregate and view complete enrollment schedules across tables using explicit inner joins:
```sql
SELECT 
    s.student_id, 
    s.student_name, 
    c.course_code, 
    c.course_name, 
    r.registration_date
FROM registrations r
INNER JOIN students s ON r.student_id = s.student_id
INNER JOIN courses c ON r.course_code = c.course_code
ORDER BY r.registration_date DESC, s.student_name ASC;
```

---

## 🚀 Key Database Strengths Demonstrated
*   **Data Integrity Enforced:** Uses relational keys to guarantee that invalid student IDs or duplicate enrollment records cannot be inserted into the system accidentally.
*   **Scalability Ready:** The modular schema allows the database to easily scale from a few dozen records to thousands of active entries seamlessly.
*   **Performance Optimization:** Composite primary indexing on the associative mapping table ensures lightning-fast join queries across deep data tables.

