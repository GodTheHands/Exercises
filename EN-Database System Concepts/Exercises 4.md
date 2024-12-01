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

It is possible the referenced tuple haven’t been referenced yet.

#### c

We may need to detect some error when query are dealing with nullable values.

## Problem 9

### Problem Description

SQL allows a foreign-key dependency to refer to the same relation, as in the following example:

```sql
create table manager
	(employee_ID	char(20),
     manager_ID		char(20),
     primary key employee_ID,
     foreign key (manager_ID) references manager(employee_ID)
     						on delete cascade)
```

Here, $employee\_ID$ is a key to the table *manager*, meaning that each employee has at most one manager. The foreign-key clause requires that every manager also be an employee. Explain exactly what happens when a tuple in the relation *manager* is deleted.

### Solution

When a tuple in relation *manager* is deleted. SQL would check the corresponding tuple in *manager* whose $manager\_ID$ is indentical to the $employee\_ID$ of the deleted tuple. Then those tuples are deleted, too. And then check these conditions again, until no more tuple can be deleted any more.

## Problem 11

### Problem Description

Operating systems usually offer only two types of authorization control of data files: read access and write access. Why do database systems offer so many kinds of authorization?

### Solution

Because there are various kinds of needs for specific authorization.

## Problem 12

### Problem Description

Suppose a user wants to grant **select** access on a relation to another user. Why should the user include (or not include) the clause **granted by current role** in the **grant** statement?

### Solution

Include: it guarantees even if the **select** access of the user who grants the access is revoked. Another user will still have the **select** access. It decouples the access and make it easy to add or delete users without considering too much about privilege.

Exclude: when the **select** access of user who grants the access is revoked, another user’s access will also be revoked. This ensures the security of the system to some extent by avoiding unfriendly user to propagate access without limitation.

## Problem 13

### Problem Description

Consider a view $v$ whose definition references only relation $r$.

- If a user is granted **select** authorization on $v$, does that user need to have **select** authorization on $r$ as well? Why or why not?
- If a user is granted **update** authorization on $v$, does that user need to have **update** authorization on $r$ as well? Why or why not?
- Give an example of an **insert** operation on a view $v$ to add a tuple $t$ that is not visible in the result of **select** * **from** $v$. Explain your answer.

### Solution

#### a

No, because the view may be established for hiding some information for security.

#### b

Yes, because if not, he will only be able to affect the view, but that makes no sense.

#### c

==This question is almost open so we won’t give a fixed answer==.

## Problem 14

### Problem Description

Consider the query

```sql
select course_id, semester, year, sec_id, avg(tot_cred)
from takes natural join student
where year = 2017
group by course_id, semester, year, sec_id
having count (ID) >= 2;
```

Explain why appending **natural join** *section* in the **from** clause would not change the result.

### Solution

Because $course\_id,sec\_id,semester$ and $year$ is foreign key, thus there must be a corresponding tuple in *section* whenever there is a tuple in the original query. Thus adding it would not affect the result.

## Problem 19

### Problem Description

Under what circumstances would the query

```sql
select *
from student natural full outer join takes
				natural full outer join course
```

include tuples with null values for the *title* attribute?

### Solution

Since *title* is not primary key, so it is totally possible to be *null*. Besides this reason, since there’s a foreign key path from *takes* to *course*, this indicates the latter `natural full outer join` won’t yield *null* tuple if the former result is not null. However, it is totally possible for *student* to be not *null* but *takes* to be *null*. The above are the only two reasons for *title* to be *null*.

## Problem 21

### Problem Description

For the view of Exercise 4.18, explain why the database system would not allow a tuple to be inserted into the database through this view.

### Solution

Because the view doesn’t contain any information aboout employee other than ID. Attempting to insert data by this view will make the database unable to fill the information, which is object to the semantic.

## Problem 23

### Problem Description

Explain why, when a manager, say Satoshi, grants an authorization, the grant should be done by the manager role, rather than by the user Satoshi.

### Solution

Because if by the user Satoshi, once he left, all the authorization granted from him will be cascade revoked. However other employee doesn’t need to leave with him, thus it would lead to redundant coupled relationship.

## Problem 24

### Problem Description

Suppose user $A$, who has all authorization privileges on a relation $r$, grants **select** on relation $r$ to **public** with grant option. Suppose user $B$ then grants **select** on $r$ to $A$. Does this cause a cycle in the authorization graph? Explain why.

### Solution

Yes, it is indeed from $A$ to **public**, from **public** to $B$ and from $B$ to $A$.

## Problem 25

### Problem Description

Suppose a user creates a new relation $r1$ with a foreign key referencing another relation $r2$. What authorization privilege does the user need on $r2$? Why should this not simply be allowed without any such authorization?

### Solution

$r2$ need **references** privilege. Because the definition of a foreign key restricts future activity of $r2$.

## Problem 26

### Problem Description

Explain the difference between integrity constraints and authorization constraints.

### Solution

Integrity constraints ensure the data consistency by preventing authorized users to make unintended changes.

Authorization constraints prevents unauthorized users from modifying the database.