# Trello 卡片管理

## 真实来源

- **技能**：trello
- **API**：Trello REST API
- **配置**：`TRELLO_API_KEY` + `TRELLO_TOKEN`

---

## 干什么
通过 OpenClaw 管理 Trello 看板、列表和卡片，实现任务管理自动化。

## 怎么干

### 1. 准备工作

```bash
# 1. 获取 API Key
# 访问 https://trello.com/app-key

# 2. 生成 Token（点击页面上的 Token 链接）

# 3. 设置环境变量
export TRELLO_API_KEY="your-api-key"
export TRELLO_TOKEN="your-token"
```

### 2. 执行步骤

**方式一：列出看板**

```bash
# 获取所有看板
curl -s "https://api.trello.com/1/members/me/boards?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" | jq '.[] | {name, id}'
```

**方式二：列出列表**

```bash
# 获取看板中的列表
curl -s "https://api.trello.com/1/boards/{boardId}/lists?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" | jq '.[] | {name, id}'
```

**方式三：列出卡片**

```bash
# 获取列表中的卡片
curl -s "https://api.trello.com/1/lists/{listId}/cards?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" | jq '.[] | {name, id, desc}'
```

**方式四：创建卡片**

```bash
curl -s -X POST "https://api.trello.com/1/cards?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" \
  -d "idList={listId}" \
  -d "name=新任务" \
  -d "desc=任务描述"
```

**方式五：移动卡片**

```bash
# 移动到另一个列表
curl -s -X PUT "https://api.trello.com/1/cards/{cardId}?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" \
  -d "idList={newListId}"
```

**方式六：添加评论**

```bash
curl -s -X POST "https://api.trello.com/1/cards/{cardId}/actions/comments?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" \
  -d "text=评论内容"
```

**方式七：归档卡片**

```bash
curl -s -X PUT "https://api.trello.com/1/cards/{cardId}?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" \
  -d "closed=true"
```

### 3. 常用查询模板

```bash
# 搜索看板
curl -s "https://api.trello.com/1/members/me/boards?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" | jq '.[] | select(.name | contains("Work"))'

# 获取看板所有卡片
curl -s "https://api.trello.com/1/boards/{boardId}/cards?key=$TRELLO_API_KEY&token=$TRELLO_TOKEN" | jq '.[] | {name, list: .idList}'
```

### 4. 效果展示

```
Trello 操作完成！

看板列表：
1. 产品开发 (id: abc123)
2. 运营活动 (id: def456)
3. 个人任务 (id: ghi789)

列表（产品开发看板）：
- 待办 (3 张卡片)
- 进行中 (2 张卡片)
- 已完成 (5 张卡片)

创建卡片：
- 名称：新功能设计
- 列表：待办
- 描述：设计用户仪表板功能
- URL: https://trello.com/c/xxx

移动卡片：
- 卡片：Bug 修复 #123
- 从：待办 → 进行中
- 状态：已移动
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Trello 账号 | 看板服务 | [trello.com](https://trello.com) |
| TRELLO_API_KEY | API 密钥 | [app-key](https://trello.com/app-key) |
| TRELLO_TOKEN | 访问令牌 | 点击 Token 链接 |

## API 限制

- 300 请求/10秒/API Key
- 100 请求/10秒/Token
- `/1/members` 端点：100 请求/900秒

## 相关资源

- [Trello REST API](https://developer.atlassian.com/cloud/trello/rest/)
- OpenClaw 技能：trello
