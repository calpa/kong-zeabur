# 🌐 Kong Gateway OSS (無資料庫模式) on Zeabur

<div align="center">

[![Kong Gateway](https://camo.githubusercontent.com/733593a5edce1e6474a3a82297582a813bbee7ba2edee6db8b35aa8c744a1e83/68747470733a2f2f6b6f6e6768712e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031382f30352f6b6f6e672d6c6f676f2d6769746875622d726561646d652e706e67)](https://zeabur.com/templates/QUF7QG)

![Kong 版本](https://img.shields.io/badge/Kong-3.10.0.1-blue)
![授權條款](https://img.shields.io/badge/License-MIT-green)

[English README](README.md)

</div>

## ✨ 功能特點

- 🚀 **一鍵部署** 在 Zeabur 上
- 🗄️ **無資料庫** - 完全在記憶體中運行
- 📝 **宣告式配置** - 使用程式碼定義路由和外掛
- 🔌 **預先配置** 包含 httpbin 範例服務
- 🌐 **自訂網域** 支援
- 📊 **Kong Manager** 管理介面
- 🔄 **無狀態** - 適合無伺服器和容器化環境

## 🚀 部署方式

### 選項一：一鍵部署（推薦）

[![部署到 Zeabur](https://zeabur.com/button.svg)](https://zeabur.com/templates/QUF7QG)

1. 點擊上方的「Deploy on Zeabur」按鈕
2. 設定您偏好的網域名稱
3. 開始部署！🚀

### 選項二：使用 Zeabur CLI

```bash
# 如果尚未安裝 Zeabur CLI
npm install -g @zeabur/cli

# 部署模板
zeabur template deploy kong-db-less.yml

# 或更新現有模板
zeabur template update -c QUF7QG -f kong-db-less.yml
```

## ⚙️ 配置設定

### 環境變數

| 變數名稱 | 描述 | 預設值 |
|----------|-------------|---------|
| `KONG_DATABASE` | 資料庫模式（無資料庫模式始終為 `off`） | `off` |
| `KONG_DECLARATIVE_CONFIG` | 宣告式配置檔案路徑 | `/kong/declarative/kong.yml` |
| `KONG_ADMIN_LISTEN` | 管理 API 監聽地址 | `0.0.0.0:8001` |
| `KONG_PROXY_ACCESS_LOG` | 代理訪問日誌位置 | `/dev/stdout` |
| `KONG_NGINX_WORKER_PROCESSES` | Worker 進程數量 | `1` |

### 自訂配置

編輯 `volumes` 區段中的 `kong.yml` 檔案來自訂您的 Kong Gateway 配置。配置使用宣告式 YAML 格式編寫。

## 💡 使用說明

### 訪問服務

- **Kong 代理**：`https://您的網域.zeabur.app`
  - 範例路由：`https://您的網域.zeabur.app/httpbin`
- **Kong Manager 管理介面**：`https://您的網域.zeabur.app:8002`
- **狀態端點**：`https://您的網域.zeabur.app/status`

### 預設路由

- `/httpbin` - 代理到 httpbin.org（範例服務）
- `/status` - 健康檢查端點

## 🔧 開發指南

### 更新模板

1. 修改 `kong-db-less.yml` 檔案
2. 在 Zeabur 上更新模板：
   ```bash
   npx zeabur template update -c QUF7QG -f kong-db-less.yml
   ```

### 本地測試

1. 安裝 [Docker](https://www.docker.com/)
2. 在本地運行 Kong Gateway：
   ```bash
   docker run -d --name kong \
     -e "KONG_DATABASE=off" \
     -e "KONG_DECLARATIVE_CONFIG=/kong.yml" \
     -v $(pwd)/kong.yml:/kong.yml \
     -p 8000:8000 \
     -p 8001:8001 \
     kong/kong-gateway:3.10.0.1
   ```

## 🔒 安全性

- 🔐 管理 API（端口 8001）不會暴露在網際網路上
- 🔒 生產環境請考慮添加身份驗證
- 🔄 定期更新至最新版 Kong Gateway
- 🔒 檢視並自訂預設的 CORS 和速率限制設定

## 📄 授權條款

本專案採用 [MIT 授權條款](LICENSE)。

---

<div align="center">
  由 <a href="https://calpa.me">Calpa</a> 用 ❤️ 製作
</div>
