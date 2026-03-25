# Notion 笔记操作

## 真实来源

- **技能**：notion
- **API**：Notion API (2025-09-03)
- **配置**：`NOTION_API_KEY` 环境变量

---

## 干什么
让 OpenClaw 自动操作 Notion，包括创建笔记、更新内容、管理数据库、搜索笔记等。

## 怎么干

### 1. 准备工作

```bash
# 1. 创建 Notion Integration
# 访问 https://notion.so/my-integrations

# 2. 保存 API Key
mkdir -p ~/.config/notion
echo "ntn_your_key_here" > ~/.config/notion/api_key

# 3. 分享页面给 Integration
# 在 Notion 页面点击 "..." → "Connect to" → 你的 Integration
```

### 2. 执行步骤

**方式一：搜索页面和数据库**

```bash
# 搜索
curl -X POST "https://api.notion.com/v1/search" \
  -H "Authorization: Bearer $NOTION_KEY" \
  -H "Notion-Version: 2025-09-03" \
  -H "Content-Type: application/json" \
  -d '{"query": "项目文档"}'
```

**方式二：创建页面**

```bash
# 在数据库中创建页面
curl -X POST "https://api.notion.com/v1/pages" \
  -H "Authorization: Bearer $NOTION_KEY" \
  -H "Notion-Version: 2025-09-03" \
  -H "Content-Type: application/json" \
  -d '{
    "parent": {"database_id": "xxx"},
    "properties": {
      "Name": {"title": [{"text": {"content": "新任务"}}]},
      "Status": {"select": {"name": "Todo"}}
    }
  }'
```

**方式三：查询数据库**

```bash
# 查询数据源
curl -X POST "https://api.notion.com/v1/data_sources/{id}/query" \
  -H "Authorization: Bearer $NOTION_KEY" \
  -H "Notion-Version: 2025-09-03" \
  -H "Content-Type: application/json" \
  -d '{
    "filter": {"property": "Status", "select": {"equals": "Active"}},
    "sorts": [{"property": "Date", "direction": "descending"}]
  }'
```

**方式四：更新页面**

```bash
# 更新页面属性
curl -X PATCH "https://api.notion.com/v1/pages/{page_id}" \
  -H "Authorization: Bearer $NOTION_KEY" \
  -H "Notion-Version: 2025-09-03" \
  -H "Content-Type: application/json" \
  -d '{"properties": {"Status": {"select": {"name": "Done"}}}}'
```

### 3. 属性类型格式

| 类型 | 格式 |
|------|------|
| Title | `{"title": [{"text": {"content": "..."}}]}` |
| Rich text | `{"rich_text": [{"text": {"content": "..."}}]}` |
| Select | `{"select": {"name": "Option"}}` |
| Multi-select | `{"multi_select": [{"name": "A"}, {"name": "B"}]}` |
| Date | `{"date": {"start": "2024-01-15"}}` |
| Checkbox | `{"checkbox": true}` |
| Number | `{"number": 42}` |
| URL | `{"url": "https://..."}` |

### 4. 效果展示

```
Notion 操作完成！

搜索结果（5 个匹配）：
1. 项目文档 - 页面
2. 任务管理 - 数据库
3. 会议记录 - 页面
4. API 设计 - 页面
5. 周报模板 - 数据库

创建页面：
- ID: abc123-def456
- 标题：新任务
- 状态：Todo
- URL: https://notion.so/abc123def456

数据库查询（10 条记录）：
- 进行中：3 条
- 已完成：5 条
- 待处理：2 条
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Notion API Key | ntn_xxx | [创建 Integration](https://notion.so/my-integrations) |
| Notion 账号 | 工作空间 | [notion.so](https://notion.so) |

## API 说明

- **版本**：2025-09-03
- **速率限制**：约 3 请求/秒
- **Payload 限制**：最多 1000 blocks，500KB

## 相关资源

- [Notion API 文档](https://developers.notion.com)
- OpenClaw 技能：notion
