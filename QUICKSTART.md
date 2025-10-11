# OpenFDA MCP Server - 快速开始指南

## 🚀 使用 npx 快速启动（推荐）

### 配置方法

在 Cursor / Cherry Studio 的 MCP 配置文件中添加：

```json
{
  "mcpServers": {
    "openfda": {
      "command": "npx",
      "args": ["-y", "mcp-openfda"]
    }
  }
}
```

### 说明

- 无需手动安装依赖
- `npx` 会自动从 npm 下载并运行最新版本
- `-y` 参数跳过确认提示，实现无人值守启动

---

## 📦 从 npm 安装

如果你想全局安装：

```bash
npm install -g mcp-openfda
```

安装后可直接使用：

```bash
mcp-openfda
```

---

## 💊 可用工具（5 个）

### 1. search_drug_labels

搜索 FDA 药物标签，支持复杂查询语法。

**参数**:

- `search` (string): 搜索查询，如 "aspirin", "openfda.brand_name:tylenol"
- `count` (string): 按字段统计结果
- `skip` (number): 跳过记录数（分页）
- `limit` (number): 返回记录数限制 (1-1000)

### 2. get_drug_adverse_reactions

获取特定药物的不良反应信息。

**参数**:

- `drug_name` (string, 必需): 药物名称
- `limit` (number): 返回记录数限制 (1-100)

### 3. get_drug_warnings

获取药物的警告和注意事项。

**参数**:

- `drug_name` (string, 必需): 药物名称
- `limit` (number): 返回记录数限制 (1-100)

### 4. get_drug_indications

获取药物的适应症和用法信息。

**参数**:

- `drug_name` (string, 必需): 药物名称
- `limit` (number): 返回记录数限制 (1-100)

### 5. ae_pipeline_rag

高级 RAG 管道，用于药物安全分析。

**参数**:

- `query` (string): 自然语言查询
- `drug` (string): 药物名称
- `condition` (string): 医疗条件
- `top_k` (number): 返回的文本块数量 (1-10)

---

## 💡 使用示例

```javascript
// 搜索阿司匹林的信息
{
  "tool": "search_drug_labels",
  "arguments": {
    "search": "aspirin",
    "limit": 5
  }
}

// 获取布洛芬的不良反应
{
  "tool": "get_drug_adverse_reactions",
  "arguments": {
    "drug_name": "ibuprofen",
    "limit": 3
  }
}

// 查询泰诺的警告信息
{
  "tool": "get_drug_warnings",
  "arguments": {
    "drug_name": "tylenol",
    "limit": 2
  }
}

// 使用 RAG 管道进行深度分析
{
  "tool": "ae_pipeline_rag",
  "arguments": {
    "query": "cardiovascular side effects and warnings",
    "drug": "aspirin",
    "top_k": 5
  }
}
```

---

## 📝 版本信息

- **当前版本**: 0.1.1
- **npm 地址**: https://www.npmjs.com/package/mcp-openfda
- **源码地址**: https://github.com/Aki894/mcp-openfda

---

## ⚠️ 注意事项

1. **API 限制**: OpenFDA API 有速率限制，建议合理控制请求频率
2. **数据准确性**: 返回的数据仅供参考，不应作为医疗建议
3. **许可证**: GPL-3.0
4. **Node.js 版本**: 需要 Node.js 18.0.0 或更高版本

---

## 🔧 高级配置

### 手动安装配置

```json
{
  "mcpServers": {
    "openfda": {
      "command": "node",
      "args": ["/path/to/mcp-openfda/dist/index.js"]
    }
  }
}
```

### HTTP 模式启动

```bash
npm run start:http
# 或
node dist/http.js
```
