# 🌐 Kong Gateway OSS (DB-less Mode) on Zeabur

<div align="center">

[![Kong Gateway](https://camo.githubusercontent.com/733593a5edce1e6474a3a82297582a813bbee7ba2edee6db8b35aa8c744a1e83/68747470733a2f2f6b6f6e6768712e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031382f30352f6b6f6e672d6c6f676f2d6769746875622d726561646d652e706e67)](https://zeabur.com/templates/QUF7QG)

![Kong Version](https://img.shields.io/badge/Kong-3.10.0.1-blue)
![License](https://img.shields.io/badge/License-MIT-green)

[✨ Features](#-features) ·
[🚀 Deployment](#-deployment) ·
[⚙️ Configuration](#-configuration) ·
[💡 Usage](#-usage) ·
[🔧 Development](#-development) ·
[🔒 Security](#-security)

</div>

## ✨ Features

- 🚀 **One-Click Deployment** on Zeabur
- 🗄️ **Database-less** - Runs entirely in-memory
- 📝 **Declarative Configuration** - Define routes and plugins as code
- 🔌 **Pre-configured** with a sample httpbin service
- 🌐 **Custom Domain** support
- 📊 **Kong Manager** included
- 🔄 **Stateless** - Perfect for serverless and containerized environments

## 🚀 Deployment

### Option 1: One-Click Deployment (Recommended)

[![Deploy on Zeabur](https://zeabur.com/button.svg)](https://zeabur.com/templates/QUF7QG)

1. Click the "Deploy on Zeabur" button above
2. Set your preferred domain name
3. Deploy! 🚀

### Option 2: Using Zeabur CLI

```bash
# Install Zeabur CLI if you haven't
npm install -g @zeabur/cli

# Deploy the template
zeabur template deploy kong-db-less.yml

# Or update an existing template
zeabur template update -c QUF7QG -f kong-db-less.yml
```

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `KONG_DATABASE` | Database mode (always `off` for DB-less) | `off` |
| `KONG_DECLARATIVE_CONFIG` | Path to declarative config | `/kong/declarative/kong.yml` |
| `KONG_ADMIN_LISTEN` | Admin API listen address | `0.0.0.0:8001` |
| `KONG_PROXY_ACCESS_LOG` | Proxy access log location | `/dev/stdout` |
| `KONG_NGINX_WORKER_PROCESSES` | Number of worker processes | `1` |

### Custom Configuration

Edit the `kong.yml` file in the `volumes` section to customize your Kong Gateway configuration. The configuration is written in declarative YAML format.

## 💡 Usage

### Accessing Services

- **Kong Proxy**: `https://your-domain.zeabur.app`
  - Sample route: `https://your-domain.zeabur.app/httpbin`
- **Kong Manager UI**: `https://your-domain.zeabur.app:8002`
- **Status Endpoint**: `https://your-domain.zeabur.app/status`

### Default Routes

- `/httpbin` - Proxies to httpbin.org (example service)
- `/status` - Health check endpoint

## 🔧 Development

### Updating the Template

1. Make your changes to `kong-db-less.yml`
2. Update the template on Zeabur:
   ```bash
   npx zeabur template update -c QUF7QG -f kong-db-less.yml
   ```

### Testing Locally

1. Install [Docker](https://www.docker.com/)
2. Run Kong Gateway locally:
   ```bash
   docker run -d --name kong \
     -e "KONG_DATABASE=off" \
     -e "KONG_DECLARATIVE_CONFIG=/kong.yml" \
     -v $(pwd)/kong.yml:/kong.yml \
     -p 8000:8000 \
     -p 8001:8001 \
     kong/kong-gateway:3.10.0.1
   ```

## 🔒 Security

- 🔐 Admin API (port 8001) is not exposed to the internet
- 🔒 Consider adding authentication for production use
- 🔄 Regularly update to the latest Kong Gateway version
- 🔒 Review and customize the default CORS and rate limiting settings

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">
  Made with ❤️ by <a href="https://calpa.me">Calpa</a>
</div>
