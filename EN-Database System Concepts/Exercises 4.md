# Exercises 4

## Problem 1

### Problem Description

Consider the following SQL query that seeks to find a list of titles of all courses taught in Spring 2017 along with the name of the instructor.

```sql
select name, title
from instructor natural join teaches natural join section natural join course
where semester='Spring' and year = 2017
```

What’s wrong with this query?

### Solution

Since *instructor* and *course* all have an attribute *dept_name*, the result would be those instructors who taught the course in his department.

## Problem 2

### Problem Description

Write the following queries in SQL:

a. Display a list of all instructors, showing each instructor’s ID and the number of sections taught. Make sure to show the number of sections as 0 for instructors who have not taught any section. Your query should use an outer join, and should not use subqueries.

b. Write the same query as in part a, but using a scalar subquery and not using outer join.

c. Display the list of all course sections offered in Spring 2018, along with the ID and name of each instructor teaching the section. If a section has more than one instructor, that section should appear as many times in the result as it has instructors. If a section does not have any instructor, it should still appear in the result with the instructor name set to “-”.

d. Display the list of all departments, with the total number of instructors in each department, without using subqueries. Make sure to show departments that have no instructors, and list those departments with an instructor count of zero.

### Solution

#### a

```sql
select instructor.ID, count(sec_id)
from instructor left outer join teaches
group by instructor.ID
```

#### b

```sql
select instructor.ID, (select count(sec_id) from teaches where instructor.ID = teaches.ID) as num
from instructor
```

#### c

```sql
select course_id, sec_id, ID, coalesce(name, '-')
from section natural left outer join teaches natural left outer join instructor
where semester = 'Spring' and year = 2018
```

#### d

```sql
select dept_name, count(name)
from department natural left outer join instructor
group by dept_name
```

## Problem 3

### Problem Description

Outer join expressions can be computed in SQL without using the SQL **outer join** operation. To illustrate this fact, show how to rewrite each of the following SQL queries without using the **outer join** expression.

a. `select * from student natural left outer join takes`

b. `select * from student natural full outer join takes`

### Solution

#### a

```sql
(select * from student natural join takes)
union
(select student.*, null, null, null, null, null from student where not exists
 (select * from takes where student.ID=takes.ID)
)
```

#### b

```sql
(select * from student natural join takes)
union
(select student.*, null, null, null, null, null from student where not exists
 (select * from takes where student.ID=takes.ID)
)
union
(select takes.ID, null, null, null, course_id, sec_id, semester, year, grade from takes where not exists
 (select * from student where student.ID=takes.ID)
)
```

## Problem 4

### Problem Description

Suppose we have three relations $r(A,B)$, $s(B,C)$ and $t(B,D)$, with all attributes declared as **not null**.

a. Give instances of relations $r$, $s$, and $t$ such that in the result of ($r$ **natural left outer join** $s$) **natural left outer join** $t$ attribute $C$ has a non-null value.

b. Are there instances of $r$, $s$, and $t$ such that the result of $r$ **natural left outer join** ($s$ **natural left outer join** $t$) has a null value for $C$ but a non-null value for $D$? Explain why or why not.

### Solution

#### a

==This question is almost open so we won’t give a fixed answer==.

#### b

$s$ **natural left outer join** $t$ will never let $C$ be null. Hence the reason for $C$ to be null is the outmost outer join, however by definition, in this case $C$ and $D$ will be null at the same time. And such a contradiction leads to proof.

## Problem 5

### Problem Description

**Testing SQL queries**: To test if a query specified in English has been correctly written in SQL, the SQL query is typically executed on multiple test databases, and a human check if the SQL query result on each test database matches the intention of the specification in English.

a. In Section 4.1.1, we say an example of an erroneous SQL query which was intended to find which courses had been taught by each instructor; the query computed the natural join of *instructor*, *teaches*, and *course*, and as a result it unintentionally equated the *dept_name* attribute of *instructor* and *course*. Give an example of a dataset that would help catch this particular error.

b. When creating test databases, it is important to create tuples in referenced relations that do not have any matching tuple in the referencing relation for each foreign key. Explain why, using an example query on the university database.

c. When creating test databases, it is important to create tuples with null values for foreign-key attributes, provided the attribute is nullable (SQL allows foreign-key attributes to take on null values, as long as they are not part of the primary key and have not been declared as **not null**). Explain why, using an example query on university database.

*Hint*: Use the queries from Exercise 4.2.

### Solution

#### a

==This question is almost open so we won’t give a fixed answer==.

#### b