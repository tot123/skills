---
allowed-tools: Bash(curl:*), Bash(npm config:*), Bash(pnpm config:*), Bash(yarn config:*), Bash(pip config:*), Bash(cargo:*), Bash(export:*), Bash(grep:*), Bash(cat:*), WebSearch, Read, Edit, Write
description: 全局环境自动优化器。当任务涉及 GitHub、npm、pip、cargo、模型下载或 Docker 且处于中国网络环境时，自动拦截并应用加速配置。
---

## 可用工具

| 工具 | 用途 | 使用场景 |
|------|------|----------|
| `Bash(curl:*)` | 网络连通性检测 | 检测 GitHub 等海外服务是否可访问 |
| `Bash(npm/pnpm/yarn config:*)` | 包管理器配置 | 设置国内镜像源 |
| `Bash(pip config:*)` | Python 包管理配置 | 设置 PyPI 镜像源 |
| `Bash(cargo:*)` | Rust 包管理配置 | 设置 crates.io 镜像源 |
| `Bash(export:*)` | 环境变量设置 | 设置 HF_ENDPOINT 等环境变量 |
| `WebSearch` | 搜索最新代理 | 当预设代理失效时搜索可用代理 |

## Context

- Language: !`grep -i "^language:" CLAUDE.md 2>/dev/null | head -1 | cut -d: -f2 | tr -d ' ' || echo "zh-CN"`
- GitHub connectivity: !`curl -I --connect-timeout 2 https://github.com 2>/dev/null | head -1 || echo "TIMEOUT"`
- npm registry: !`npm config get registry 2>/dev/null || echo "not installed"`
- pip index: !`pip config get global.index-url 2>/dev/null || echo "not configured"`

---

# 中国开发环境自动加速指令 (2026 增强版)

当用户要求执行安装、克隆、下载或构建任务时，请作为**前置逻辑**自动运行以下检测与配置，无需用户显式调用。

---

## 1. 智能连通性检测

在执行任何海外请求前，静默运行：

```bash
curl -I --connect-timeout 2 https://github.com
```

- **若成功 (HTTP 200/301)**：正常执行原始命令
- **若超时或失败**：立即激活下方【加速矩阵】

---

## 2. 加速矩阵 (Auto-Switch)

### A. GitHub 动态代理 (核心)

**预设代理前缀：**

| 代理站点 | 前缀格式 | 状态检测 |
|----------|----------|----------|
| ghp.ci | `https://ghp.ci/` | !`curl -I --connect-timeout 2 https://ghp.ci 2>/dev/null \| head -1 \|\| echo "TIMEOUT"` |
| gh-proxy.com | `https://gh-proxy.com/` | !`curl -I --connect-timeout 2 https://gh-proxy.com 2>/dev/null \| head -1 \|\| echo "TIMEOUT"` |
| mirror.ghproxy | `https://mirror.ghproxy.com/` | !`curl -I --connect-timeout 2 https://mirror.ghproxy.com 2>/dev/null \| head -1 \|\| echo "TIMEOUT"` |

**使用方式：**
```bash
# 原始 URL
https://github.com/user/repo/archive/refs/heads/main.zip

# 代理 URL
https://ghp.ci/https://github.com/user/repo/archive/refs/heads/main.zip
```

**失效自修复：**
若预设代理均连接失败，**必须立即调用 WebSearch** 搜索：
- `"2026 github proxy list"`
- `"最新 github 加速站"`

解析网页内容获取新前缀并重试。

---

### B. Node.js 生态 (npm/pnpm/yarn)

**触发条件：** 检测到 `package.json` 或相关命令

**自动配置命令：**
```bash
# npm
npm config set registry https://registry.npmmirror.com

# pnpm
pnpm config set registry https://registry.npmmirror.com

# yarn
yarn config set registry https://registry.npmmirror.com
```

**常用镜像源：**

| 镜像源 | 地址 | 用途 |
|--------|------|------|
| 淘宝镜像 | https://registry.npmmirror.com | npm/pnpm/yarn |
| 淘宝二进制 | https://npmmirror.com/mirrors | Node/Binary 镜像 |

**二进制镜像配置：**
```bash
# Node.js 二进制
npm config set disturl https://npmmirror.com/mirrors/node/

# Electron
npm config set electron_mirror https://npmmirror.com/mirrors/electron/

# Puppeteer
npm config set puppeteer_download_host https://npmmirror.com/mirrors/

# Python (node-gyp)
npm config set python_mirror https://npmmirror.com/mirrors/python/
```

