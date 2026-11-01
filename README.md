# 最小 GitHub Pages 靜態網頁

首頁僅顯示「與連芯心理師的諮商經驗及臺北市諮商心理師公會申訴結果」。白底、深色文字，支援手機，無外部字型、套件或建置需求。本專案不包含任何申訴文件、附件或申訴內文。

## 檔案與目前狀態

- `index.html`：首頁，內含 CSS 及 GA4 gtag.js 載入邏輯。
- `README.md`：本部署說明。
- **GA4 尚未啟用**：Measurement ID 仍是佔位符；原始狀態不載入 gtag.js，不傳送 Analytics 資料。
- 目前僅有本機檔案；尚未上傳 GitHub，也未啟用 GitHub Pages。

可直接用瀏覽器開啟 `index.html` 檢視排版。這只是本機預覽，不代表已發布或已完成追蹤驗證。

## 啟用 GitHub Pages

1. 登入 GitHub，建立空白儲存庫，例如 `counseling-experience`。GitHub Free 可使用公開儲存庫的 Pages。
2. 解壓縮後，將 `index.html` 和 `README.md` 直接上傳到儲存庫 `main` 分支的根目錄。不要只上傳 ZIP 或把檔案再包在下一層資料夾。
3. 在儲存庫中選擇 **Settings → Pages**。
4. 在 **Build and deployment** 中，將 **Source** 設為 **Deploy from a branch**。
5. **Branch** 選擇 `main`，資料夾選擇 **/ (root)**，按 **Save**。
6. 等待部署完成；同一頁會顯示網站網址。必要時到 **Actions** 查看 Pages 部署狀態。
7. 一般專案網站網址為 `https://你的帳號.github.io/counseling-experience/`。以 Settings → Pages 實際顯示的網址為準。
8. 開啟該網址，確認中文標題正確，手機畫面沒有橫向溢出。

公開儲存庫中的 README 與原始碼也可被讀取；上傳時只選取本專案檔案，不要上傳整個諮商資料夾。網站部署後可被公開存取。

## 建立 GA4 網站資料串流

1. 前往 https://analytics.google.com/ 並登入。若尚無 Analytics 帳戶，依畫面建立帳戶。
2. 在 **管理 → 建立 → 資源** 建立 GA4 資源，輸入名稱，選擇適用時區（例如臺灣）與貨幣，完成畫面要求。
3. 在 **管理 → 資料收集和修改 → 資料串流** 選擇 **新增串流 → 網站**；若剛建立資源，也可直接從設定流程選擇網站。
4. 輸入已部署的完整 GitHub Pages 網址與串流名稱，確認 HTTPS，建立串流。
5. 本專案只需要基本頁面瀏覽統計。可先關閉「加強型評估」以避免額外自動事件。
6. 在串流詳細資料複製 **評估 ID（Measurement ID）**，格式為 `G-` 開頭。不要使用數字串流 ID、資源 ID 或 `GTM-` 容器 ID。

## 填入 Measurement ID

在 `index.html` 找到：

```js
const measurementId = 'G-REPLACE_WITH_YOUR_MEASUREMENT_ID';
```

僅將引號內的佔位符替換為你的實際 `G-` 開頭 ID，再將更新後的 `index.html` 提交到 GitHub 的 `main` 分支。Pages 重新部署後，有效 ID 才會使程式載入 Google 的 gtag.js 並嘗試傳送資料；填入 ID 本身不代表追蹤已驗證成功。

程式使用 `page_title: '首頁'`，並移除傳送網址的查詢參數與片段，將 `page_referrer` 設為空字串，關閉 Google signals 及廣告個人化訊號。這些設定不等同匿名化或同意管理。不要在後續新增事件中傳送姓名、申訴文件或其他個人資料。

啟用後，訪客瀏覽器會連線至 Google 並可能使用 Analytics Cookie。本版本沒有 Cookie 同意介面或隱私告知頁；若日後需要這些功能，須另行加入。原始佔位符狀態不會進行上述 Analytics 連線。

## 驗證是否收到資料

1. 等待 GitHub Pages 新版部署成功，開啟正式網址。
2. 在 GA4 的「即時」報表查看自己的測試造訪，或使用 Google Tag Assistant 檢查標籤及目的地 ID。
3. 若沒有資料，確認使用正確 ID、網站已更新、瀏覽器允許 JavaScript，並檢查是否被擴充功能或網路規則阻擋。
4. 一般報表可能延後更新。僅在確實看到測試事件後，才可說已驗證收集成功。

GA4 的使用者與瀏覽次數是受 Cookie、瀏覽器及阻擋設定影響的估計，並非精確的人頭數；不會回補啟用前的瀏覽。

## robots.txt

此最小版本未加入 `robots.txt`，也未設定 `noindex`。robots.txt 不提供存取保護；搜尋引擎是否收錄與何時收錄也沒有保證。

## 官方說明

- GitHub Pages 發布來源：https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- GA4 資源及資料串流設定：https://support.google.com/analytics/answer/9304153?hl=zh-Hant
- Google tag / gtag.js：https://developers.google.com/tag-platform/gtagjs

介面名稱可能隨語言與產品更新略有不同。以上步驟於 2026-11-01 核對官方文件。