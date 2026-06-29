# easy-index

一个轻量级的企业内部导航页系统，基于纯前端技术栈（HTML/CSS/JavaScript），无需后端即可部署使用。

## 功能特性

- **多页面导航** — 首页、常用网址、API 接口、关于页面，各模块独立维护
- **登录鉴权** — 基于 localStorage 的用户认证，支持多账户、不同权限级别
- **角色权限** — 不同用户仅可见自己有权限访问的页面，菜单和按钮动态渲染
- **响应式布局** — 适配电脑与手机端，两列卡片布局自动切换为单列
- **零依赖** — 纯 HTML/CSS/JS，无需 npm、框架或构建工具，下载即用
- **配置简单** — 网址和 API 入口以 JS 数组形式配置，增删改查直观方便

## 项目结构

```
.
├── index.html      # 首页 - 导航入口，含 LOGO 与三个功能入口
├── login.html      # 登录页 - 用户名/密码认证，24 小时登录有效期
├── website.html    # 常用网址入口 - 卡片式展示外部链接
├── api.html        # API 接口入口 - 卡片式展示 API 文档/接口链接
├── about.html      # 关于页 - 导航页使用说明
└── README.md
```

## 快速开始

直接将项目文件部署到任意静态文件服务器即可：

```bash
# 方式一：Python 简易服务器
python -m http.server 8080

# 方式二：Node.js
npx serve .

# 方式三：直接打开 HTML 文件（部分浏览器可能存在跨域限制）
```

浏览器访问 `http://localhost:8080`，自动跳转到登录页。

## 测试账号

| 用户名 | 密码 | 权限范围 |
|--------|------|----------|
| admin | 123456 | 全部页面（首页 + 常用网址 + API 接口 + 关于） |
| test1 | 123456 | 首页 + 常用网址 |
| test2 | 123456 | 首页 + API 接口 |
| test3 | 123456 | 首页 + 关于 |

## 自定义配置

### 修改常用网址

编辑 `website.html` 中的 `websiteList` 数组：

```js
const websiteList = [
    { name: "百度", desc: "国内常用搜索引擎", url: "https://www.baidu.com" },
    { name: "GitHub", desc: "全球最大的代码托管平台", url: "https://github.com" },
    // 按格式新增条目...
];
```

### 修改 API 接口

编辑 `api.html` 中的 `apiList` 数组：

```js
const apiList = [
    { name: "高德地图API", desc: "提供地理编码、地图展示等服务", url: "https://lbs.amap.com/" },
    // 按格式新增条目...
];
```

### 修改用户权限

编辑 `login.html` 中的 `userList` 数组，修改 `allowPages` 即可控制用户可访问的页面。

## 技术说明

- 登录状态存储在 `localStorage` 的 `saikenLoginState` 键中
- 登录有效期为 24 小时，超时自动清除并跳转登录页
- 权限校验在 `checkAuth()` 函数中执行，每个页面加载时触发
- 下拉菜单和首页按钮根据当前用户权限动态渲染
