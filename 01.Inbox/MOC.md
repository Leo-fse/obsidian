---
created: 2024-10-12 12:10:38
modified: 2024-10-13 21:37:47
---



### Books
[Obsidian カテゴリーの記事一覧 - Jazzと読書の日々](https://wineroses.hatenablog.com/archive/category/Obsidian)

```dataviewjs
const FOLDER = "Inbox/Books"

dv.span(">[!test]- `$= dv.pages('\"" + FOLDER + "\"').file.tasks.filter(x => !x.completed).length` asks\n>```dataview\n>task from \"" + FOLDER + "\" where !completed group by file.link\n>```\n")

const p = dv.el("input","")
p.placeholder = "..."
p.style = "font-size:large;border-radius:3px;"
const btn = dv.el("button", "＋")
btn.style = "font-size:small;margin:5px;width:40px;"
const b = dv.el("div", "")
b.style = "max-height:14000px;"
disp()

p.onkeyup = () => disp()

btn.onclick = () =>{
  navigator.clipboard.writeText(p.value)
  s = "obsidian-book-search-plugin:open-book-search-modal"
  app.commands.executeCommandById(s) 
}

function disp(){
  const  d = dv.pages(`"${FOLDER}"`)
  .filter(x => (x.title + x.subtitle + x.author + x.description).includes([p.value]))
  .sort(x => x.file.ctime, "desc")
  .map(x => `<tr style="font-size:small;padding:4px;"><td><img style="max-width:60px;" src="${x.coverSmallUrl}"></td><td><a class=internal-link href="${x.file.name}">${x.title}</a></td><td>${x.author}</td><td>${(x.publisher || "")}</td><td>${x.publishDate.toLocaleString()}</td></tr>`)
  b.innerHTML = "<br><table style='width:100%;'>" + d.join("\n") + "</table>"
}
```



```dataviewjs
const FOLDER = "Inbox/Books"

dv.span("蔵書検索")
const a = dv.el("input")
a.placeholder = "keyword"
a.style = "font-size:18px;background:whitesmoke;width:100%;"
dv.paragraph("---")
const b = dv.el("div","")
a.onkeyup = function(){
  d = dv.pages(`"${FOLDER}"`)
  .filter(x => x.file.name.includes([a.value]))
  .sort(x => x.publishDate, "desc")
  .map(x => "<a href=obsidian://open?file="+encodeURI(x.file.name)+"><img width=98 src="+x.coverUrl+"></a>")
  b.innerHTML = d.join(" ")
}
```

# 📚 My Bookshelf

```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Book
FROM  #📚Book
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status
```

## List of all books

```dataview
TABLE WITHOUT ID
	status as Status,
	"![|60](" + cover + ")" as Cover,
	link(file.link, title) as Title,
	author as Author,
	join(list(publisher, publish)) as Publisher
FROM #📚Book
WHERE !contains(file.path, "Templates")
SORT status DESC, file.ctime ASC
```
