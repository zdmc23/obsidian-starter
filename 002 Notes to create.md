# 002 Notes to create

```dataviewjs  
let phantoms =
  dv.pages()
    .flatMap(p => p.file.outlinks.map(link => [link, p.file]))
    .groupBy(p => p[0])
    //.filter(g => g.rows.length > 1)
    .filter(g => !g.key.path.endsWith(".png") && !g.key.path.endsWith(".jpeg") && !g.key.path.endsWith(".jpg"))
    .map(g => { return { key: g.key, rows: g.rows.map(r => r[1]) }})
    .filter(g => dv.page(g.key) === undefined)
    .sort(g => g.rows.length, "desc")

dv.table(
  ["Note to Create", "Linked From"],
  phantoms.map(g => [
    g.key,
    g.rows.map(p => p.link),
  ])
)
```
