---
title: "MySql Tips and Tricks"
date: 2021-10-23T00:39:25+06:00
featureImage: images/blog/tutorials/mysql/tips/msql-feature-small.jpg
postImage: images/blog/tutorials/mysql/tips/msql-feature-large.jpg
---

### Repairing utf8 broken characters 
Sometimes during data table backup or migration, you may end up having broken utf8 characters. A easy way to solve the problem is following the below SQL Query:
{{< highlight sql "linenos=table,linenostart=1" >}}
UPDATE table_name SET column_name = 
    CONVERT(BINARY CONVERT(column_name USING latin1) USING utf8);
{{< / highlight >}}
That's it. It will fix the broken characters. But as always be sure to back up your data table before doing any of such conversion.