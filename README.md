# Panel.NA1 自动挂机 - HuggingFace 部署指南

> ⭐ **觉得有用？给个 Star 支持一下！**

在 Hugging Face 免费部署自动挂机程序，持续赚取 [Panel.NA1](https://panel.na1.host) 金币。

![示例输出](UI.png)

## ✨ 功能特性

| 功能 | 说明 |
|------|------|
| 🤖 自动挂机 | 每分钟自动签到，持续赚取金币 |
| 📊 实时监控 | Web 面板显示金币、收益、在线人数 |
| 🛡️ 自动保活 | 防止 HuggingFace Space 休眠 |
| 📱 TG 通知 | 可选的 Telegram 状态推送 |
| 🔄 自动恢复 | Cookie 自动刷新，长期稳定运行 |

---

## ⚠️ 前置条件

> **必须先完成此步骤，否则无法挂机赚取金币！**

1. 登录 [panel.na1.host](https://panel.na1.host)
2. 进入 **钱包** 页面
3. 点击 **添加钱包**，随便输入一个名字即可
4. 完成后再进行下面的部署步骤

---

## 🚀 快速部署

### 第一步：创建 Space

1. 打开 [HuggingFace Spaces](https://huggingface.co/spaces)
2. 点击 `+ New Space` → 选择 `Gradio` → 创建

### 第二步：配置环境变量

进入 `Settings` → `Variables and secrets` → `New secret`

| 变量名 | 说明 | 必填 |
|--------|------|:----:|
| `PANEL_NA1_COOKIES` | NA1 登录 Cookie | ✅ |
| `PROJECT_URL` | Space 保活链接 | ❌ |
| `TG_BOT_TOKEN` | Telegram Bot Token | ❌ |
| `TG_CHAT_ID` | Telegram 聊天 ID | ❌ |
| `TG_API_URL` | Telegram API 反代地址 | ❌ |

### 第三步：上传文件

上传以下文件到 Space，完成后自动运行：

```
├── app.py              # 主程序
├── requirements.txt    # 依赖
└── README.md           # 说明文档
```

### 第四步：访问监控面板

部署完成后，访问以下地址查看运行状态：

```
https://用户名-项目名.hf.space/na1
```

---

## 🔧 配置说明

### 🍪 获取 Cookie

1. 登录 [panel.na1.host](https://panel.na1.host)
2. 按 `F12` → 切换到 `Network` 标签
3. 刷新页面 → 点击任意请求
4. 在 `Headers` → `Cookie` 中复制完整内容

```
# Cookie 格式示例
crisp-client%2Fsession%2XXX=session_XXX; remember_web_XXX; XSRF-TOKEN=eyJXXX; pterodactyl_session=eyJXXX
```

> ⚠️ 确保包含 `XSRF-TOKEN`、`pterodactyl_session`、`remember_web`

### 🔗 获取保活链接

1. 打开你的 Space 页面
2. 点击右上角 `⋮` → `Embed this Space`
3. 复制 **Direct URL**

```
# 链接格式
https://用户名-项目名.hf.space
```

> 💡 设置后自动注册保活服务，防止 Space 休眠

### 📱 Telegram 通知配置

> ⚠️ **重要**：HuggingFace 无法直接访问 `api.telegram.org`，必须配置反代才能收到通知

| 变量 | 说明 |
|------|------|
| `TG_BOT_TOKEN` | 从 [@BotFather](https://t.me/BotFather) 获取 |
| `TG_CHAT_ID` | 从 [@userinfobot](https://t.me/userinfobot) 获取 |
| `TG_API_URL` | Telegram API 反代地址 |

**反代地址格式：**
```
# 不带斜杠结尾
https://your-tg-proxy.com
```

> 💡 可使用 Cloudflare Workers 自建反代，确保稳定性

---

## 📡 API 接口

| 端点 | 说明 | 响应示例 |
|------|------|----------|
| `GET /` | 健康检查 | `{"status":"ok","coins":1250,"earned":58}` |
| `GET /na1` | Web 监控面板 | HTML 页面 |

---

## 📊 状态说明

| 运行状态 | 含义 |
|:--------:|------|
| 🟢 运行中 | 正常挂机 |
| 🟡 启动中 | 正在初始化 |
| 🔴 未配置 | 未设置 Cookie |
| 🔴 已过期 | Cookie 失效，需更新 |

| 保活状态 | 含义 |
|:--------:|------|
| 🛡️ 保活 | 已启用 |
| ⏭️ 跳过 | 未配置 PROJECT_URL |
| ⚠️ 失败 | 注册失败 |

---

## ❓ FAQ

<details>
<summary><b>Cookie 多久过期？</b></summary>

NA1 Cookie 有效期较长，程序会自动刷新。若显示"已过期"，需重新获取并更新环境变量。
</details>

<details>
<summary><b>为什么需要保活？</b></summary>

HuggingFace 免费 Space 无访问时会自动休眠。设置 `PROJECT_URL` 后注册外部保活服务，定期访问防止休眠。
</details>

<details>
<summary><b>为什么收不到 Telegram 通知？</b></summary>

HuggingFace 网络限制无法直接访问 `api.telegram.org`，必须配置 `TG_API_URL` 反代地址。可使用 Cloudflare Workers 自建反代。
</details>

<details>
<summary><b>金币有什么用？</b></summary>

NA1 金币可兑换服务器资源，详见 [NA1 官网](https://panel.na1.host)。
</details>

---

## 📜 免责声明


本项目仅供学习交流，请遵守 [panel.na1.host](https://panel.na1.host) 服务条款。使用本程序产生的任何后果由用户自行承担。

