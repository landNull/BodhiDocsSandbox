---
parent:
  - "[[TOCs]]"
child: 
related: 
status: 
type:
  - TOC
tags: 
created:
---
# Table Of Contents `BUTTON[child-note]` `BUTTON[note-in-folder]`

>[!info]+ Featured Notes, Bookmarks & Highlights
> ```dataview 
> LIST
>FROM "03 Work" OR "04 Life" OR "05 Interests"  OR "08 Sources"
> WHERE contains(file.folder, this.file.folder) AND (contains(status, "Featured") OR file.starred)
> SORT file.mtime DESC
> limit 10
> ```
>```dataview
>LIST
>choice(Highlight, Highlight + "", "") 
>FROM "03 Work" OR "04 Life" OR "05 Interests"  OR "08 Sources"
>WHERE contains(file.folder, this.file.folder) AND Highlight
>FLATTEN Highlight
>SORT file.mtime DESC
>LIMIT 10
> ``` 

> [!example]+ Sub-topics
> ```dataview 
> table without id file.link as "Note", file.mday AS Updated
>FROM "03 Work" OR "04 Life" OR "05 Interests"
> WHERE contains(file.folder, this.file.folder) AND (contains(type, "Topic"))
> SORT file.mtime DESC
> LIMIT 10
> ```

> [!info]+ Parent & Child Notes
> ```breadcrumbs
> # Shows parent and child notes
> type: tree
> fields: [parent, child]
> depth: [0, 0]
> show-attributes: [field]
> sort: field desc
> ```

> [!summary]- Related & Sibling Notes
> ```breadcrumbs
> # Shows sibling and related notes
> type: tree
> fields: [sibling, related]
> depth: [0, 0]
> show-attributes: [field]
> sort: field desc
> ```

> [!attention]- Notes in This Folder
> ```dataview 
> table without id file.link as "Note", file.mday AS Updated
>FROM "03 Work" OR "04 Life" OR "05 Interests"
> WHERE contains(file.folder, this.file.folder) AND !contains(status, "Featured") AND file.name != this.file.name
> SORT file.mtime DESC
> LIMIT 50
> ``` 

> [!tip]- TIPS
Add *Highlight::* in front of a paragraph, change the status of a note to *Featured* or *Bookmark* a note to add it to the Featured Notes, Bookmarks & Highlights block. 
>
Add the *Insert Sub-Topics Blocks* template to a note to create a sub-topic.
>
>Add notes in the *Parent or Child field* to add it to the Parents & Child Notes block. Add notes to the *Related field* to add it to the Related & Sibling block. (Siblings are notes that have the same parent.) Use *Alt + p* to open the properties view.
