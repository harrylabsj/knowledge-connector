# Knowledge Connector

Knowledge Connector 的价值，不是“帮你建一个图”，而是把散落在不同文档里的知识变成可搜索、可解释、可行动的知识图谱结果。

这次升级重点收敛到 6 件事：
- 安装后能自检
- 更像向导的导入入口
- 更顺手的导入体验
- 更能命中中文自然问题的跨文档搜索
- 更容易检查关系的可视化
- 带下一步建议的图谱结果

## 它适合什么问题

- “把这个目录里的笔记都导进来”
- “这个概念到底在哪些文档里出现过”
- “哪些文档之间其实在讲同一件事”
- “围绕这个概念画一个能看懂的关系图”
- “图谱出来以后，我下一步该补什么、查什么、连什么”

## 现在的核心体验

### 1. 安装自检

```bash
kc doctor
```

自检会告诉你：
- 数据目录是否存在、是否可写
- `concepts.json` / `relations.json` / `sources.json` 是否可读
- CLI 入口是否存在
- `kc` 是否在 PATH 中可用

如果依赖还没安装但文件已经在本地，也可以在包目录里运行：

```bash
node bin/cli.js doctor
```

需要指定数据目录时，可以设置 `KC_DATA_DIR=/path/to/data`。

### 2. 导入文档

```bash
kc import-wizard --dir notes/
kc import-docs --dir notes/
kc import-docs --files intro.md roadmap.md ideas.txt
```

导入后会告诉你：
- 预计会导入多少文件
- 支持哪些文件类型
- 导入了多少文档
- 新增或更新了多少来源
- 抽出了多少概念
- 自动补了多少关系

重复导入同一个文件时，会按真实路径识别来源，避免把同一份文档重复塞进来源列表。

### 3. 跨文档搜索

```bash
kc search "强化学习"
kc answer "哪些文档把规划和强化学习连起来了？"
kc query "transformer" --sources
kc query --ask "哪些文档同时提到了规划和强化学习？"
```

搜索结果不只给概念，还会给：
- 命中的来源文档
- 相关关系
- 下一步建议

`kc answer` 会把这些结果整理成更像答案页的输出，也可以保存成 HTML。中文自然问题会先拆出关键词再匹配来源和概念，不再只做整句包含。

### 4. 概念子图

```bash
kc map --concept "人工智能" --depth 2
```

这个命令适合做“围绕一个主题看局部图谱”，比直接扔一整张大图更可操作。

### 5. 图谱可视化

```bash
kc visualize --format html --output graph.html
kc visualize --concept "机器学习" --depth 2 --output ml-graph.html
```

生成的 HTML 图现在会同时显示：
- 图谱本身
- 下一步建议
- 常用后续命令提示

HTML 和 DOT 输出会转义用户输入、概念名和来源路径，避免把文档内容原样注入到可视化页面里。

## 为什么这条产品线值得继续做

因为用户装它，不是为了“又一个知识技能”，而是为了更快回答这些问题：
- 我的知识散在哪里
- 哪些概念其实互相关联
- 哪些文档值得一起看
- 下一步该补什么，而不是只把图存下来

## 安装

```bash
clawhub install knowledge-connector
```

## 一句话卖点

把分散文档变成可导入、可回答、可视化、可行动的知识图谱结果。
