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
流程:
```bash
Project name: xxxxxx
Select a framework: React
Select a variant: JavaScript
Which linter to use: ESLint
Install with npm and start now: no
```

### 安裝 npm 套件並運行
流程:
```bash
cd xxx-project
npm install
npm run dev
```

### 建立 Git 版本控制
流程:
```bash
git init
git add .
git commit -m "feat: 新增 XXXXXX"
檢查 log: git log
```

## Vite 專案部屬
網址: https://github.com/

### 建立 github 新專案
流程:
1. github 首頁
2. Repositories
3. New
4. Repository name: XXXXXX
5. Create repository

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
> npm run build 是建立 dist 檔
> npm run deploy 是將 dist 部屬到 github  

流程:
```bash
npm run build
npm run deploy
```



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

## 加入 Sass

### 安裝 Sass
```bash
npm add -D sass
```

### 新增 all.scss
路徑: `src/assets/all.scss`  

寫入樣式:
```scss
$primary-bg: green;

body {
  background-color: $primary-bg;
}
```


### 修改 main.jsx
> 註解或刪除 `import './index.css'`  
> 載入 `import './assets/all.scss'`

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
// import './index.css'   //  註解或刪除
import App from './App.jsx'
import './assets/all.scss'  //  載入 all.scss

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

## 載入 Bootstrap 套件
網址: https://getbootstrap.com/

### 安裝 Bootstrap
```bash
npm i bootstrap
```

### 載入 bootstrap 樣式
**修改 all.scss**  
```scss
@import 'bootstrap/scss/bootstrap';
```
**修改 App.jsx**  
> 因測試先改 button 樣式  
> `className` 加入 `btn btn-primary` 樣式 
```jsx
<button
  type="button"
  className="counter btn btn-primary" //  加入 btn btn-primary 樣式
  onClick={() => setCount((count) => count + 1)}
>
  Count is {count}
</button>
```

### 客製化 bootstrap
流程:   
1. 複製 `node_modules/bootstrap/scss/` 底下的 `_variables-dark.scss`  與 `_variables.scss` 檔案
2. 貼到 `assets` 資料夾底下
3. 修改 `all.scss` 測試樣式
```scss
@import 'bootstrap/scss/functions';

$primary: red;

@import './variables';

@import 'bootstrap/scss/bootstrap';
```
### 使用 Modal 功能
流程:  
1. 將官網 `bootstrap` 的 `Modal` 其中範例 `Live demo` 程式碼複製到 `App.jsx`
2. 修改 `class` > `className` 跟 `tabindex` > `tabIndex` 名稱
3. 在 `main.jsx` 載入 `import 'bootstrap'`

**App.jsx**
```jsx
<button
  type="button"
  className="btn btn-primary"
  data-bs-toggle="modal"
  data-bs-target="#exampleModal"
>
  Launch demo modal
</button>

<div
  className="modal fade"
  id="exampleModal"
  tabIndex="-1"
  aria-labelledby="exampleModalLabel"
  aria-hidden="true"
>
  <div className="modal-dialog">
    <div className="modal-content">
      <div className="modal-header">
        <h1 className="modal-title fs-5" id="exampleModalLabel">
          Modal title
        </h1>
        <button
          type="button"
          className="btn-close"
          data-bs-dismiss="modal"
          aria-label="Close"
        ></button>
      </div>
      <div className="modal-body">...</div>
      <div className="modal-footer">
        <button
          type="button"
          className="btn btn-secondary"
          data-bs-dismiss="modal"
        >
          Close
        </button>
        <button type="button" className="btn btn-primary">
          Save changes
        </button>
      </div>
    </div>
  </div>
</div>
```
**main.jsx**
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'
import 'bootstrap'  // 載入 bootstrap
import './assets/all.scss'
// import './index.css'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

