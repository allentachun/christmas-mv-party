聖誕 MV 猜歌計分網站 V4：GitHub Pages + Firebase（可選）

一、先上傳到 GitHub 儲存庫的最外層
  index.html
  firebase-config.js

GitHub Pages > Deploy from branch > main > /(root)
網站：https://allentachun.github.io/christmas-mv-party/

二、單機主持人模式
  上傳上面兩個檔案後就能在 Safari 使用。
  無須 Firebase。資料存在該手機瀏覽器，請定期匯出 JSON 備份。

三、多人連線（需要 Firebase）
  1. Firebase 保持 Spark 免費方案，不綁 Cloud Billing。
  2. Firebase Console > 專案設定 > Your apps > Web app > Config，複製網頁 firebaseConfig。
  3. GitHub 編輯 firebase-config.js，替換 YOUR_... 佔位符。不放 Service Account 或金鑰 JSON。
  4. Firebase Console > Authentication > Sign-in method > Anonymous > Enable。
  5. Firestore Database > 建立資料庫；在 Rules 分頁貼入 firestore.rules，按 Publish。
  6. GitHub 上傳更新後，開啟網站 > 設定 > 多人連線。
  7. 主持人先在單機名單輸入 6-10 個姓名，再點「建立新房間」，分享連結或房間代碼。
  8. 參賽者用自己的 Safari 開啟網頁，選自己的席位加入。
  9. 主持人逐階段開放答題，玩家提交答案。主持人查看私密答案、停止收件、判定哪一階段猜中，最後輸入 KTV 分數並儲存。
  10. 每位參賽者從自己手機提交兩項人氣獎票選，主持人公布後自動結算分數。

安全注意
  - Firebase Web Config 可公開；Service Account 私鑰、GitHub Token 不可公開。
  - 必須使用附上的 Firestore Rules，不能把規則改為 allow read, write: if true。
  - 房間代碼不是安全密碼；Anonymous 登入不能強力防止一個人佔多個席位。
  - 主持人被授權判定歌名、演唱分數與人氣獎。沒有可信後端，無法防止惡意主持人改分數；適合熟人派對而非公開競賽。
  - 玩家作答沒有權限修改既有答案，也不能讀取其他玩家答案。主持人可查看及確認。
  - 資料長期保留在 Firestore（目前沒有自動刪除）；活動後可在 Console 刪除 rooms 集合相關資料。
  - Firebase 同步需要網路。若超出 Spark 免費額度，服務可能中斷，但不應為此升級 Blaze。

重要限制
  - 此版含 Firebase 連線程式與規則，但尚未在你的 Firebase 專案中實際部署、連線驗證。
  - GitHub 僅提供靜態網頁，真正即時同步由 Firebase 負責。
  - 只有主持人手機的單機資料可以匯出 JSON，雲端的排名可以匯出 CSV。
