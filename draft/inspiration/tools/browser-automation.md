# 浏览器自动化

## 干什么
通过 OpenClaw 控制浏览器进行自动化操作，如网页抓取、表单填写、截图、测试等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：browser
- 需要的配置：无（使用内置浏览器）

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

**方式五：网页监控**

```
监控网页变化：
- URL：https://example.com/price
- 监控元素：.price-value
- 变化时通知我
```

**OpenClaw 会自动：**
1. 启动或连接浏览器
2. 执行导航和交互
3. 提取页面内容
4. 生成截图或报告

### 3. 效果展示

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

批量操作：
- 处理页面：3 个
- 截图保存：3 张
- 耗时：12.3 秒

监控设置：
- 监控元素：.price-value
- 当前值：¥999
- 变化时将通知
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| browser | 浏览器技能 | 内置 |

## 来源

- 贡献者：Community
- 来源：自动化测试实践
- 日期：2024

## 相关资源

- [Browser 技能文档](https://openclaw.ai/skills/browser)
- [Playwright 文档](https://playwright.dev)
