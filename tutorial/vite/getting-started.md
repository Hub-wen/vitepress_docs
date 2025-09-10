# VitePress 技术文档

## 概述

VitePress 是一个基于 Vite 和 Vue 的静态站点生成器，专为技术文档而设计。它具有以下特点：

- ⚡ 极速的热重载
- 📝 基于 Markdown 的内容编写
- 🎨 使用 Vue 3 开发自定义主题
- 🔍 开箱即用的 SEO 优化

## 准备工作

::: tip 提示
已经安装 或者 熟练了，可以不用看此步骤
:::

::: details 必备工具
- 必装：[nodejs](https://yiov.top/website/nodejs)
- 可选安装：[git](https://yiov.top/website/pages/git)
- 建议安装：[vscode](https://yiov.top/website/VSCode)
:::

::: details npm、pnpm、yarn、bun
::: code-group

```sh [npm]
#查询npm版本
npm -v
```

```sh [pnpm]
#安装pnpm
npm install -g pnpm
#查询pnpm版本
pnpm -v
```

```sh [yarn]
#安装yarn
npm install -g yarn
#查询yarn版本
yarn -v
```
```sh [bun]
#安装yarn
npm install -g bun
#查询bun版本
bun -v
```
:::

::: details 创建目录
::: code-group

```sh [新建目录]
#盘符可以自定义 回车进入
#创建目录并进入文件夹
mkdir vitepress && cd vitepress
```
:::


## 快速开始

### 安装

::: details 安装vitepress
::: code-group

```sh [npm]
# 创建新项目
npm init vitepress@latest
# 或现有项目中安装
npm add -D vitepress
```
```sh [pnpm]
pnpm add -D vitepress
```
```sh [yarn]
yarn add -D vitepress
```
```sh [bun]
bun add -D vitepress
```
:::

### 初始化

::: details 初始化vitepress
::: code-group

```sh [npm]
# 创建新项目
npm init vitepress@latest

# 或现有项目中安装
npm vitepress init

```
```sh [pnpm]
pnpm vitepress init
```
```sh [yarn]
yarn vitepress init
```
```sh [bun]
bun vitepress init
```
:::

```sh [向导]
T   Welcome to VitePress!
|
o  Where should VitePress initialize the config?
|  ./docs             #新手默认；老手直接./
|
o  Site title:
|  My Awesome Project #标题（不需要动）
|
o  Site description:  #副标题（不需要动）
|  A VitePress Site
|
o  Theme:             #主题选择
|  Default Theme      #默认（不可以自定义）
|
o  Use TypeScript for config and theme files?
|  Yes                #是否使用TS
|
o  Add VitePress npm scripts to package.json?
|  Yes                #是否使用命令
|
—  Done! Now run npm run docs:dev and start writing.
```

### 基本配置

在 `.vitepress/config.mjs` 中配置：

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
::: details 我的配置
::: code-group
```js
import { defineConfig } from 'vitepress'
// import {set_sidebar} from "./gen_sidebar.mjs";
// import { set_sidebar } from "./auto_gen_sidebar.mjs";	// 改成自己的路径
// https://vitepress.dev/reference/site-config
//自定义配置
export default defineConfig({
  base: "/vitepress_docs/", // 这是部署到github相关的配置
  title: "学习笔记文档库", //站点名
  description: "Aldebaran的学习笔记文档库", //站点描述
  lang: 'zh-CN', //语言，可选 en-US
  cleanUrls:true, //开启纯净链接
  //fav图标及谷歌字体
  head: [
    ['link',
      { rel: 'icon', href: '/vitepress_docs/logo.png' }
    ],
    [
      'link',
      { rel: 'preconnect', href: 'https://fonts.googleapis.com' }
    ],
    [
      'link',
      { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' }
    ],
    [
      'link',
      { href: 'https://fonts.googleapis.com/css2?family=Roboto&display=swap', rel: 'stylesheet' }
    ],
    [
      'link',
      { href: 'https://raw.githubusercontent.com/LhamoJam/SmileySans-woff-/main/SmileySans-Oblique.ttf.woff2', rel: 'stylesheet' }
    ],
  ],
  //appearance:true, //默认浅色且开启切换
  //启用深色模式
  appearance:'dark', 
  // appearance:false, // 关闭
  // appearance: "force-dark", // 强制深色主题
  // 站点地图
  // sitemap: {
  //   hostname: 'https://aldebaran.cc',
  // },
  //markdown配置
  markdown: {
    image: {
      // 开启图片懒加载
      lazyLoading: true
    },
    // toc显示1-6级标题
    toc: {level: [1,2,3,4,5,6]},
  },
  lastUpdated: true, //显示最后更新时间

  //主题配置
  themeConfig: {
    // https://vitepress.dev/reference/default-theme-config
    logo: '/docs.png', //左上角logo
    //siteTitle: false, //标题隐藏
    darkModeSwitchLabel: '深浅模式', //手机端深浅模式文字修改
    //本地搜索
    // 设置搜索框的样式
    search: {
      provider: "local",
      options: {
        translations: {
          button: {
            buttonText: "搜索文档",
            buttonAriaLabel: "搜索文档",
          },
          modal: {
            noResultsText: "无法找到相关结果",
            resetButtonTitle: "清除查询条件",
            footer: {
              selectText: "选择",
              navigateText: "切换",
            },
          },
        },
      },
    },
    //侧边栏文字更改(移动端)
    sidebarMenuLabel:'目录', 
    //返回顶部文字修改
    returnToTopLabel:'返回顶部', 
    outline: { 
      level: [2,4], // 显示2-4级标题
      // level: 'deep', // 显示2-6级标题
      label: '当前页大纲' // 文字显示
    },
    // outline:false, // 关闭标题显示
    // outlineTitle:'当前页大纲', //老方式设置标题
    //上次更新时间
    lastUpdated: {
      text: '最后更新于',
      formatOptions: {
        dateStyle: 'short', // 可选值full、long、medium、short
        timeStyle: 'medium' // 可选值full、long、medium、short
      },
    },
    //自定义上下页名
    docFooter: { 
      prev: '上一页', 
      next: '下一页', 
    }, 
    //广告
    carbonAds: { 
      code: './public/qrcode.jpg' , //'your-carbon-code', 
      placement: 'https://cdn.jsdelivr.net/gh/Hub-wen/blogimage@main/img/202509062346138.jpg' //s'your-carbon-placement', 
    },

    //导航栏
    nav: [
      // { text: 'Examples', link: '/markdown-examples' },
      {
        text: '笔记',
        items: [
          {
            // 分组标题1
            text: '介绍',
            items: [
              { text: '前言', link: '/notes/index/' },
            ],
          },
          {
            // 分组标题1
            text: '真题',
            items: [
              { text: '真题介绍', link: '/notes/真题/index' },
              { text: '2025', link: '/notes/真题/2025/' },
              { text: '2024', link: '/notes/真题/2024/' },
              { text: '2023', link: '/notes/真题/2023/' },
              { text: '2022', link: '/notes/真题/2022/' },
              { text: '2021', link: '/notes/真题/2021/' },
              { text: '2020', link: '/notes/真题/2020/' },
              { text: '2019', link: '/notes/真题/2019/' },
              { text: '2018', link: '/notes/真题/2018/' },
              { text: '2017', link: '/notes/真题/2017/' },
              { text: '2016', link: '/notes/真题/2016/' },              
            ],
          },
        ]
      },
      {
        text: '指南',
        items: [
          {
            // 分组标题1
            text: '介绍',
            items: [
              { text: '前言', link: '/tutorial/index' },
            ],
          },
          {
            // 分组标题2
            text: 'hexo',
            items: [
              { text: '快速上手', link: '/tutorial/hexo/getting-started' },
              { text: '配置', link: '/tutorial/hexo/configuration' },
              { text: '页面', link: '/tutorial/hexo/page' },
              { text: 'Frontmatter', link: '/tutorial/hexo/frontmatter' },
            ],
          },
          {
            // 分组标题3
            text: 'vitepress',
            items: [
              { text: '快速上手', link: '/tutorial/vite/getting-started' },
              { text: '配置', link: '/tutorial/vite/configuration' },
              { text: '页面', link: '/tutorial/vite/page' },
              { text: 'Frontmatter', link: '/tutorial/vite/frontmatter' },
            ],
          },
          {
            // 分组标题4
            text: 'harmonyOS',
            items: [
              { text: '快速上手', link: '/tutorial/harmony/getting-started' },
              { text: '配置', link: '/tutorial/harmony/configuration' },
              { text: '页面', link: '/tutorial/harmony/page' },
              { text: 'Frontmatter', link: '/tutorial/harmony/frontmatter' },
            ],
          },
          {
            // 分组标题5
            text: '工具',
            items: [
              { text: 'VPN', link: '/tutorial/工具/vpn/index' },
              { text: 'IDM', link: '/tutorial/工具/idm/index' },
              { text: 'JDK', link: '/tutorial/工具/jdk/index' },
              { text: 'Windhawk', link: '/tutorial/工具/windhawk/index' },
            ],
          },
        ],
      },
      {
        text: '学习',
        items: [
          {
            // 分组标题1
            text: '介绍',
            items: [
              { text: '前言', link: '/study/index' },
            ],
          },
          { text: '数学', 
            items: [
              {text: '高数', link: '/study/math/Advanced_Mathematics/基础知识'}, 
              {text: '概率论', link: '/study/math/Probability_theory/概率论基础公式'},
              {text: '线代', link: '/study/math/Linear_Algebra/线性方程组'},
            ]
           },
          { text: '408', 
            items: [
              {text: '数据结构', link: '/study/408/Data_Structure/绪论'}, 
              // {text: '组成原理', link: '/study/408/Principles_of_Composition/one'},
              // {text: '操作系统', link: '/study/408/operating_system/one'},
              // {text: '计算机网络', link: '/study/408/Computer_Networks/one'},
            ],
          },
          { text: '思政', 
            items: [
              {text: '马原', link: '/study/Political/马原/导论/马克思主义是关于无产阶级和人类解放的科学'}, 
              {text: '毛中特', link: '/study/Political/毛中特/导论'},
              {text: '新思想', link: '/study/Political/新思想/导论'},
              {text: '史纲', link: '/study/Political/史纲/旧民主主义'},
              {text: '思修', link: '/study/Political/思修/导论'},
            ],
          },
          { text: '英语', link: '/study/English/index' },
          { text: '日语', link: '/study/Japanese/index' },
        ]
      },
      { text: '关于', link: '/about' },
    ],

    //侧边栏
    // sidebar: [
    //   {
    //     text: 'Examples',
    //     items: [
    //       { text: 'Markdown Examples', link: '/markdown-examples' },
    //       { text: 'Runtime API Examples', link: '/api-examples' }
    //     ]
    //   }
    // ],
    // sidebar: {"/nuxt3": set_sidebar("nuxt3")},
    // sidebar: { "/docs/front-end/react": set_sidebar("docs/front-end/react") },
    sidebar: false, // 关闭侧边栏
    aside: "left", // 设置右侧侧边栏在左侧显示

    //自定义社交链接 
    socialLinks: [
      {icon: 'github', link: 'https://github.com/Hub-wen'},
      {
        icon: {
          svg: '<svg t="1756719994230" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="12287" data-spm-anchor-id="a313x.search_index.0.i7.57293a81DOVLSa" width="200" height="200"><path d="M221.4 152.6h141.8V396h-141.8V152.6z" fill="#FAD996" p-id="12288"></path><path d="M363.4 152.6c-9-16.6-138.2-14.2-142 0-3 11.4-23.6 287 15.8 182.4 10.4-27.4 22.6-47.6 37.2-78.6 10.6-22.6 22-42.4 32.6-54.4 16.6-18.6 18 9.6 33.6 22.6 41.6 34.4 31.8-55.6 22.8-72z" fill="#F9F8F7" p-id="12289"></path><path d="M834.2 851c0 24.8-20.2 45-45 45H234.8c-24.8 0-45-20.2-45-45v-370h1.2l321.2-270 321.2 270h0.6l0.2 370z" fill="#FAD996" p-id="12290"></path><path d="M833.4 481l-321.2-270-1.8 1.6V896h278.8c24.8 0 45-20.2 45-45l-0.2-370h-0.6z" fill="#F7C872" p-id="12291"></path><path d="M62 548L432.6 166.2s81.2-90.6 171.8 0c79 79 343.6 400 343.6 400s-55.4 41-125.2 14.2c-37.8-14.4-118.2-68-133.4-150.8-11-60.2-45.8 29-60.8-38.2-9.4-42.2-67.2-96.6-67.2-96.6s-48.4-55.4-100.2 0c-13.8 14.8-11.4 134.6-44 128-26.4-5.2-20-105.6-27-81.2-9.6 33-25 61-54.4 47.2-33.2-15.6-42.4 79.6-64.8 112.8-17.2 25.4-23.8-45.8-40.4-29.2-21.2 21-2.4 94-39.4 108s-132.8-2-129.2-32.4z" fill="#e6e6e6" p-id="12292" data-spm-anchor-id="a313x.search_index.0.i6.57293a81DOVLSa" class=""></path><path d="M512 126.2v144c28.8 1 49.4 24.6 49.4 24.6s57.8 54.4 67.2 96.6c15 67.2 49.8-22 60.8 38.2 15.2 82.8 95.6 136.4 133.4 150.8 69.8 26.8 125.2-14.2 125.2-14.2s-264.6-321-343.6-400c-33.2-33.2-65.2-42-92.4-40z" fill="#dbdbdb" p-id="12293" data-spm-anchor-id="a313x.search_index.0.i5.57293a81DOVLSa" class=""></path><path d="M405.2 495h99.8v99.8h-99.8v-99.8zM405.2 609.2h99.8v99.8h-99.8v-99.8z" fill="#FB8A5D" p-id="12294"></path><path d="M519 495h99.8v99.8h-99.8v-99.8zM519 609.2h99.8v99.8h-99.8v-99.8z" fill="#EA6D4B" p-id="12295"></path></svg>'
        },
        link: 'https://aldebaran.cc/',
        // You can include a custom label for accessibility too (optional but recommended):
        ariaLabel: '主页'
      },
      {
        icon: {
          svg: '<svg t="1756720419332" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="15578" width="200" height="200"><path d="M511.228735 511.267568m-511.228735 0a511.228735 511.228735 0 1 0 1022.457471 0 511.228735 511.228735 0 1 0-1022.457471 0Z" fill="#ED7826" p-id="15579"></path><path d="M874.256 151.19592c199.648599 199.657229 199.663701 523.355389 0 723.027719-199.648599 199.648599-523.37912 199.657229-723.034192 0L874.256 151.19592z" fill="#DB6D27" p-id="15580"></path><path d="M1004.426058 646.022067L637.660048 279.273316l-74.718826 74.727455-205.05716-28.818331 42.26746 191.599401-147.362248 147.362249 51.800939 51.800939-12.778183 12.778183 288.938394 288.947024c204.474667-27.802203 370.429248-176.424364 423.675634-371.648169z" fill="#CE6028" p-id="15581"></path><path d="M617.270615 781.960969c95.708012 0 173.453647-77.963531 173.99515-173.147298l1.074377-140.145801-1.607251-7.628508-4.59307-9.589571-7.781683-6.021257c-10.098713-7.911126-61.278326 0.532874-75.057535-11.971322-9.768633-8.927254-11.293903-25.064483-14.264621-46.925253-5.497014-42.347284-8.953142-44.56076-15.595726-58.905203-24.095818-50.985448-89.47533-89.298425-134.389901-94.586172h-121.667809c-95.723113 0-173.977891 78.084344-173.977891 173.445017V608.813671c0 95.18161 78.246148 173.147298 173.977891 173.147298h199.888069z m-197.672436-407.232056h96.450151c18.421899 0 33.340207 14.950669 33.340208 33.122312 0 18.098292-14.918308 33.178403-33.340208 33.178403h-96.450151c-18.41327 0-33.307846-15.080112-33.307847-33.178403 0.002157-18.171643 14.894577-33.122311 33.307847-33.122312z m-33.305689 231.510999c0-18.163013 14.894577-32.992868 33.307846-32.992868h195.991834c18.301086 0 33.154672 14.829855 33.154672 32.992868 0 17.936488-14.862216 32.999341-33.154672 32.999341h-195.991834c-18.415427 0-33.307846-15.062853-33.307846-32.999341z" fill="#FFFFFF" p-id="15582"></path></svg>'
        },
        link: 'https://blog.aldebaran.cc/',
        // You can include a custom label for accessibility too (optional but recommended):
        ariaLabel: '博客'
      },
      {
        icon: {
          //svg: '<svg t="1756720448216" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="16599" width="200" height="200"><path d="M787 956H237c-93.34 0-169-75.66-169-169V237c0-93.34 75.66-169 169-169h550c93.34 0 169 75.66 169 169v550c0 93.34-75.66 169-169 169z" fill="#1E1E1E" p-id="16600"></path><path d="M779.21 427.25c-4.53-53.01-47.34-94.63-100.45-97.67l-86.16-4.94c-53.69-3.08-107.51-3.08-161.2 0l-86.16 4.94c-53.12 3.04-95.92 44.66-100.45 97.67-6.82 79.83-6.82 160.11 0 239.94 4.53 53.01 47.34 94.63 100.45 97.67l86.16 4.94c53.69 3.08 107.51 3.08 161.2 0l86.16-4.94c53.12-3.04 95.92-44.66 100.45-97.67 6.83-79.84 6.83-160.11 0-239.94zM730.4 638.03l-2.94 32.91c-2.15 24.07-21.65 42.9-45.78 44.22l-106.21 5.82c-42.28 2.32-84.65 2.32-126.93 0l-106.21-5.82c-24.13-1.32-43.62-20.16-45.78-44.22l-2.94-32.91a1018.34 1018.34 0 0 1 0-181.63l2.94-32.91c2.15-24.07 21.65-42.9 45.78-44.22l106.21-5.82c42.28-2.32 84.65-2.32 126.93 0l106.21 5.82c24.13 1.32 43.62 20.16 45.78 44.22l2.94 32.91a1018.34 1018.34 0 0 1 0 181.63z" fill="#FFBE68" p-id="16601"></path><path d="M457.3 358.7l-0.54 0.35c-13.03 8.46-30.45 4.76-38.91-8.27l-35.78-55.09c-8.46-13.03-4.76-30.45 8.27-38.91l0.54-0.35c13.03-8.46 30.45-4.76 38.91 8.27l35.78 55.09c8.46 13.03 4.76 30.45-8.27 38.91zM566.7 358.7l0.54 0.35c13.03 8.46 30.45 4.76 38.91-8.27l35.78-55.09c8.46-13.03 4.76-30.45-8.27-38.91l-0.54-0.35c-13.03-8.46-30.45-4.76-38.91 8.27l-35.78 55.09c-8.46 13.03-4.76 30.45 8.27 38.91zM462.58 478.24l0.17 0.46c4.06 11.15-1.69 23.48-12.84 27.54l-95.03 34.59c-11.15 4.06-23.48-1.69-27.54-12.84l-0.17-0.46c-4.06-11.15 1.69-23.48 12.84-27.54l95.03-34.59c11.15-4.06 23.48 1.69 27.54 12.84zM561.42 478.24l-0.17 0.46c-4.06 11.15 1.69 23.48 12.84 27.54l95.03 34.59c11.15 4.06 23.48-1.69 27.54-12.84l0.17-0.46c4.06-11.15-1.69-23.48-12.84-27.54l-95.03-34.59c-11.15-4.06-23.48 1.69-27.54 12.84z" fill="#FFBE68" p-id="16602"></path><path d="M551.84 622.3c-13.4 0-29.67-7.04-40.78-25.57-11.11 18.53-27.38 25.57-40.78 25.57-20.9 0-38.12-20.24-42.83-50.37-0.7-4.47 2.36-8.66 6.83-9.36 4.47-0.7 8.66 2.36 9.36 6.83 3.31 21.16 14.52 36.52 26.65 36.52 11.22 0 25.77-8.4 32.95-31.96a8.185 8.185 0 1 1 15.66 0c7.18 23.57 21.72 31.96 32.95 31.96 12.13 0 23.34-15.36 26.65-36.52 0.7-4.47 4.89-7.53 9.36-6.83 4.47 0.7 7.52 4.89 6.83 9.36-4.73 30.13-21.94 50.37-42.85 50.37z" fill="#FFBE68" p-id="16603"></path></svg>'
          svg: '<svg t="1756733061454" class="icon" viewBox="0 0 1074 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="9131" width="200" height="200"><path d="M903.643237 150.431534H718.623684l83.319882-83.319881c0.109812-0.109812 0.233351-0.205898 0.329436-0.31571a39.120538 39.120538 0 0 0-55.317813-55.317813l-0.315709 0.329437-138.637695 138.637694h-129.537022l-138.637694-138.637694-0.315709-0.329437A39.120538 39.120538 0 0 0 284.138641 66.782217l0.329436 0.315709 83.319882 83.319882H170.387099A170.373372 170.373372 0 0 0 0 320.818633l1.37265 471.052451A170.400825 170.400825 0 0 0 171.759749 962.23073h44.954302a61.76927 61.76927 0 0 0 123.428728 0h409.118463a61.76927 61.76927 0 0 0 123.538539 0h30.884635a170.400825 170.400825 0 0 0 170.34592-170.359646V320.818633a170.387099 170.387099 0 0 0-170.387099-170.387099z m45.421003 629.634757a70.16989 70.16989 0 0 1-70.169891 70.183616H201.8757a70.183617 70.183617 0 0 1-70.183617-70.183616V330.180109a70.16989 70.16989 0 0 1 70.183617-70.16989h677.018649a70.156164 70.156164 0 0 1 70.169891 70.16989z" fill="#1296db" p-id="9132"></path><path d="M650.416684 502.049671l226.487322 38.434212 16.814968-91.267528-228.903187-45.475909-14.399103 98.309225zM420.195752 404.193421l-228.916913 45.475909 16.828694 91.267528 226.487322-38.434213-14.399103-98.309224zM608.537119 685.12006c-16.787515 2.662942-54.755026-30.102224-64.583203-50.719434a1.907984 1.907984 0 0 0-1.743266-1.125573h-0.219624a1.949164 1.949164 0 0 0-1.756993 1.125573c-9.828177 20.589757-47.781962 53.368649-64.583203 50.719434C456.859246 682.210041 441.073765 649.26643 441.073765 649.26643l-43.458112 28.139334s10.981204 20.081876 19.930884 32.490636c12.889188 17.954268 38.832281 30.761096 69.373753 30.074771 22.26439-0.494154 43.924814-17.693464 51.899913-24.844973a3.912054 3.912054 0 0 1 2.621763-0.988308h1.37265a3.870874 3.870874 0 0 1 2.55313 0.974582c8.235903 7.261321 29.800241 24.364545 51.886186 24.858699 30.541472 0.686325 56.470839-12.13423 69.373754-30.088497 8.908501-12.353854 19.930884-32.490636 19.930884-32.490636L643.114184 649.26643s-15.812933 32.943611-34.577065 35.85363z" fill="#1296db" p-id="9133"></path></svg>'
        },
        link: 'https://space.bilibili.com/694124492',
        // You can include a custom label for accessibility too (optional but recommended):
        ariaLabel: '哔哩哔哩'
      },
    ], 

    //页脚信息
    footer: {
      // message: 'Released under the MIT License.',
      // copyright: 'Copyright © 2023-2024 备案号：<a href="https://beian.miit.gov.cn/" target="_blank">京****号</a>', 
      // 自动更新时间
      // copyright: `Copyright © 2025-${new Date().getFullYear()} Aledbaran. 备案号：<a href="https://beian.miit.gov.cn/" target="_blank">晋****号</a>`, 
      copyright: `Copyright © 2025-${new Date().getFullYear()} Aldebaran.`, 
    },
  }
})

```
:::


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
- [VitePress
快速上手中文教程](https://vitepress.yiov.top/)
- [教程](https://docs.bugdesigner.cn/docs/Tutorial/vitepress.html)

---

*最后更新: {9.10}*