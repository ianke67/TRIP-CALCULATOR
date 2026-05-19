# 旅遊記帳小幫手

## 檔案說明
```
index.html      主程式（所有功能都在這裡）
manifest.json   PWA 設定（讓手機可以加入桌面）
sw.js           Service Worker（離線快取）
icon-192.png    App 圖示
icon-512.png    App 圖示（大）
```

---

## 部署步驟

### 第一步：上傳到 GitHub Pages

1. 去 [github.com](https://github.com) 建立新 repo（建議設為 Public）
2. 把這 5 個檔案全部上傳到 **根目錄**（不要放在子資料夾）
3. 進入 Settings → Pages → Source 選 `main` branch → Save
4. 等 1～2 分鐘，你的網址就是 `https://你的帳號.github.io/repo名稱/`

### 第二步：在手機加入桌面（PWA）

**iOS（Safari）：**
1. 用 Safari 打開你的網址
2. 點下方分享按鈕 →「加入主畫面」
3. 完成！桌面會出現 App 圖示

**Android（Chrome）：**
1. 用 Chrome 打開你的網址
2. 瀏覽器會自動出現「加入主畫面」提示，或點右上角選單 →「安裝應用程式」
3. 完成！

---

## Firebase 設定（跨裝置同步，選用）

### 建立 Firebase 專案
1. 前往 [console.firebase.google.com](https://console.firebase.google.com)
2. 建立新專案（關閉 Google Analytics 就好，比較快）
3. 點「新增應用程式」→ 選「Web」（`</>`）→ 給個名稱 → 複製 `firebaseConfig` 裡的值

### 啟用服務
1. **Authentication** → 開始使用 → 啟用 `Google` 登入方式
2. **Firestore Database** → 建立資料庫 → 選「正式模式」→ 選離你近的地區（asia-east1 = 台灣）

### 設定安全性規則
在 Firestore → 規則，把規則改成這樣：
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth.uid == userId;
    }
  }
}
```
這樣只有本人才能讀寫自己的資料。

### 把設定填入 App
打開 App → 右上角齒輪 → 貼入 Firebase 設定 → 儲存 → 用 Google 帳號登入

---

## 更新 App

只要修改 `index.html` 推上 GitHub，手機下次打開時會自動更新。
