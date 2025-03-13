```markdown
<%*
  function toStudlyCase(str) {
    const normalized = str.replace(/[-_]/g, ' ').replace(/[^\w\s]/g, '').trim();
    return normalized.split(/\s+/).map(word => word.charAt(0).toUpperCase() + word.slice(1).toLowerCase()).join('');
  }

  let title = tp.file.title.replace(/\.md$/, '');
  let newTitle = title; // Default to current title
  
  // Always prompt for manual use; skip in batch mode
  if (!tp.config.batch_mode) {
    newTitle = await tp.system.prompt("Enter Title", ""); // Blank prompt
  }
  
  const finalTitle = (newTitle && newTitle.trim()) ? newTitle : "Untitled";
  const studlyTitle = toStudlyCase(finalTitle); // StudlyCase for file name and frontmatter
  const spacedTitle = finalTitle.replace(/[-_]/g, ' ').trim(); // Spaced title for heading
  const newFileName = `${studlyTitle}.md`;
  
  if (tp.file.title !== newFileName) {
    await tp.file.rename(newFileName);
  }
  
  // Build output with tR
  tR = "---\n";
  tR += `title: "${studlyTitle}"\n`; // StudlyCase in frontmatter
  tR += "---\n";
  tR += `# ${spacedTitle}\n`; // Spaced title in heading
_%>
<% tp.file.cursor(1) %>
```