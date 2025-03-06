<%*
  let title = tp.file.title
  if (title.startsWith("Untitled")) {
    title = await tp.system.prompt("Title");
    await tp.file.rename(title);
  } 
  
  tR += "---"
%>
parent: 
child: 
related: 
status:
tags: 
created: <% tp.date.now("YYYY-MM-DD") %>
summary:

---
# <%* tR += `${title}` %>
<% tp.file.cursor(1) %>