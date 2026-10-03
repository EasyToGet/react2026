# React + Vite + gh-pages + axios + Sass + Bootstrap 開發環境建立

## Node.js 安裝
網址: https://nodejs.org/en  
流程: node.js 首頁 > Get Node.js > Windows Installer(.msi) > 安裝 LTS 版本

## Vite 環境建立
網址: https://vite.dev/

### 檢查 node.js 版本
```bash
node -v
```
### 建立 Vite 專案
```bash
npm create vite@latest
```
流程: Project name: xxxxxx > Select a framework: React > Select a variant: JavaScript > Which linter to use: ESLint > Install with npm and start now: no

### 安裝 npm 套件並運行
流程: cd xxx-project > npm install > npm run dev

### 建立 Git 版本控制
流程: git init > git add . > git commit -m "feat: 新增 XXXXXX" > 檢查 log: git log

## Vite 專案部屬
網址: https://github.com/

### 建立 github 新專案
流程: github 首頁 > Repositories > New > Repository name: XXXXXX > Create repository

### 部屬本地專案到 github
指令:
```bash
git remote add origin https://github.com/EasyToGet/test2026.git
git branch -M main
git push -u origin main
```

## 安裝 gh-pages 套件與部屬
### 安裝 gh-pages
指令:
```bash
npm install gh-pages
```

### 修改 package.json
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

### 部屬 gh-pages
流程: npm run build > npm run deploy

> npm run build 是建立 dist 檔
> npm run deploy 是將 dist 部屬到 github

### 修改專案路徑
#### 修改 vite.config.js
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

## 載入 axios 套件
**randomuser**  
網址: https://randomuser.me/
> 取得假資料

**axios**  
網址: https://www.npmjs.com/package/axios  

### 安裝 axios
```bash
npm install axios
```

### 寫入 axios
**修改 App.jsx**  
```jsx
//  載入外部資源
import { useState, useEffect } from 'react'   //  {} 加入 useEffect
import axios from 'axios'   //  axios 套件載入

//  載入內部資源
import heroImg from './assets/hero.png'
import reactLogo from './assets/react.svg'
import viteLogo from './assets/vite.svg'
import './App.css'

function App() {
  const [count, setCount] = useState(0)

  //  測試 axios 程式碼 起始位置
  useEffect(() => {
    (async () => {
      const res = await axios.get('https://randomuser.me/api/');
      console.log(res);
    })()
  }, [])
  //  測試 axios 程式碼 結束位置

  return (
    <>
    </>
  )
}

export default App
```

> 使用 useEffect 必須寫入 `import { useState, useEffect } from 'react'`  
> 使用 axios 必須寫入 `import axios from 'axios' `  
> 測試 axios 程式碼  
```jsx
useEffect(() => {
  (async () => {
    const res = await axios.get('https://randomuser.me/api/');
    console.log(res);
  })()
}, [])
```