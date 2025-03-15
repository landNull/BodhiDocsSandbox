<%*
  function toStudlyCase(str) {
    const normalized = str.replace(/[-_]/g, ' ').replace(/[^\w\s]/g, '').trim();
    return normalized.split(/\s+/).map(word => word.charAt(0).toUpperCase() + word.slice(1).toLowerCase()).join('');
  }

  // Get current file content to check for frontmatter
  const currentContent = await tp.file.content;
  const hasFrontmatter = currentContent.trim().startsWith('---');

  // Get current title without .md for comparison
  let title = tp.file.title.replace(/\.md$/, '');
  let newTitle = title; // Default to current title
  
  // Always prompt for manual use; skip in batch mode
  if (!tp.config.batch_mode) {
    newTitle = await tp.system.prompt("Enter Title", ""); // Blank prompt
  }
  
  const finalTitle = (newTitle && newTitle.trim()) ? newTitle : "Untitled";
  const studlyTitle = toStudlyCase(finalTitle); // StudlyCase for file name and frontmatter
  const spacedTitle = finalTitle.replace(/[-_]/g, ' ').trim(); // Spaced title for heading
  const newFileName = studlyTitle; // No .md here, Templater adds it
  
  // Rename file if needed (compare without .md)
  if (title !== newFileName) {
    await tp.file.rename(newFileName); // Templater appends .md automatically
  }

  // Handle frontmatter and content
  if (hasFrontmatter) {
    const frontmatterEnd = currentContent.indexOf('---', 3); // Find closing ---
    if (frontmatterEnd === -1) {
      // Malformed frontmatter, treat as no frontmatter
      tR = `---\ntitle: "${studlyTitle}"\n---\n# ${spacedTitle}\n${currentContent}`;
    } else {
      let existingFrontmatter = currentContent.slice(0, frontmatterEnd + 3);
      const bodyContent = currentContent.slice(frontmatterEnd + 3).trim();
      
      // Check if title exists in frontmatter and update or add it
      if (existingFrontmatter.match(/^title:/m)) {
        existingFrontmatter = existingFrontmatter.replace(/^title:.*$/m, `title: "${studlyTitle}"`);
      } else {
        existingFrontmatter = existingFrontmatter.replace('---\n', `---\ntitle: "${studlyTitle}"\n`);
      }
      
      tR = `${existingFrontmatter}\n${bodyContent}`;
    }
  } else {
    tR = `---\ntitle: "${studlyTitle}"\n---\n# ${spacedTitle}\n${currentContent}`.trim();
  }
_%>
<% tp.file.cursor(1) %>