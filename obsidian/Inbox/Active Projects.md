
```dataview
table file.tags, status
from ""
where contains(file.tags, "#Project")
	OR contains(file.tags, "#project")
	AND status!=done
```