---
layout: post
title: Leetcode-Rank Scores and Department Highest Salary
tags: Leetcode sql
---
**Q178 [Rank Scores](https://leetcode.com/problems/rank-scores/#/description)**

The core logic in this question is to find the corresponding rank for a score.
Looking at the desired output, soon you'll notice that one way to solve this problem is to find how many *distinctive* numbers greater than or equal to a specific score.
<p>
    <pre>
+-------+------+
| Score | Rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |
+-------+------+
</pre>
</p>
Hence, my solution is 
{% highlight ruby %}
SELECT score, (SELECT Count(*) FROM (SELECT Distinct score s FROM scores) temp WHERE s>=score) rank
FROM scores
ORDER BY score DESC
{% endhighlight %}

**Q184 [Department Highest Salary](https://leetcode.com/problems/department-highest-salary/)**

Given tables <code>employee</code> and <code>department</code> below,
<pre>
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
</pre>
<pre>
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
</pre>
the requested query is to find employees who have the highest salary in each of the departments.

How to proceed?
1. find the maximum salary within each department (the <code>temp</code> table below)
2. find the corresponding employee with the maximum salary (the second <code>where</code> condition below)

Hence, my solution is 
{% highlight ruby %}
SELECT d.name Department, e.name Name, e.salary Salary
FROM employee e, department d, 
    (SELECT MAX(salary) maxSal, departmentId 
    FROM employee GROUP BY departmentId) temp
WHERE e.departmentId=d.id
AND e.salary=temp.maxSal
AND e.departmentId=temp.departmentId
{% endhighlight %}

There is no *JOIN* keyword, but it's implicit join which you can find more info on 
<a href="https://en.wikipedia.org/wiki/Join_(SQL)" target="_blank">wiki-JOIN</a>