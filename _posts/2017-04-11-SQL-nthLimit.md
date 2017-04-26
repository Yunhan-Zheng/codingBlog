---
layout: post
title: Leetcode-Nth Highest Salary
tags: leetcode sql
---
<strong>Q177 
    <a href="https://leetcode.com/problems/nth-highest-salary/#/description" target="_blank">Nth Highest Salary</a>
</strong>

This problem requires to return the n<sup>th</sup> highest salary from the below <code>employee</code> table where n is passed in as a parameter
<p>
    <pre>
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
</pre>
</p>

My first thought is
1. find n highest salaries
2. find the minimum from the above set 

Below is one solution from <a href="https://discuss.leetcode.com/user/addy9908" target="_blank">addy9908</a>, which has the same logic as mine but is more concise because s/he uses <a href="http://www.mysqltutorial.org/mysql-limit.aspx" target="_blank">LIMIT</a>.
{% highlight ruby %}
SELECT IF(COUNT(*)<N,NULL, MIN(salary)) AS salary
FROM (SELECT DISTINCT salary 
    FROM employee 
    ORDER BY salary DESC 
    LIMIT N) temp 
{% endhighlight %}

The other way to solve the problem is to find the salary where the number of distinct salaries greater than or equal to itself is equivalent to the parameter.

Below solution by [vivian16](https://discuss.leetcode.com/topic/25599/no-variable-no-limit-x-1-just-one-query-808ms/8) has runtime **860 ms**.
What I don't understand is that this solution will be much slower without the **Limit 1** statement

{% highlight ruby %}
SELECT DISTINCT salary FROM employee e
WHERE (SELECT Count(Distinct salary) 
    FROM employee e2 WHERE e2.salary>=e.salary)= N
Limit 1 
{% endhighlight %}