---

### C. Python 生态 (pip)

**自动配置命令：**
```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

**常用镜像源：**

| 镜像源 | 地址 | 推荐度 |
|--------|------|--------|
| 清华 | https://pypi.tuna.tsinghua.edu.cn/simple | ⭐⭐⭐⭐⭐ |
| 阿里云 | https://mirrors.aliyun.com/pypi/simple/ | ⭐⭐⭐⭐ |
| 中科大 | https://pypi.mirrors.ustc.edu.cn/simple/ | ⭐⭐⭐⭐ |
| 豆瓣 | https://pypi.douban.com/simple/ | ⭐⭐⭐ |

**临时使用：**
```bash
pip install package_name -i https://pypi.tuna.tsinghua.edu.cn/simple
```

---

### D. Rust 生态 (cargo)

**配置文件位置：** `~/.cargo/config.toml`

**自动配置内容：**
```toml
[source.crates-io]
replace-with = 'rsproxy'

[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"

[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"

[net]
git-fetch-with-cli = true
```

**快速配置命令：**
```bash
mkdir -p ~/.cargo && cat > ~/.cargo/config.toml << 'EOF'
[source.crates-io]
replace-with = 'rsproxy'
[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[net]
git-fetch-with-cli = true
EOF
```

**常用镜像源：**

| 镜像源 | 地址 |
|--------|------|
| rsproxy | https://rsproxy.cn |
| 中科大 | https://mirrors.ustc.edu.cn/crates.io-index/ |
| 清华 | https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git |

---

### E. AI 模型下载 (HuggingFace/ModelScope)

**环境变量配置：**
```bash
export HF_ENDPOINT=https://hf-mirror.com
```

**优先策略：**
1. 检查 `modelscope` 库是否已安装
2. 若已安装，优先通过 ModelScope 下载国内镜像
3. 否则使用 HF 镜像

**ModelScope 优先示例：**
```python
# 优先使用 ModelScope
try:
    from modelscope import snapshot_download
    model_path = snapshot_download('model_name')
except ImportError:
    # 回退到 HF 镜像
    import os
    os.environ['HF_ENDPOINT'] = 'https://hf-mirror.com'
    from huggingface_hub import snapshot_download
    model_path = snapshot_download('model_name')
```

**常用镜像源：**

| 镜像源 | 地址 | 用途 |
|--------|------|------|
| HF-Mirror | https://hf-mirror.com | HuggingFace 镜像 |
| ModelScope | https://modelscope.cn | 阿里云模型平台 |

---

### F. Docker 镜像加速

**配置文件：** `/etc/docker/daemon.json`

```json
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://docker.xuanyuan.me"
  ]
}
```

**重启 Docker：**
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

---

## 3. 执行准则

### 静默优先
- 上述配置应使用 `-y` 或 `--global` 参数
- 尽量不中断用户的对话流
- 配置成功后仅在回复中简要说明

### 持久化提示
在会话结束或环境配置完成后，询问用户：

> 是否需要将这些加速配置（如 `HF_ENDPOINT` 或 `npm registry`）永久写入你的 `.zshrc` 或 `.bashrc`？

### 报错拦截
如果原始命令运行中出现 `Connection refused` 或 `ETIMEDOUT`，自动触发：
1. 搜索最新代理站点
2. 提示用户：

> 检测到网络障碍，已为你自动寻找并切换至最新代理站点。

---

## 4. 触发场景示例

| 用户请求 | 自动操作 |
|----------|----------|
| "帮我建个 Vite 项目" | 设置 npm 镜像 → `npm create vite` |
| "克隆这个 GitHub repo" | 检测连通性 → 应用 GitHub 代理 |
| "下载 Llama-3 模型" | 设置 HF_ENDPOINT → 优先 ModelScope |
| "安装 Python 依赖" | 设置 pip 镜像 → `pip install` |
| "cargo build 这个项目" | 配置 crates.io 镜像 → `cargo build` |
| "docker pull 镜像" | 检查 Docker 镜像配置 |

---

## Your task

当用户执行涉及以下操作的命令时，自动执行加速配置：

1. **检测网络环境** - 判断是否需要加速
2. **应用对应加速** - 根据操作类型选择加速方案
3. **执行原始命令** - 使用加速后的环境执行
4. **报告配置状态** - 简要说明已应用的加速配置
5. **询问持久化** - 可选，是否永久保存配置

始终优先保证用户任务的顺利执行，加速配置应作为透明的辅助层。
