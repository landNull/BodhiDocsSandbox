# My Home Page

> [!example] Recently Created Notes
> ```dataview
> LIST
> FROM "Bodhi Linux Documentation"
> FLATTEN status
> Sort file.ctime DESC
> limit 10
> ```

> [!info] Recently Updated Notes
> ```dataview
> LIST
> FROM "Bodhi Linux Documentation"
> Sort file.mtime DESC
> limit 10
> ```

>[!example] Notes without a parent note
>```dataview
>LIST
>FROM "Bodhi Linux Documentation"
>WHERE (length(file.inlinks) = 0 AND length(file.outlinks) = 0 AND length(file.tags) = 0) OR !parent
>FLATTEN status
>SORT file.mtime desc
>Limit 15
>```

>[!note] Status of Notes
> ```dataview
> TABLE  without id status AS Status, rows.file.link as Note
> FROM "Bodhi Linux Documentation"
> FLATTEN status
> WHERE status AND !contains(status, "Pinned")  AND !contains(status, "Featured") AND !contains(status, "Completed") AND !contains(status, "Read-Later") 
> GROUP BY status
> SORT file.cday desc
> LIMIT 50
> ```

>[!summary] Completed Notes
> ```dataview
> TABLE  without id status AS Status, rows.file.link as Note
> FROM "Notes"
> FLATTEN status
> WHERE status AND contains(status, "Completed")
> GROUP BY status
> SORT file.cday desc
> LIMIT 50
> ```

