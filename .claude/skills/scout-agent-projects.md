---
name: scout-agent-projects
description: 搜索 GitHub 上有趣的 Agent 项目，自动生成小红书可发布内容
trigger: 当用户提到"找项目"、"搜 agent"、"小红书内容"、"AgentScout" 时触发
---

# AgentScout - GitHub Agent 项目发现与小红书内容生成

## 概述
AgentScout 自动搜索 GitHub 上最新、最有趣的 AI Agent 开源项目，通过 LLM 评分排名，然后为你选中的项目自动生成：
- 📖 结构化分析教程（analysis.md）
- ✍️ 小红书文案 + 标签（post.md）
- 🖼️ 6-9 张配图（封面、架构、代码卡片、步骤卡片、总结卡片）

## 使用方式

```bash
# 进入项目目录
cd AgentScout

# 安装依赖
pip install -r requirements.txt
playwright install chromium  # 可选，用于网页截图

# 配置环境变量
cp .env.example .env
# 编辑 .env，填入 GITHUB_TOKEN 和 LLM_API_KEY

# 运行完整流水线
python -m src.pipeline
```

## 流程
1. 🔍 自动搜索 GitHub（关键词 + 组织监控）
2. 📊 LLM 评分（新颖度/实用性/内容适配度/易用性）
3. 🏆 展示 Top3 摘要，用户选择一个
4. 📖 深度分析项目（README + 代码 → 结构化教程）
5. ✍️ 生成小红书文案 + 智能标签
6. 🎨 生成 6-9 张配图
7. 📦 产出保存在 `output/{日期}_{项目名}/`

## 产出结构
```
output/{YYYY-MM-DD}_{project_name}/
├── analysis.md        # 结构化分析教程
├── post.md            # 小红书文案（含标签）
├── images/            # 所有配图
│   ├── P1_cover.png
│   ├── P2_terminal.png
│   ├── ...
│   └── P9_summary.png
└── metadata.json      # 项目元数据 + 评分
```
