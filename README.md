# KINYO 通路網紅追蹤表（GitHub Pages ＋ Firebase）

登入：Google 帳號　資料庫：Firebase Firestore　網址：GitHub Pages
網頁程式是公開的，但資料只有通過登入且在名單內的人讀得到、寫得進去。

## 一、建立 Firebase（約 10 分鐘，只做一次）

1. 到 https://console.firebase.google.com 用公司 Google 帳號建立專案（Analytics 可關閉）。
2. 左側「建構 → Authentication → 開始使用 → 登入方式」，啟用 **Google**。
3. 「Authentication → 設定 → 已授權的網域」新增你的 GitHub Pages 網域，例如 `你的帳號.github.io`。
4. 左側「建構 → Firestore Database → 建立資料庫」，選台灣或東亞區域，用正式版模式。
5. Firestore 的「規則」分頁，貼上 `firestore.rules` 的內容，按發布。
   只有規則裡名單內的信箱能用；新增人員就把 Gmail 加進名單再發布。
6. 「專案設定（齒輪）→ 您的應用程式 → 網頁 (</>)」註冊一個網頁應用程式，
   把畫面上的 `firebaseConfig` 四個值填進 `firebase-config.js`。

## 二、上傳到 GitHub 並開啟網址

1. 把這個資料夾的檔案（index.html、firebase-config.js、firestore.rules、README.md）放進倉庫根目錄。
2. 倉庫「Settings → Pages」，Source 選 Deploy from a branch、Branch 選 main、資料夾 `/ (root)`。
3. 幾分鐘後網址是 `https://你的帳號.github.io/倉庫名稱/`，把網址給同事即可。

## 三、搬移現有資料

1. 在原本 Claude 上的看板：設定 → 資料匯出／匯入 → 「產生匯出資料」→「複製」。
2. 打開新網址、登入、角色選「行銷」→ 設定 → 資料匯出／匯入，把內容貼到匯入框，按「匯入」。
3. 產品圖不能跟著搬（舊圖存在 Claude 裡），請在各型號的詳細頁重新上傳。
   新上傳的圖會縮小後直接存進資料庫，不需要另外開 Storage。

## 四、之後誰可以做什麼

| 需求 | 做法 |
| --- | --- |
| 看板使用、改資料 | 信箱在名單內，用 Google 登入即可，欄位權限依畫面上的「角色」分工 |
| 新增或移除可編輯的人 | Firestore 規則的信箱名單加或刪一行，按發布 |
| 修改程式或版面 | 在 GitHub 倉庫「Settings → Collaborators」加入對方，改 index.html 後 commit 到 main，Pages 會自動更新 |
| 更新程式會不會動到資料 | 不會，資料在 Firebase，不在 GitHub |

## 注意

- 「角色」是畫面上的分工，不是帳號權限；名單內的人都能讀寫。
- 離職人員要在 Firebase Authentication 的使用者清單停用或刪除。
- Firestore 免費額度對這個用量綽綽有餘。
