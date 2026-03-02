---
layout: ../../layouts/PostLayout.astro
title: '我用 devcontainer 解決了「在我電腦上可以跑」的問題'
description: '開發環境一致性一直是個頭痛問題，devcontainer 讓我徹底解脫。'
pubDate: '2024-11-20'
section: tech
emoji: '💻'
tags: ['devcontainer', 'Docker', '開發工具']
minutesRead: 5
---

如果你曾經花超過一小時 debug 一個「在我機器上明明可以跑」的問題，這篇文章可能會讓你感同身受。

## 問題的起點

我有兩台工作機：一台 MacBook、一台 Windows PC。加上偶爾連的 Linux 伺服器。

每次換環境，就是一場小型災難。Node.js 版本不對、環境變數沒設、某個依賴裝不上去……

## devcontainer 是什麼

簡單說：把你的開發環境打包進一個 Docker 容器，然後用 VS Code 直接在裡面開發。

```json
// .devcontainer/devcontainer.json
{
  "name": "My Project",
  "build": { "dockerfile": "../Dockerfile" },
  "forwardPorts": [3000],
  "postCreateCommand": "npm install"
}
```

設定好之後，任何人（包括未來的你）只要：
1. 安裝 Docker
2. 安裝 VS Code + Dev Containers 擴充功能
3. 打開專案，點「在容器中重新開啟」

就能得到一模一樣的開發環境。

## 我實際用下來的感受

**好的地方：**
- 真的解決了環境不一致的問題
- 可以安心嘗試新工具，不怕搞壞本機
- 適合交接專案給新成員

**需要適應的地方：**
- 第一次建立容器需要等待（之後有快取就快了）
- 記憶體用量比直接跑本機多一點
- 需要對 Docker 有基本認識

## 這個部落格就是用 devcontainer 開發的

Astro + Node.js 20，在任何有 Docker 的機器上 clone 下來就能跑。這種感覺還不錯。
