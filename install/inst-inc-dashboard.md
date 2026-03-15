---
id: de55ea33-20bd-4c51-8e97-6fd64a2bdfdf
tags:
  - "#inc/dashboard"
  - "#managed/shard/inc"
---

```dataviewjs
// Parse version string to sortable number (e.g., "4.2" -> 40200, "4.A" -> 49900)
function parseVersion(v) {
  if (!v) return 0;
  const parts = String(v).split('.');
  const major = parseInt(parts[0]) || 0;
  const minor = parts[1] === 'A' ? 99 : (parseInt(parts[1]) || 0);
  return major * 10000 + minor * 100;
}

function sortByVersion(pages, desc = false) {
  return pages.array().sort((a, b) => {
    const av = parseVersion(a.increment);
    const bv = parseVersion(b.increment);
    return desc ? bv - av : av - bv;
  });
}

function formatName(p) {
  return p.file.name.replace(/^\(Increment\)\s*/, '');
}

// Only look in Mesh/ folder
const meshPages = (tag) => dv.pages(tag).where(p => p.file.path.startsWith('Mesh/'));

// Loop Health
dv.header(1, "Loop Health");
const openLoops = meshPages('#inc/increment').where(p => p.status === 'open').array();
const openCount = openLoops.length;
dv.paragraph(`**${openCount} open loop${openCount !== 1 ? 's' : ''}**`);

// Current Checkpoint
dv.header(1, "Current Checkpoint");
const checkpoints = meshPages('#inc/checkpoint').array().sort((a, b) => {
  const av = parseVersion(a.increment ?? a.file.name.match(/(\d+\.\d+)/)?.[1]);
  const bv = parseVersion(b.increment ?? b.file.name.match(/(\d+\.\d+)/)?.[1]);
  return bv - av;
});
if (checkpoints.length > 0) {
  const current = checkpoints[0];
  dv.paragraph(dv.fileLink(current.file.path, false, current.file.name.replace(/^\(Increment\)\s*/, '')));
} else {
  dv.paragraph("*No checkpoints found*");
}

// Open Loops
dv.header(1, "Open Loops");
const open = sortByVersion(
  meshPages('#inc/increment').where(p => p.status === 'open')
);
if (open.length === 0) {
  dv.paragraph("*None*");
} else {
  dv.table(["Increment", "Version", "Opened"],
    open.map(p => [dv.fileLink(p.file.path, false, formatName(p)), p.increment ?? "—", p.opened ?? "—"])
  );
}

// Recently Closed
dv.header(1, "Recently Closed");
const closed = sortByVersion(
  meshPages('#inc/increment').where(p => p.status === 'closed'),
  true
).slice(0, 10);
if (closed.length === 0) {
  dv.paragraph("*None*");
} else {
  dv.table(["Increment", "Version"],
    closed.map(p => [dv.fileLink(p.file.path, false, formatName(p)), p.increment ?? "—"])
  );
}

// Checkpoint History
dv.header(1, "Checkpoint History");
if (checkpoints.length === 0) {
  dv.paragraph("*None*");
} else {
  dv.list(checkpoints.map(p =>
    dv.fileLink(p.file.path, false, p.file.name.replace(/^\(Increment\)\s*/, ''))
  ));
}
```
