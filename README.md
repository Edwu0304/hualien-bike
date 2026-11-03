# 花東縱谷鐵馬行

花東縱谷三天單車行程的單頁式行程網站，可離線瀏覽、搜尋行程節點，並一鍵開啟 Google Maps 導航。

## 上線資訊

| 項目 | 內容 |
| --- | --- |
| 網站網址 | <https://edwu0304.github.io/hualien-bike/> |
| GitHub Repo | <https://github.com/Edwu0304/hualien-bike>（公開） |
| 託管方式 | GitHub Pages |
| 來源分支 | `main`（根目錄） |
| 入口檔案 | `index.html` |
| 狀態 | 線上可存取（HTTP 200） |

## 專案結構

```
.
├── index.html   # 網站主體：樣式、行程資料、互動邏輯全部內嵌於此檔
├── README.md    # 本文件
└── .gitignore
```

`index.html` 為完全自足的單一檔案：CSS 與 JavaScript 皆內嵌，行程資料以 `itinerary` 陣列寫在頁面內，因此除了 Google Maps 連結與頁首背景圖之外，其餘內容不需網路即可瀏覽。

## 功能

- **日期分頁**：依 `day` 欄位（`1` / `2` / `3` / `other`）切換行程。
- **關鍵字搜尋**：搜尋地點、時間或備註，即時過濾行程節點。
- **Google Maps 導航**：每個節點與每日路線提供導航按鈕，可帶入途經點與單車模式。
- **行程內建**：無需上傳檔案即可檢視完整行程。

## 本機預覽

直接以瀏覽器開啟 `index.html`，或起一個本機靜態伺服器：

```bash
python -m http.server 8000
# 開啟 http://localhost:8000/
```

## 部署方式

Repo 採用 GitHub Pages 的「分支來源」模式，推送至 `main` 即自動重新部署：

```bash
git add .
git commit -m "update"
git push origin main
```

推送到 `main` 後約 1 分鐘生效；若未更新，至 Repo 的 **Actions** 頁面確認 `pages build and deployment` 是否成功，或到 **Settings → Pages** 檢查來源設定。

## 資料維護

行程內容維護於 `index.html` 內的 `itinerary` 陣列，每筆資料格式：

```js
{
  day: "1",                     // 分頁：1 / 2 / 3 / other
  title: "節點標題",
  fields: [                     // 顯示於節點的欄位
    { label: "出發時間", value: "11:30" }
  ],
  mapOptions: [                 // 導航按鈕
    { label: "按鈕文字", query: "Google Maps 搜尋字串" }
  ]
}
```

每日的整體路線導航另存於 `dailyRoutes` 物件，以 `day` 為 key，支援 `origin` / `waypoints` / `destination` / `travelmode` 等參數。

修改後直接提交並推送即可，不需建置流程。

## 原始資料

原始規劃檔為 `花東縱谷單車行程.xlsx`（僅存於本機，已由 `.gitignore` 排除，不會上傳至 Repo）。網站上的行程資料為該檔內容的手動整理版本，兩者不會自動同步。

## 注意事項

- 部分行程含時效性資訊（例如「玉富自行車道 3K+100 至 9K+100 封閉至 2026/12/31」），出發前請重新確認官方公告。
- 頁首背景圖來自 Pexels，需連網載入。
- `~$*.xlsx` 為 Excel 開啟檔案時產生的鎖定檔，已列入 `.gitignore`。
