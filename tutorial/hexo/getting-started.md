# VitePress 技术文档

## 概述

VitePress 是一个基于 Vite 和 Vue 的静态站点生成器，专为技术文档而设计。它具有以下特点：

- ⚡ 极速的热重载
- 📝 基于 Markdown 的内容编写
- 🎨 使用 Vue 3 开发自定义主题
- 🔍 开箱即用的 SEO 优化

## 快速开始

### 安装

```bash
# 创建新项目
npm init vitepress@latest

# 或现有项目中安装
npm add -D vitepress
```

### 基本配置

在 `.vitepress/config.js` 中配置：

```js
export default {
  title: '我的文档',
  description: '使用 VitePress 创建的技术文档',
  themeConfig: {
    nav: [
      { text: '指南', link: '/guide/' }
    ],
    sidebar: {
      '/guide/': [
        {
          text: '指南',
          items: [
            { text: '介绍', link: '/guide/' },
            { text: '快速开始', link: '/guide/getting-started' }
          ]
        }
      ]
    }
  }
}
```

## 功能特性

### Markdown 扩展

VitePress 扩展了标准 Markdown 语法：

````markdown
```js{1,3-4}
// 代码高亮与行号聚焦
function hello() {
  console.log('Hello VitePress')
}
```
````

### 自定义组件

在 Markdown 中使用 Vue 组件：

```md
<CustomComponent :value="10" />

<script setup>
import CustomComponent from './CustomComponent.vue'
</script>
```

## 部署指南

### 构建静态文件

```bash
npm run docs:build
```

### 部署到 GitHub Pages

1. 在项目根目录创建 `.github/workflows/deploy.yml`
2. 使用官方提供的部署工作流
3. 推送代码到 GitHub 仓库

## 了解更多

- [官方文档](https://vitepress.dev/)
- [GitHub 仓库](https://github.com/vuejs/vitepress)
- [Vue.js](https://vuejs.org/)

---

*最后更新: {当前日期}*