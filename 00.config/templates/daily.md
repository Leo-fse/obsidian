---
created:
modified:
aliases: 
tags:
  - Daily
---
< [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>]] | [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>]] > WN: [[<% tp.date.now("YYYY-[W]ww", 0, tp.file.title, "YYYY-MM-DD") %>]]
## 今日やること／やったこと

## Created
```dataview
TABLE 
	WITHOUT ID 
	link(file.link, title) AS "Title",
	file.frontmatter.category AS category
FROM
	"01.Inbox" or "03.Books" or "04.ReadItLater"
WHERE
	dateformat(file.cday, "yyyy-MM-dd") = this.file.name
```
