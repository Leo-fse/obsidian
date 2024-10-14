---
created: 2024-10-14 16:21:30
modified: 2024-10-14 17:47:39
---
### ER図の記述形式は２つある。
- IE（Information Engineering）：ジェームズ・マーチン考案
- IDEF1X ：アメリカ空軍開発
### ER図のエンティティに記載するものは以下の４つ。
- エンティティ名
- 属性
- 主キー（PK）
- 外部キー（FK）
### エンティティ間にリレーションシップがある場合はエンティティ同士をつなぐ。
エンティティ同士の数量的な関係を多重度やカーディナリティという。


```mermaid
--- 
title: "家計管理の概念をまとめたER図"
---

erDiagram
    C["利用者"] {
	    string name
    }
    A["入出金行為"] {
	    string actionid PK 
	    date date "Only 99 characters are allowed"
	    string name
	    string item
    }
    AD["入出金明細"] {
	    string actionid PK
	    string spentitemid FK
	    float amount
    }
    TG["タグ"] {
	    string tagid PK
	    string item
    }
    SI["費目"] {
	    string itemid PK
	    string itemname
	    string group
    }
    C||--o{ A : places
    A ||--|{ AD : contains
    AD }|..|{ SI : uses
    A }o..o{ TG : ""


```

|Value (left)|Value (right)|Meaning|
|---|---|---|
|`\|o`|`o\|`|Zero or one|
|`\|`|`\|`|Exactly one|
|`}o`|`o{`|Zero or more (no upper limit)|
|`}\|`|`\|{`|One or more (no upper limit)|

参考：
[[mermaidの書き方]]
