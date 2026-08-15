# Simple Full Stack Demo

這是一個給初學者使用的前後端教學專案。

## 專案結構

```text
simple-fullstack-render-demo/
├── backend/
│   ├── main.py
│   └── requirements.txt
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── script.js
├── README.md
└── 前後端部署.md
```

## 1. 先在本地端成功跑起來

### 啟動 Backend

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

開啟：

```text
http://127.0.0.1:8000
```

FastAPI Docs：

```text
http://127.0.0.1:8000/docs
```

### 啟動 Frontend

可以用 VS Code 的 Live Server，開啟：

```text
frontend/index.html
```

或使用本地 Python 伺服器：

```bash
cd frontend
python -m http.server 5500
```

開啟：

```text
http://127.0.0.1:5500
```

> 目前先不要部署到 Render。先把專案在本地端跑通，確認前後端可正常溝通。

## 2. 前端先部署到 GitHub Pages

當本地端功能正常後，前端可以先部署到 GitHub Pages。

### 目前設定

```javascript
const API_URL = "http://127.0.0.1:8000";
```

這是本地開發用的設定，方便先測試前後端連線。

等前端上傳到 GitHub Pages 後，再視情況改成正式可用的 URL。

## 3. 後續再考慮 Render

如果之後想把 Python Backend 也公開上線，再部署到 Render。

這個時候再修改：

```javascript
const API_URL = "https://your-service.onrender.com";
```

但現在的核心目標是：

1. 本地端先跑成功
2. Frontend 先部署到 GitHub Pages
3. 後端先不用急著上 Render

## 4. 建議的學習順序

1. 在本地成功啟動 backend
2. 在本地成功啟動 frontend
3. 測試 API /docs
4. 確認前後端可以互相傳送資料
5. 之後再把 frontend 部署到 GitHub Pages
6. 最後才討論 Render 部署

## 5. 常用指令

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

```bash
cd frontend
python -m http.server 5500
```
