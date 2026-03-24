# 浏览器自动化

## 真实来源

- **工具**：OpenClaw 内置 `browser` 工具
- **底层**：Playwright
- **文档**：系统内置工具说明

---

## 干什么
通过 OpenClaw 控制浏览器进行自动化操作，如网页抓取、表单填写、截图、测试等。

## 怎么干

### 1. 准备工作
- OpenClaw 版本：>= 1.0.0
- 无需额外安装（browser 为内置工具）

### 2. 执行步骤

**方式一：网页抓取**

```
打开这个网页并提取内容：
https://example.com/article

提取：
- 标题
- 正文内容
- 作者信息
- 发布时间
```

**方式二：截图**

```
截取网页截图：
- URL：https://my-app.com/dashboard
- 全页面截图
- 保存到：~/Downloads/dashboard.png
```

**方式三：表单自动填写**

```
自动填写登录表单：
1. 打开 https://example.com/login
2. 填写用户名：myuser
3. 填写密码：[请提供]
4. 点击登录按钮
5. 截图登录后页面
```

**方式四：批量操作**

```
批量截图产品页面：
URL 列表：
- /products/1
- /products/2
- /products/3

每个页面：
1. 打开页面
2. 等待加载完成
3. 截图保存
```

### 3. 可用操作

browser 工具支持以下操作：

| Action | 说明 |
|--------|------|
| `status` | 查看浏览器状态 |
| `start` | 启动浏览器 |
| `stop` | 关闭浏览器 |
| `open` | 打开 URL |
| `navigate` | 导航到 URL |
| `snapshot` | 获取页面快照（DOM 树） |
| `screenshot` | 截图 |
| `act` | 执行交互（点击、输入等） |
| `pdf` | 生成 PDF |
| `console` | 执行 JavaScript |

### 4. 效果展示

```
浏览器自动化完成！

网页抓取：
- 标题：深入理解 React Hooks
- 作者：张三
- 发布：2024
- 内容：[已提取 2,345 字]

截图：
- 文件：~/Downloads/dashboard.png
- 尺寸：1920x1080
- 大小：234KB

表单填写：
- 登录成功
- 跳转到：/dashboard
- 已截图登录后页面
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| browser | 浏览器工具 | 内置 |

## 相关资源

- [Playwright 文档](https://playwright.dev)
- OpenClaw 系统工具说明：browser 工具
