<%*
let title = tp.file.title; // Defau
const content = await tp.file.content;
const headingMatch = content.match(/^# (.+)$/m);
if (headingMatch) {
  title = headingMatch[1];
}
tR += `---
title: "${title}"
slug: "${title.toLowerCase().replace(/\s+/g, "-")}"
date: "${tp.date.now("YYYY-MM-DD")}"
---
`;
%>
<% tp.file.content %>