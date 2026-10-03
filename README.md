# React review 2026

## Vite 安裝與 React 開發環境建立
### Node.js 安裝
網址: https://nodejs.org/en
流程: node.js 首頁 > Get Node.js > Windows Installer(.msi) > 安裝 LTS 版本

### Vite 環境建立
網址: https://vite.dev/

1. 檢查 node.js 版本 
```bash
node -v
```
2. 建立 Vite 專案
```bash
npm create vite@latest
```
流程: Project name: xxxxxx > Select a framework: React > Select a variant: JavaScript > Which linter to use: ESLint > Install with npm and start now: no

3. 安裝 npm 套件並運行  
流程: cd xxx-project > npm install > npm run dev

4. 建立 Git 版本控制  
流程: git init > git add . > git commit -m "feat: 新增 XXXXXX" > 檢查 log: git log

### Vite 專案部屬
網址: https://github.com/

1. 建立 github 新專案  
流程: github 首頁 > Repositories > New > Repository name: XXXXXX > Create repository

2. 部屬本地專案到 github
指令:
```bash
git remote add origin https://github.com/EasyToGet/test2026.git
git branch -M main
git push -u origin main
```

### 安裝 gh-pages 套件與部屬
1. 安裝 gh-pages
指令:
```bash
npm install gh-pages
```

2. 修改 package.json
```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint .",
    "preview": "vite preview",
    "deploy": "gh-pages -d dist"  // 加入此行
  },
}
```

3. 部屬 gh-pages  
流程: npm run build > npm run deploy

> npm run build 是建立 dist 檔
> npm run deploy 是將 dist 部屬到 github

4. 修改專案路徑
**修改 vite.config.js** 

```jsx
import react from '@vitejs/plugin-react'
import { defineConfig } from 'vite'

// https://vite.dev/config/
export default defineConfig({
  // 開發中、產品路徑
  base: process.env.NODE_ENV === 'production' ? '/react2026/' : '/',
  plugins: [react()],
})
```

> 在 defineConfig 裡加入
> `base: process.env.NODE_ENV === 'production' ? '/專案名稱/' : '/'`
