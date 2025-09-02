
# 📅 Internship Log - {{date:MMMM YYYY}}

## Monthly Summary
- **Key Accomplishments:** 
- **Overall Learnings:** 

---

### Weekly Breakdown

```dataviewjs
const pages = dv.pages('"Daily Logs"').where(p => moment(p.file.name).format("YYYY-MM") === "{{date:YYYY-MM}}");

const groups = pages.groupBy(p => "Week " + moment(p.file.name).format("W"));

for (let group of groups.sort(g => g.key)) {
  dv.header(4, group.key);
  dv.list(group.rows.map(p => p.file.link));
}
```