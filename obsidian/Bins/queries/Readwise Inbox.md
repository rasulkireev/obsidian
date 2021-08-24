These are the [[Readwise]] imports that still have to check for note quality... a.k.a [[Inbox]] 


```dataview
table file.tags, file.path
from "Sources/Readwise"
where contains(status, "inbox")
```