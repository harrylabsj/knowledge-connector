---
title: Knowledge Connector
version: 1.0.1
description: 知识连接器 - 从文档和对话中提取概念，构建知识图谱，支持智能查询和推荐
triggers:
  - 知识提取
  - 概念关联
  - 知识图谱
  - 知识查询
  - 知识推荐
  - knowledge extract
  - knowledge connect
  - knowledge query
---

# Knowledge Connector Skill

知识连接器是一个智能知识管理工具，能够从文档和对话中自动提取概念、建立概念间关系、构建知识图谱，并提供智能查询和推荐功能。

## 功能特性

- **知识提取 (extract)**: 从文本、文档中提取关键概念和实体
- **关系建立 (connect)**: 自动识别概念间的关联关系
- **知识图谱构建**: 将概念和关系组织成可视化图谱
- **智能查询 (query)**: 支持自然语言查询知识库
- **知识推荐 (recommend)**: 基于关联性推荐相关知识

## 安装

```bash
# 通过 npm 安装
npm install -g knowledge-connector

# 或通过 ClawHub 安装
clawhub install knowledge-connector
```

## CLI 命令

### 1. 提取知识

```bash
# 从文件提取概念
kc extract -f document.txt

# 从文本提取概念
kc extract -t "人工智能是计算机科学的一个分支"

# 提取并保存到知识库
kc extract -f document.txt --save
```

### 2. 建立关联

```bash
# 自动分析并建立概念关联
kc connect --auto

# 手动建立两个概念的关联
kc connect --from "人工智能" --to "机器学习" --relation "包含"

# 批量导入关系
kc connect --file relations.json
```

### 3. 查询知识

```bash
# 搜索概念
kc query "人工智能"

# 查看概念详情
kc query --concept "深度学习" --detail

# 查找关联概念
kc query --concept "神经网络" --related

# 自然语言查询
kc query --ask "什么是机器学习？"
```

### 4. 可视化图谱

```bash
# 生成知识图谱可视化
kc visualize

# 导出为 HTML
kc visualize --format html --output graph.html

# 导出为 JSON
kc visualize --format json --output graph.json

# 只显示特定概念相关的子图
kc visualize --concept "人工智能" --depth 2
```

### 5. 管理知识库

```bash
# 查看统计信息
kc stats

# 导出知识库
kc export --output backup.json

# 导入知识库
kc import --file backup.json

# 清空知识库
kc clear --confirm
```

## 数据结构

### 概念 (Concept)

```json
{
  "id": "uuid",
  "name": "人工智能",
  "type": "domain",
  "aliases": ["AI", "Artificial Intelligence"],
  "description": "计算机科学的一个分支",
  "source": "document.txt",
  "createdAt": "2024-01-01T00:00:00Z",
  "updatedAt": "2024-01-01T00:00:00Z",
  "metadata": {}
}
```

### 关系 (Relation)

```json
{
  "id": "uuid",
  "from": "concept-id-1",
  "to": "concept-id-2",
  "type": "包含",
  "weight": 0.85,
  "source": "auto-extract",
  "createdAt": "2024-01-01T00:00:00Z"
}
```

### 关系类型

- `包含` / `is-a`: 概念包含关系
- `相关` / `related-to`: 一般关联
- `因果` / `causes`: 因果关系
- `顺序` / `follows`: 时序关系
- `对立` / `opposite`: 对立关系
- `相似` / `similar`: 相似关系

## 配置

配置文件位于 `~/.config/knowledge-connector/config.json`:

```json
{
  "dataDir": "~/.local/share/knowledge-connector",
  "autoExtract": true,
  "autoConnect": true,
  "defaultDepth": 2,
  "maxResults": 20,
  "language": "zh-CN"
}
```

## 使用示例

### 示例 1: 构建编程语言知识图谱

```bash
# 提取概念
echo "Python 是一种解释型、高级、通用的编程语言。Java 是面向对象的编程语言。" | kc extract --save

# 建立关联
kc connect --from "Python" --to "编程语言" --relation "is-a"
kc connect --from "Java" --to "编程语言" --relation "is-a"

# 可视化
kc visualize --format html --output languages.html
```

### 示例 2: 查询知识

```bash
# 查找所有编程语言
kc query --type "编程语言"

# 查看与 Python 相关的概念
kc query --concept "Python" --related
```

## API 使用

```javascript
const KnowledgeConnector = require('knowledge-connector');

const kc = new KnowledgeConnector();

// 提取概念
const concepts = await kc.extract('JavaScript 是一种动态类型语言');

// 添加关系
await kc.connect({
  from: 'JavaScript',
  to: '动态类型语言',
  type: 'is-a'
});

// 查询
const results = await kc.query('JavaScript');

// 获取推荐
const recommendations = await kc.recommend('JavaScript');
```

## 注意事项

1. 首次使用时会自动创建数据目录
2. 建议定期备份知识库数据
3. 大量数据时查询性能可能下降，建议定期优化
4. 概念名称区分大小写

## 更新日志

### v1.0.1 (2026-03-12)
- 发布到 ClawHub
- 修复概念提取算法

### v1.0.0 (2024-03-12)
- 初始版本发布
- 实现核心功能：提取、关联、查询、可视化
- CLI 命令完整支持

## 许可证

MIT License
