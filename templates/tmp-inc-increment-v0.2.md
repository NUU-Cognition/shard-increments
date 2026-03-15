# Filename: Mesh/Increments/(Increment) [X.N] - [Name].md

```markdown
---
id: [generate-uuid]
tags:
  - "#inc/increment"
status: [open|closed|deprecated]
increment: "X.N"
checkpoint: "[[hyperlink to the latest checkpoint]]"
continues:
/* If this increment continues work from a prior increment, add wikilinks here. Otherwise leave empty. */
opened: [YYYY-MM-DD]
template: "[[tmp-inc-increment-v0.2]]"
---

# (Increment) [X.N] — [Name]

*[What this increment delivers]*

## Context

[Detailed context for the increment]

**Related Documents**

- [[Related documents if present]]

## Scope

- [Goal or deliverable]
(continue)

## Artifacts

/* Dataview query - displays all artifacts with increment field linking to this document */

```dataviewjs
const currentFile = dv.current().file.name;
const allPages = dv.pages()
  .where(p => p.increment && p.increment.path && p.increment.path.includes(currentFile));

const groups = {
  "Tasks": allPages.filter(p => p.file.path.includes("/Tasks/")).array(),
  "Plans": allPages.filter(p => p.file.path.includes("/Plans/")).array(),
  "Notepads": allPages.filter(p => p.file.path.includes("/Notepads/")).array(),
  "Reports": allPages.filter(p => p.file.path.includes("/Reports/")).array()
};

for (const [type, pages] of Object.entries(groups)) {
  if (pages.length > 0) {
    dv.header(3, type);
    dv.table(["Name", "Status"],
      pages.map(p => [p.file.link, p.status ?? "—"])
    );
  }
}

if (allPages.length === 0) {
  dv.paragraph("*No artifacts linked to this increment yet*");
}
```



## Log

| Date | Version | Change |
|------|---------|--------|
| [YYYY-MM-DD] | [X.N] | [Change and artifacts, if referencing an artifact, use hyperlinks] |
(continue)
```
