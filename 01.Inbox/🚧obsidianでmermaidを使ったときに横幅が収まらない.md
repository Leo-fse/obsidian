---
created: 2024-10-14 19:52:17
modified: 2024-10-14 19:52:19
---
[2021-11-10 Obsidian内蔵のMermaid - めモらンだム・ヤード](https://sorashima.hatenablog.com/entry/MermaidImplemetedInObsidian)

obsidianにおいてmermaidの図が横に大きくなりすぎるときはcssに  
```css
.mermaid>svg{ min-width: 400px; max-width: 100%; }
```  
とすれば改善できた

CSSスニペットのフォルダは、`<vaultフォルダ>/.obsidian/sunippets`。ここに拡張子`.css`のファイルを置く。