---
name: github-proxy
description: 通过代理镜像访问 GitHub 内容。用于下载原始文件、Releases、归档包、Gist 以及 git clone。优先使用 gh-proxy.com（支持 API），失败后降级到 ghfast.top。
---

# GitHub 代理加速

当用户需要访问 GitHub 内容且直连被墙时，在 URL 前加上代理镜像前缀。支持 raw 文件、Releases、归档包、Gist、git clone 以及 API 请求。

## 镜像源（按优先级）

1. **主用：** `https://gh-proxy.com`（支持文件下载 + API 请求 + git clone）
2. **备用：** `https://ghfast.top`（支持文件下载 + git clone）

## 使用方法

将任何 GitHub 链接加上代理前缀：

```
原始文件:
原始: https://raw.githubusercontent.com/owner/repo/main/file.txt
代理: https://gh-proxy.com/https://raw.githubusercontent.com/owner/repo/main/file.txt

Release 下载:
原始: https://github.com/owner/repo/releases/download/v1.0/app.zip
代理: https://gh-proxy.com/https://github.com/owner/repo/releases/download/v1.0/app.zip

归档包 (tarball/zipball):
原始: https://github.com/owner/repo/archive/refs/heads/main.tar.gz
代理: https://gh-proxy.com/https://github.com/owner/repo/archive/refs/heads/main.tar.gz

Gist:
原始: https://gist.githubusercontent.com/owner/abc123/raw/file.txt
代理: https://gh-proxy.com/https://gist.githubusercontent.com/owner/abc123/raw/file.txt

API 请求（仅 gh-proxy.com 支持）:
原始: https://api.github.com/repos/owner/repo/contents/path
代理: https://gh-proxy.com/https://api.github.com/repos/owner/repo/contents/path

Git Clone:
原始: https://github.com/owner/repo.git
代理: https://gh-proxy.com/https://github.com/owner/repo.git
```

## 工作流程

1. 优先尝试 `gh-proxy.com`
2. 如果失败，降级到 `ghfast.top`
3. 如果都失败了，告知用户两个镜像源都不可用

## 局限性

- `ghfast.top` 不支持 API 请求（返回 403），但支持文件下载和 git clone
- `gh-proxy.com` 支持 API 请求、文件下载和 git clone
- 不支持 GitHub 网页本身（如仓库主页、文件树的 HTML 页面）
- 如需查看仓库目录结构，可通过 API 代理获取（`/repos/owner/repo/contents/path`）
