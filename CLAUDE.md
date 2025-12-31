# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个**单文件新年倒计时网页**，所有代码都集中在 `index.html` 中。项目零依赖、零配置，直接在浏览器中打开即可运行。

## 架构结构

```
index.html  (约 716 行)
├── <style>          # CSS 样式（约 300 行）
│   ├── 极光背景动画
│   ├── 粒子/烟花 Canvas 层级
│   ├── 发光边框效果
│   ├── 倒计时卡片样式
│   └── 响应式设计 (@media max-width: 768px)
│
└── <script>         # JavaScript 逻辑（约 350 行）
    ├── Canvas 初始化 (367-379)
    ├── 粒子系统 (381-506)
    │   ├── Particle 类
    │   ├── connectParticles() - 粒子连线
    │   └── animateParticles() - 动画循环
    │
    ├── 烟花系统 (522-645)
    │   ├── FireworkParticle 类
    │   ├── createFirework() - 创建烟花
    │   └── animateFireworks() - 动画循环
    │
    └── 倒计时逻辑 (647-714)
        ├── updateCountdown() - 更新时间显示
        └── enterCelebrationMode() - 跨年庆典模式
```

## 开发指南

### 运行项目

无需构建命令，直接在浏览器打开 `index.html` 即可：

```bash
# 用默认浏览器打开
open index.html

# 或启动简单的本地服务器（可选）
python3 -m http.server 8000
```

### 修改倒计时目标日期

编辑 `index.html` 第 648 行：

```javascript
const targetDate = new Date('2026-01-01T00:00:00');
```

### 修改文本内容

| 内容 | 位置 |
|------|------|
| 主标题 | 第 336 行 `<h1>` |
| 年份数字 | 第 337 行 `.year` |
| 祝福语 | 第 356-360 行 `.wishes` |
| 庆典模式标题 | 第 690 行 |
| 庆典模式祝福 | 第 691 行 |

### 移动端性能优化

项目已针对移动端进行多项优化，关键代码在：

- **设备检测**（第 453 行）：`isMobile` 变量控制是否为移动设备
- **粒子数量**（第 454 行）：移动端 20 个，桌面端 60 个
- **Canvas 发光**（第 444-447 行）：移动端禁用 shadowBlur
- **可见性检测**（第 509-520 行）：页面隐藏时暂停动画

修改任何动画相关代码时，务必考虑移动端性能影响。

### Canvas 分层

项目使用两个 Canvas 层：

| Canvas | z-index | 用途 |
|--------|---------|------|
| `#particle-canvas` | 1 | 粒子背景 + 连线 |
| `#firework-canvas` | 2 | 烟花爆炸效果 |

这种分层设计允许独立控制两个动画循环，提升性能。

## 常见修改场景

### 更换配色方案

1. **背景渐变**：修改第 37 行 `linear-gradient`
2. **极光颜色**：修改第 83-85 行 `radial-gradient` 颜色值
3. **边框发光**：修改第 111 行 `linear-gradient` 色值
4. **年份渐变**：修改第 140 行 `linear-gradient` 色值

### 调整动画速度

- **粒子移动速度**：修改 Particle 类 `speedX/speedY`（第 403-404 行）
- **极光动画**：修改 `auroraMove` 动画时长（第 86 行）
- **自动烟花频率**：修改 `autoFireworkInterval`（第 640 行）

### 添加新的烟花颜色

编辑 `createFirework()` 函数中的 `colors` 数组（第 586-596 行）。

## 部署

静态文件，可直接部署到任何静态托管服务：

- GitHub Pages
- Netlify
- Vercel
- Cloudflare Pages

部署前记得更新第 12、15、19-20 行的 Open Graph 元数据中的 URL。
