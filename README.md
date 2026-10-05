# 越南旅行 Web App（10/8 – 10/12）

一個單頁、像手機 App 一樣的旅行小幫手，用 Vue.js + Tailwind CSS 製作。

| 檔案 | 用途 |
|---|---|
| `index.html` | 主程式（畫面 + 功能） |
| `style.css` | 粉彩配色與樣式 |
| `banner.jpg` | 頁首橫幅圖片（**要你自己上傳**） |

---

## 步驟 A：讓 App 上線（約 10 分鐘，用電腦操作比較方便）

### A1. 把檔案上傳到 GitHub
1. 準備好 3 個檔案放在同一個資料夾：`index.html`、`style.css`，以及你的橫幅圖片。
2. 把圖片「Web app Banner 素材」**改名成 `banner.jpg`**（如果是 PNG 就改成 `banner.png`）。
3. 打開專案頁面：<https://github.com/pengwei1307/-Vietnam1008-1012>
4. 專案是空的時候，畫面中間會有一行小字 **uploading an existing file**，點它。
   （專案已經有檔案的話，就點右上方 **Add file → Upload files**。）
5. 把 3 個檔案一起拖進虛線框裡，等進度條跑完。
6. 拉到最下面，按綠色的 **Commit changes**。

### A2. 開啟 GitHub Pages（把它變成網站）
1. 在專案頁面點上方的 **Settings**（齒輪）。
2. 左側選單點 **Pages**。
3. 在 **Build and deployment → Source** 選 **Deploy from a branch**。
4. **Branch** 選 `main`，資料夾選 `/ (root)`，按 **Save**。
5. 等 1～2 分鐘後重新整理這一頁，上方會出現 **Your site is live at https://…**，這就是你的 App 網址！

> 如果 Pages 頁面說需要升級付費方案，代表這個 repo 是 Private（私人）的。
> 到 **Settings → General**，拉到最底的 **Danger Zone → Change visibility**，改成 **Public** 即可免費使用。

### A3. 加到手機主畫面（變成 App 圖示）
- **iPhone（Safari）**：打開網址 → 點下方「分享」按鈕 → **加入主畫面**。
- **Android（Chrome）**：打開網址 → 右上角 ⋮ → **加到主畫面**。

### A4. 開始使用
1. 點左上角 **加入成員** → 輸入密碼 **0125** → 設定暱稱和頭貼。
2. 成為成員後，就能新增／編輯行程、購物清單、便利貼和花費。

---

## 步驟 B（選做）：讓所有旅伴資料同步

沒做這一步，**每個人的資料只會存在自己的手機裡**。
如果希望大家看到同一份行程、互相留言，就要接上免費的 Google Firebase 資料庫：

1. 到 <https://console.firebase.google.com> 用 Google 帳號登入 → **建立專案**（名稱隨意，Google Analytics 可以關掉）。
2. 左側選單 **建構 (Build) → Firestore Database** → **建立資料庫** → 地區選 `asia-east1 (台灣)` → 選 **以測試模式啟動** → 建立。
3. 回到專案首頁，點 **`</>`（網頁）** 圖示新增一個網頁應用程式，暱稱隨意，按註冊。
4. 畫面會出現一段 `const firebaseConfig = { ... }`，把 **大括號裡的內容** 複製起來。
5. 在 GitHub 打開 `index.html` → 點右上角鉛筆圖示（Edit this file）→ 找到這一行：
   ```js
   const FIREBASE_CONFIG = null;
   ```
   改成：
   ```js
   const FIREBASE_CONFIG = {
     apiKey: "……",
     authDomain: "……",
     projectId: "……",
     storageBucket: "……",
     messagingSenderId: "……",
     appId: "……"
   };
   ```
6. 按 **Commit changes**，等 1 分鐘，重新打開 App。「資訊」頁最下方顯示「已開啟雲端同步」就成功了。

> ⚠️ 測試模式的資料庫 30 天後會自動鎖起來，剛好涵蓋這次旅行。若要延長，到 Firestore 的「規則」把到期日改晚。
> 成員密碼只是防止誤改，不是真正的資安保護，請不要在 App 裡放護照號碼等敏感資料。

---

## 常見修改

所有設定都在 `index.html` 的 `<script>` 最上方，用 ①～⑦ 標示：

- **改密碼**：`MEMBER_PIN`
- **補飯店電話**：`HOTELS` 裡的 `phone: ''`
- **改預設行程**：`SEED_ITINERARY`（只會在第一次開啟時寫入，之後請直接在 App 裡改）
- **改配色**：`style.css` 最上面的 `:root` 色碼

## 功能說明

- **天氣**：使用 Open-Meteo，出發前約 2 週內才有預報。
- **匯率**：使用 open.er-api.com 每日匯率，沒網路時會用上次的匯率。
- **交通時間**：依兩地距離估算（步行／開車／大眾運輸），點擊可開啟 Google 地圖看即時路線。
  想更準，可以在行程裡填「座標」（Google 地圖長按地點即可複製）。
- **背景色**：會自動取用橫幅圖片底部的顏色。
