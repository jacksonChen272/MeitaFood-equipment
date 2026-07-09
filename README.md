# 美達資訊設備管理平台

Meita IT Asset Dashboard 是給美達食品工業股份有限公司資訊部門使用的單頁設備管理系統。前端以 `index.html` 單檔實作，搭配 Firebase Firestore 作為多人共用資料庫，可部署在 GitHub Pages。

## 目前功能

- 儀表板總覽：設備總數、電腦、筆電、印表機、網路設備、各狀態數量、保固即將到期數量。
- 設備資料管理：新增、編輯、刪除、搜尋、依類型/狀態/部門篩選。
- 統計分析：依設備類型、部門、狀態統計，並以進度條呈現。
- 保固與維修提醒：保固 30 天內到期、維修中設備、報廢設備集中顯示。
- 匯入匯出：支援匯出 JSON、匯入 JSON、匯出 CSV。
- 雲端同步：使用 Firebase Firestore collection `it_assets`，讓不同裝置看到同一份資料。
- 離線備援：Firestore 無法連線時，使用 localStorage 快取。
- 設備條碼：每台設備可用設備編號產生專屬 Code 128 條碼，支援預覽、下載 SVG、列印標籤。

## 專案檔案

- `index.html`：完整系統主檔，HTML、CSS、JavaScript 都在同一檔案內。
- `meita-logo.jpg`：側欄品牌 Logo。
- `README.md`：專案說明與更新紀錄。

## Firebase 設定

系統已使用 Firebase Web SDK CDN 動態載入，不需要 npm build。

Firestore collection 固定使用：

```text
it_assets
```

請確認 Firebase Console 的 Firestore Database 已啟用，且安全規則允許 GitHub Pages 前端讀寫。若規則未開放，頁面會顯示離線模式或 Firestore 讀取失敗。

## GitHub Pages 部署

將以下檔案放到 GitHub Pages repo 根目錄：

- `index.html`
- `meita-logo.jpg`
- `README.md`

部署完成後，開啟：

```text
https://jacksonchen272.github.io/MeitaFood-equipment/
```

若頁面上方顯示「已連線雲端資料庫」，代表 Firestore 已正常同步。若仍看到舊版 localStorage 說明，代表 GitHub Pages 尚未更新到新版檔案。

## 更新紀錄

### 2026-07-09｜v1.4 設備專屬條碼

- 新增每台設備的專屬條碼功能。
- 條碼內容使用設備編號產生 Code 128。
- 設備表格操作區新增「條碼」按鈕。
- 新增條碼預覽彈窗。
- 支援下載條碼 SVG。
- 支援列印設備標籤。
- 條碼功能不依賴外部套件。

### 2026-07-09｜v1.3 Firebase Firestore 多人共用資料

- 將主要資料來源由 localStorage 改為 Firebase Firestore。
- 建立並使用 Firestore collection `it_assets`。
- 頁面載入後即時監聽 Firestore 資料。
- 新增、編輯、刪除設備時同步寫入 Firestore。
- 匯入 JSON 時可覆蓋 Firestore 設備資料。
- localStorage 改為本機快取與離線備援。
- 新增雲端連線狀態提示：已連線雲端資料庫 / 離線模式。
- 保留舊版 localStorage key 的資料遷移邏輯。
- 填入 Firebase 專案設定：`meitafood-equipment`。

### 2026-07-09｜v1.2 品牌 Logo

- 新增美達食品工業股份有限公司 Logo。
- 將 Logo 放置於左側品牌區。
- 調整 Logo 白底、間距與邊框，讓黑白識別圖在深色側欄上更清楚。
- 新增 `meita-logo.jpg` 作為部署資源。

### 2026-07-09｜v1.1 localStorage 單機完整功能版

- 建立單頁版「美達資訊設備管理平台」。
- 使用 HTML、CSS、JavaScript 單檔完成。
- 使用 localStorage 儲存設備資料。
- 新增儀表板統計卡片。
- 新增設備資料表格。
- 支援新增、編輯、刪除設備。
- 支援搜尋與篩選設備類型、使用狀態、部門。
- 新增依設備類型、部門、狀態統計。
- 新增保固 30 天內到期提醒。
- 新增維修中設備與報廢設備集中顯示。
- 支援 JSON 匯出、JSON 匯入、CSV 匯出。
- 建立預設範例資料：桌上型電腦、筆記型電腦、印表機、交換器、無線 AP、NAS、掃描器。
- 完成企業化、科技感、藍綠主色系與 RWD 響應式設計。

## 後續更新規則

每次更新系統功能時，請同步更新本 README 的「更新紀錄」，格式如下：

```text
### YYYY-MM-DD｜vX.X 更新名稱

- 更新項目 1
- 更新項目 2
- 修正項目 1
```

