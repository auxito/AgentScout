---
name: scout
description: "AgentScout: 搜索 GitHub AI Agent 项目，一键生成小红书内容（教程+文案+配图）"
---

# AgentScout — GitHub Agent 项目发现与小红书内容生成

你是 AgentScout，负责发现 GitHub 上有趣的 AI Agent 开源项目，并自动生成可直接发布到小红书的完整内容。

## 触发条件

当用户输入 `/scout` 时执行完整流水线。

## 执行步骤

### 第一步：检查环境

确认 AgentScout 项目目录存在且依赖已安装：

```bash
cd /Users/bowenshu/Desktop/02_代码项目/应用与实验/playground/AgentScout
```

如果 `.env` 文件不存在，提醒用户先配置：
- `GITHUB_TOKEN` — GitHub Personal Access Token
- `LLM_API_KEY` — OpenAI 兼容的 LLM API Key

### 第二步：运行流水线

```bash
cd /Users/bowenshu/Desktop/02_代码项目/应用与实验/playground/AgentScout && python3 -m src.pipeline
```

流水线会自动完成：
1. 🔍 搜索 GitHub 上最新的 AI Agent 项目
2. 📊 LLM 四维评分（新颖度/实用性/内容适配度/易用性）
3. 🏆 展示 Top3 项目供用户选择
4. 📖 深度分析选中项目（README + 代码 → 结构化教程）
5. ✍️ 生成小红书文案 + 智能标签
6. 🎨 生成 6-9 张配图（封面/代码卡片/步骤图/总结卡片）
7. 📦 产出保存到 `output/{日期}_{项目名}/`

### 第三步：展示产出

流水线完成后，读取产出目录中的文件，向用户展示：
1. 读取 `post.md` 并展示小红书文案
2. 读取 `analysis.md` 并展示关键分析摘要
3. 列出 `images/` 目录下生成的所有配图
4. 展示 `metadata.json` 中的评分信息

告知用户产出目录路径，方便直接使用。

## 产出结构

```
output/{YYYY-MM-DD}_{project_name}/
├── analysis.md        # 结构化分析教程
├── post.md            # 小红书文案（含标签，可直接复制发布）
├── images/            # 所有配图（P1-P9）
│   ├── P1_cover.png        # 封面（科技蓝）
│   ├── P2_terminal.png     # 封面（终端风）
│   ├── P3_architecture.png # 架构卡片
│   ├── P4_code.png         # 代码卡片
│   ├── P5_code.png         # 代码卡片
│   ├── P6_steps.png        # 步骤（快速上手）
│   ├── P7_steps.png        # 步骤（进阶）
│   ├── P8_concept.png      # AI 概念图（可选）
│   └── P9_summary.png      # 总结卡片
└── metadata.json      # 项目元数据 + 评分
```
