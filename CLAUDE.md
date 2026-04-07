# desa 網站工作說明

## 網站基本資訊

- 網域：https://desassossego.net
- Hugo 靜態網站，theme 是 PaperMod（git submodule）
- 部署：push 到 GitHub（kt-tan/desa），GitHub Actions 自動建置並部署到 GitHub Pages

## 本地開發

Hugo server 啟動指令（port 1314，因為 1313 另一個 hugo instance 在用）：

```
hugo server -p 1314 --disableFastRender
```

`--disableFastRender` 是必要的，沒有它 CSS 改動不會即時反映。

## 內容修改流程

文章 `.md` 檔的正確修改順序：

1. 先改 Obsidian vault 裡的版本：
   `/Users/kongtat/Library/Mobile Documents/iCloud~md~obsidian/Documents/puh-inn/3 desassossego.net/posts/`
2. 改完確認後，再 cp 到網站：
   `cp <vault>/posts/*.md /Users/kongtat/website/desa/content/posts/`

不要直接改 `content/posts/` 裡的檔案，vault 是唯一的來源。

## YAML front matter 規則

如果一篇文章的 `tags` 和 `categories` 有重複的項目，移除 `tags` 裡的那個，保留 `categories`。

## Git 規則

- `public/` 已在 `.gitignore`，不要 commit
- commit 只加需要的檔案，不要 `git add -A`
- themes/PaperMod 是 git submodule，不要手動改

## URL 規則

baseURL 是根路徑 `https://desassossego.net/`，所有 URL 不加 `/desa/` 前綴。如果看到路徑裡有 `/desa/`，那是舊的 GitHub Pages 子路徑設定，需要修掉。

## 自訂版面檔案位置

- `assets/css/extended/custom.css`：所有自訂樣式
- `layouts/index.html`：首頁（全文五篇，帶分頁）
- `layouts/partials/header.html`：頁首（含 site description）
- `layouts/partials/post_meta.html`：文章 meta（日期 + category 連結）
- `content/archive.md`：archive 頁
- `content/search.md`：search 頁（Fuse.js）
