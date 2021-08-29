```dataview
table file.tags, file.path
from ""
where (contains(status, "to_read") AND contains(tags, "book"))
 OR (contains(status, "to_read") AND contains(tags, "books"))
```