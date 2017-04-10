---
layout: post
title: Leetcode-Rank Scores
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
