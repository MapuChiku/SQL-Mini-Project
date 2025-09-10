### DAY ☀️: **Mini Project – 3: College Management Database System**  


### 🎯 **Project Title:**  
**College Management Database System**

---

### 🧠 **Objective:**  
To create and manage a real-world college database covering **all core SQL concepts**, from installation to indexing, normalization, joins, subqueries, grouping, filtering, and more.

---

### 🛠️ Step 1: Create Database

```sql
CREATE DATABASE college_db;
USE college_db;
```

---

### 🛠️ Step 2: Create Tables

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    gender VARCHAR(10),
    city VARCHAR(50)
);

CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

CREATE TABLE enrollments (
    enroll_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    marks INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

---

### 🛠️ Step 3: Insert Data

```sql
INSERT INTO students VALUES  
(1, 'Anjali', 20, 'Female', 'Delhi'),  
(2, 'Rahul', 21, 'Male', 'Mumbai'),  
(3, 'Priya', 19, 'Female', 'Chennai'),  
(4, 'Rohan', 22, 'Male', 'Delhi'),  
(5, 'Neha', 20, 'Female', 'Kolkata');

INSERT INTO departments VALUES  
(101, 'Computer Science'),  
(102, 'Electronics'),  
(103, 'Mechanical');

INSERT INTO courses VALUES  
(201, 'DBMS', 101),  
(202, 'SQL Programming', 101),  
(203, 'Circuit Analysis', 102),  
(204, 'Thermodynamics', 103);

INSERT INTO enrollments VALUES  
(301, 1, 201, 88),  
(302, 2, 202, 92),  
(303, 3, 201, 75),  
(304, 4, 203, 60),  
(305, 5, 204, 70);
```

---

### ✅ **Mini Project – 3 Tasks (25 Tasks)**

---

### ⚡ Task 1  
**Question:** List all students from the `students` table.

select * from students;

### ⚡ Task 2  
**Question:** Show all courses offered by the `Computer Science` department using a join.

select course_id, course_name
from courses
join Departments
on courses.dept_id = departments.dept_id
where dept_name = 'Computer Science';

### ⚡ Task 3  
**Question:** Display student names and marks who scored more than `80`.

select name, marks
from students
join enrollments
on students.student_id = enrollments.student_id
where marks > 80;

### ⚡ Task 4 
**Question:** Show students who scored **between 70 and 90** marks.

select name, marks
from students
join enrollments
on students.student_id = enrollments.student_id
where marks between 70 and 90;

### ⚡ Task 5
**Question:** Display students whose names **start with 'A'** using `LIKE`.

select * from students where name Like 'A%';

### ⚡ Task 6  
**Question:** List all cities without duplicates using `DISTINCT`.

select distinct city from students;

### ⚡ Task 7  
**Question:** Show top 3 students by marks using `ORDER BY` and `LIMIT`.

select name,marks 
from students 
join enrollments
on students.student_id = enrollments.student_id
order by enrollments.marks desc LIMIT 3;

### ⚡ Task 8  
**Question:** Show students with **NULL marks** (insert a test NULL to test this).

INSERT INTO enrollments VALUES  
(306, 3, 203, NULL);

select students.name, enrollments.marks
from students
join enrollments
on students.student_id = enrollments.student_id
where marks IS NULL;

### ⚡ Task 9  
**Question:** Show student name as `Student_Name` and city as `Location` using `AS`.

select name AS student_name, city AS location
from students;

### ⚡ Task 10  
**Question:** Update Priya's marks to 85 in the `enrollments` table.

UPDATE enrollments  
SET marks = 80  
WHERE student_id = 3;

### ⚡ Task 11  
**Question:** Delete enrollments where marks are less than 60.

delete from enrollment where marks < 60;

### ⚡ Task 12  
**Question:** Count the number of students in each city using `GROUP BY`.

select count(city) from students;

### ⚡ Task 13  
**Question:** Show **average marks** per course.

select courses.course_name, AVG(Marks) 
from courses
join enrollments
on courses.course_id = enrollments.course_id
group by courses.course_name;

### ⚡ Task 14  
**Question:** Use `HAVING` to show only those courses whose average marks are above 75.

select courses.course_name, AVG(Marks) 
from courses
join enrollments
on courses.course_id = enrollments.course_id
group by courses.course_name
Having AVG(Marks) > 75;

### ⚡ Task 15  
**Question:** Show departments with more than one course using `GROUP BY` and `HAVING`.

SELECT d.dept_name, COUNT(c.course_id) AS course_count
FROM departments d
JOIN courses c ON d.dept_id = c.dept_id
GROUP BY d.dept_name
HAVING COUNT(c.course_id) > 1;


### ⚡ Task 16  
**Question:** Use `IN` to show students from ‘Delhi’, ‘Mumbai’.

select * from students where city in ('Delhi','Mumbai');

### ⚡ Task 17  
**Question:** Use `EXISTS` to show students who are enrolled in any course.

select * from students s
where Exists (
  select 1
  from enrollments e
  where e.student_id = s.student_id
); 

### ⚡ Task 18  
**Question:** Use a subquery to list students who scored above the average mark.

select * 
from students s
where student_id IN (
  select student_id
  from enrollments e
  where marks > (
    select AVG(marks) from enrollments)
); 

### ⚡ Task 19  
**Question:** Show the highest and lowest marks per course using aggregate functions.

SELECT 
MAX(marks), 
MIN(marks)
from enrollments group by course_id;

### ⚡ Task 20  
**Question:** Normalize a single table holding student+course+marks into 3NF using `students`, `courses`, and `enrollments`.

student table

CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    gender VARCHAR(10),
    city VARCHAR(50)
);

course table

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)  -- Optional if dept info exists
);

enrollment table

CREATE TABLE enrollments (
    enroll_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    marks INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)


### ⚡ Task 21  
**Question:** Create an index on the `marks` column in the `enrollments` table.

create index idx_marks
on enrollments (marks);

### ⚡ Task 22  
**Question:** Join all four tables to show full data (student name, department name, course name, marks).

select
s.name,
d.dept_name,
c.course_name,
e.marks
from 
enrollments e
join students s on e.student_id = s.student_id
join courses c on e.course_id = c.course_id
join departments d on c.dept_id = d.dept_id;

### ⚡ Task 23  
**Question:** Use `BETWEEN` to show students aged between 19 and 21.

select * from students where age BETWEEN 19 AND 21;

### ⚡ Task 24  
**Question:** Use comparison and logical operators to find female students from ‘Delhi’ or ‘Kolkata’.

SELECT * FROM students WHERE city = 'Delhi' OR city = 'Kolkata';

### ⚡ Task 25
**Question:** Apply best SQL practices by writing a clean, commented query that finds the top scorer in each course with student name, course, and marks.

select
s.name,
c.course_name,
e.marks
from enrollments e
JOIN students s ON e.student_id = s.student_id 
JOIN courses c ON e.course_id = c.course_id
where (e.course_id, e.marks) IN (
  select course_id, MAX(marks)
  from enrollments
  group by course_id
)
order by c.course_name;