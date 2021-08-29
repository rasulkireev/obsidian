```dataview
table file.tags, file.path
from ""
where (contains(status, "to_read") AND contains(tags, "article"))
 OR (contains(status, "to_read") AND contains(tags, "articles"))
```