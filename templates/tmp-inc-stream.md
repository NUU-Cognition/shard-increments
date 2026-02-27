# Filename: Mesh/Types/Increments/(Increment) [X.N.0] - [Name].md

```markdown
---
id: [generate-uuid]
tags:
  - "#increment"
  - "#inc/stream"
status: [active|completed]
iteration: X.N.0
checkpoint: "[[hyperlink to the latest checkpoint]]"
template: tmp-inc-stream
---

[when you iterate, you create a copy of the below with a increased number lik X.N.1]

# (Increment) [X.N.0] — [Name]

*[What this stream delivers]*

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
| [YYYY-MM-DD] | [X.N.0] | [Change and artifacts, if referecing an artifcat, make sure to be using hyperlinks to that artifact] |
(continue)
```
