# Next.js 專案檔案結構說明（App Router + Tailwind + TypeScript）

本文件說明一個使用 App Router、TypeScript 和 Tailwind CSS 的 Next.js 專案中，各檔案與資料夾的用途與關係。

---

## 📁 專案結構總覽（含範例路由）

```
your-project/
├── app/
│   ├── layout.tsx                # 全域 Layout，包含 Navbar 等共用 UI
│   ├── page.tsx                  # 根路由首頁
│   ├── globals.css               # 全域 CSS 設定
│   ├── login/
│   │   ├── layout.tsx           # Login 區段專用的 Layout（不含 Navbar ）
│   │   └── page.tsx             # 登入頁（不需要 Navbar）
│   ├── users/
│   │   └── page.tsx             # /users 頁面 使用全域 Layout （含 Navbar ）
│   ├── contacts/
│   │   └── page.tsx             # /contacts 頁面，使用全域 Layout （含 Navbar ）
│   ├── events/
│   │   ├── page.tsx             # /events 頁面 
│   │   └── [id]/
│   │       └── page.tsx         # /events/123 動態路由，顯示特定事件
├── components/                  # 可重用元件（如 Navbar、Card 等）
├── public/                      # 靜態資源，如圖片、icon
├── node_modules/                # npm 套件
├── .next/                       # Next.js 執行與建構快取資料夾
├── out/                         # next export 時產出的靜態網站內容
├── next.config.ts               # Next.js 設定檔
├── eslint.config.mjs            # ESLint 設定檔
├── postcss.config.mjs           # PostCSS 設定
├── tailwind.config.ts           # Tailwind CSS 設定檔
├── tsconfig.json                # TypeScript 設定檔
├── package.json                 # 專案設定與套件清單
├── package-lock.json            # 套件鎖定版本
```

---

## 📁 目錄與 📄 檔案說明

### `app/`

* **App Router 架構的核心資料夾**
* 每個子資料夾代表一個路由段（segment）
* 特殊檔案：

  * `page.tsx`：該段的頁面元件
  * `layout.tsx`：該層與子層共用版型（具繼承性）
  * `globals.css`：全域樣式設定檔（取代 `styles/` 資料夾）

#### ✅ 範例說明：

* `/login`：

  * 只有 `page.tsx`，不繼承共用 `layout.tsx`
  * 適合用於登入頁、註冊頁等不需 Navbar 的簡潔頁面
* `/users`：

  * 有獨立的 `layout.tsx`，加入 Sidebar、用戶導覽邏輯
  * 可與其他區段區隔 UI 結構
* `/contacts`、`/events`：

  * 使用全域 layout.tsx（有 Navbar）
* `/events/[id]`：

  * 動態路由，顯示單一事件內容，仍沿用 `/events` 的上層 layout

---

### `components/`

* 放置可重複使用的 UI 元件
* 例如：`Button.tsx`、`Navbar.tsx` 等

---

### `public/`

* 放置靜態資源（不經 Webpack 處理）
* 可透過 `/檔名` 直接存取
* 例如圖片、favicon、robots.txt 等

---

### `node_modules/`

* 專案安裝的所有 npm 套件
* 由 `npm install` 或 `pnpm install` 自動建立

---

### `.next/`

* Next.js 執行與建構時產生的快取與輸出資料夾
* 包含 SSR、SSG 的預編譯結果與快取檔案

---

### `out/`

* 執行 `next export` 時產生的靜態網站輸出目錄
* 僅在完全靜態輸出（無 SSR）專案中會使用

---

### `next.config.ts`

* Next.js 設定檔
* 用於設定路由、圖片白名單、rewrite/redirect、實驗功能等

---

### `eslint.config.mjs`

* ESLint 設定檔
* 定義語法檢查與格式化的規則與外掛

---

### `postcss.config.mjs`

* Tailwind CSS 使用的 PostCSS 設定檔
* 通常如下設定：

```js
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

---

### `tailwind.config.ts`

* Tailwind CSS 的核心設定檔
* 常見設定：

  * `content`: 掃描哪些檔案中的 class
  * 自訂顏色、字型、斷點等主題擴充

```ts
content: [
  './app/**/*.{js,ts,jsx,tsx}',
  './components/**/*.{js,ts,jsx,tsx}',
],
```

---

### `tsconfig.json`

* TypeScript 的設定檔
* 包含型別檢查、模組解析、別名設定等

---

### `package.json`

* 專案的基本資訊與套件清單
* 包含執行指令（scripts）：

```json
"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start"
}
```

---

### `package-lock.json`

* 記錄實際安裝的每個套件版本與依賴樹
* 確保團隊成員安裝版本一致

---

## 🔁 運作流程簡要

1. 執行 `npm run dev` 啟動 Next.js 專案
2. 依據 `app/` 中的路由與版型顯示畫面
3. Tailwind CSS 從 `globals.css` 掃描 class 並生成樣式
4. 開發與建構過程中使用 `.next/` 快取與輸出
5. 若需要靜態匯出則使用 `out/`

---

## ✅ 備註

* 建議將 `components/` 視為獨立模組化設計核心，便於維護與測試
* 登入頁可設計為跳過共用 layout（無 Navbar）
