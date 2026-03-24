# 飞书文档操作

## 干什么
通过 OpenClaw 直接操作飞书文档、多维表格、知识库，实现文档自动化管理。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：feishu-doc、feishu-drive、feishu-wiki、feishu-bitable-*
- 需要的配置：飞书应用配置（App ID、App Secret）

### 2. 执行步骤

**方式一：读取飞书文档**

```
读取这个飞书文档：
https://open.feishu.cn/open-apis/documentx/docx/xxx

提取：
- 文档标题
- 主要内容
- 表格数据
```

**方式二：创建和编辑文档**

```
创建一个飞书文档：
- 标题：Q2 产品规划
- 内容：[提供内容或大纲]
- 保存到知识库：产品文档
```

**方式三：操作多维表格**

```
在这个多维表格中添加记录：
https://open.feishu.cn/base/xxx?table=yyy

字段值：
- 需求名称：搜索优化
- 优先级：P0
- 负责人：张三
- 状态：进行中
```

**方式四：管理知识库**

```
整理飞书知识库：
1. 列出所有知识库
2. 获取指定知识库的目录结构
3. 移动文档到新位置
```

**OpenClaw 会自动：**
1. 调用飞书开放平台 API
2. 处理权限和认证
3. 执行文档操作
4. 返回操作结果

### 3. 效果展示

```
飞书文档操作完成！

文档读取：
- 标题：《Q2 产品规划》
- 创建者：张三
- 最后更新：2024

创建新文档：
- 文档 Token：doccnxxx
- 访问链接：https://xxx.feishu.cn/docx/doccnxxx
- 已添加到知识库「产品文档」

多维表格记录：
- 新增记录 ID：recXXXXX
- 记录链接：[查看记录]

知识库整理：
- 移动 3 篇文档到「归档」
- 创建新目录「Q2 规划」
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 飞书企业账号 | 企业协作平台 | 企业注册 |
| 飞书应用 | 开放平台应用 | 飞书开放平台创建 |
| feishu-doc | 文档技能 | 技能安装 |
| feishu-drive | 云盘技能 | 技能安装 |
| feishu-wiki | 知识库技能 | 技能安装 |
| feishu-bitable-* | 多维表格技能 | 技能安装 |

## 来源

- 贡献者：Community
- 来源：企业协作实践
- 日期：2024

## 相关资源

- [飞书开放平台](https://open.feishu.cn)
- [Feishu Doc 技能文档](https://openclaw.ai/skills/feishu-doc)
- [Feishu Wiki 技能文档](https://openclaw.ai/skills/feishu-wiki)
