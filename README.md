# TCFSH 2026 校園風雲人物提名系統

基於 Google Apps Script (GAS) 與 Google Identity Services 構建之「臺中一中 2026 校園風雲人物（校草、校花、校猴）」票選與提名系統。本專案以 React (Vite) + Tailwind CSS 進行開發，並使用 GitHub Actions 自動部署至 GitHub Pages。

## 系統特色

- 🌟 現代化玻璃擬物與霓虹發光風格介面 (Glassmorphism + Neon theme)
- 🔐 整合 Google Identity Services 登入，防範灌票
- 🛡️ 自動辨識 @std.tcfsh.tc.edu.tw 一中生認證信箱
- 📄 使用 Google Apps Script 串接至 Google Sheets 作為後台資料庫
- 📸 支援圖片上傳與預覽
- 📱 響應式排版，完全適配手機操作體驗
- ⚖️ 內建「投票規範與隱私條款」同意流程

## 開始使用

### 1. 取得 Google Client ID
1. 前往 [Google Cloud Console](https://console.cloud.google.com/)
2. 建立新專案或選擇現有專案
3. 進入「API 與服務 > 憑證」，建立「OAuth 用戶端 ID (網頁應用程式)」
4. 將您的 GitHub Pages URL 加入「已授權的 JavaScript 來源」

### 2. 部署 Backend (Google Apps Script)
1. 建立一個 Google Sheets 表單
2. 點擊「擴充功能 > Apps Script」
3. 貼上您的後端 doPost 處理常式
4. 點擊「部署 > 新增部署作業」，選擇「網頁應用程式」，並設定「任何人」皆可存取
5. 複製生成的 Web App URL

### 3. 設定環境變數
在專案根目錄中建立 `.env` 檔案，並填入剛才取得的資訊：

```env
VITE_GOOGLE_CLIENT_ID="你的_CLIENT_ID.apps.googleusercontent.com"
VITE_GAS_URL="你的_GOOGLE_APPS_SCRIPT_WEB_APP_URL"
```

## 本地開發

確保安裝 [Node.js](https://nodejs.org/):

```bash
# 安裝依賴
npm install

# 啟動開發伺服器
npm run dev
```

## GitHub Actions 自動部署

本專案已包含 `.github/workflows/deploy.yml` 配置檔以供 GitHub Pages 部署使用。

1. 修改 `package.json` 中的 `homepage` 或是 `vite.config.ts` 內的 `base` 路徑（如果您部署在非根目錄的 GitHub Pages）。
2. 在 GitHub 的 repository 頁面中，前往 **Settings > Pages**。
3. 將 **Source** 設為 **GitHub Actions**。
4. 在 GitHub 頁面上設定 **Repository secrets** 如果你要在打包時傳入這兩個變數，您也可以直接在 GitHub Action 裡面把變數替換好，或者先確認 .env 檔案不會外洩機密。
5. 將更改 push 至 `main` 分支，GitHub Actions 將會自動編譯並發布。

### 環境變數至 GitHub
如果你想將變數隱藏，請至 Repo > Settings > Secrets and variables > Actions 添加:
- `VITE_GOOGLE_CLIENT_ID`
- `VITE_GAS_URL`

並修改 `.github/workflows/deploy.yml`：
```yaml
      - name: Build
        run: npm run build
        env:
          VITE_GOOGLE_CLIENT_ID: ${{ secrets.VITE_GOOGLE_CLIENT_ID }}
          VITE_GAS_URL: ${{ secrets.VITE_GAS_URL }}
```

## 開發工具
- [React 19](https://react.dev/)
- [Vite](https://vitejs.dev/)
- [Tailwind CSS v4](https://tailwindcss.com/)
- [Framer Motion](https://motion.dev/)
- [Lucide Icons](https://lucide.dev/)
