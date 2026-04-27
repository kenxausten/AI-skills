<!-- @AI_GENERATED -->
# Kiro CLI 配置目录

本目录包含 Kiro CLI 的 skills（技能）和 steering（指导）配置。

## Skills 技能列表

Skills 是 Kiro CLI 的扩展能力模块，用于增强 AI 助手在特定领域的功能。

### 文档处理类

| 技能名称 | 功能描述 |
|---------|---------|
| **docx** | 创建、读取、编辑 Word 文档（.docx 文件）。支持格式化、目录、页码、信头等功能。 |
| **pptx** | 处理 PowerPoint 演示文稿。支持创建幻灯片、编辑现有演示文稿、提取内容等。 |
| **pdf** | PDF 文件处理。支持读取/提取文本和表格、合并/拆分 PDF、旋转页面、添加水印、加密/解密、OCR 等。 |
| **xlsx** | 电子表格处理。支持 .xlsx、.xlsm、.csv、.tsv 文件的读取、编辑、创建和格式转换。 |

### 开发工具类

| 技能名称 | 功能描述 |
|---------|---------|
| **claude-api** | 构建、调试和优化 Claude API / Anthropic SDK 应用。支持模型版本迁移、prompt caching、工具调用等功能。 |
| **mcp-builder** | 创建高质量的 MCP（Model Context Protocol）服务器，支持 Python (FastMCP) 和 Node/TypeScript (MCP SDK)。 |
| **webapp-testing** | 使用 Playwright 进行本地 Web 应用测试。支持前端功能验证、UI 调试、截图和浏览器日志查看。 |
| **web-artifacts-builder** | 创建复杂的 HTML artifacts，使用 React、Tailwind CSS、shadcn/ui 等现代前端技术。 |

### 设计与创意类

| 技能名称 | 功能描述 |
|---------|---------|
| **frontend-design** | 创建高质量的前端界面。支持 Web 组件、页面、仪表板、React 组件等。 |
| **canvas-design** | 使用设计理念创建视觉艺术作品（.png 和 .pdf 格式）。支持海报、设计稿等静态作品。 |
| **algorithmic-art** | 使用 p5.js 创建算法艺术。支持流场、粒子系统等生成式艺术。 |
| **slack-gif-creator** | 创建适用于 Slack 的动画 GIF。提供约束验证和动画概念支持。 |
| **theme-factory** | 为 artifacts 应用主题样式。提供 10 种预设主题，支持自定义主题生成。 |
| **brand-guidelines** | 应用 Anthropic 官方品牌颜色和排版风格到各类 artifacts。 |

### 协作与沟通类

| 技能名称 | 功能描述 |
|---------|---------|
| **doc-coauthoring** | 协作文档编写工作流。支持文档、提案、技术规范、决策文档的结构化编写。 |
| **internal-comms** | 内部沟通文档编写。支持状态报告、领导更新、公司通讯、FAQ、事件报告等。 |

### OpenCLI 工具集

| 技能名称 | 功能描述 |
|---------|---------|
| **opencli-usage** | OpenCLI 顶层指南。发现适配器、了解通用标志和输出格式。 |
| **opencli-browser** | 通过 OpenCLI 驱动 Chrome 浏览器。支持页面检查、表单填写、登录流程、数据提取。 |
| **opencli-adapter-author** | 编写 OpenCLI 适配器。支持新站点适配器创建和命令添加。 |
| **opencli-autofix** | 自动修复损坏的 OpenCLI 适配器。诊断失败、修补适配器、重试并提交 issue。 |

### 企业工具类

| 技能名称 | 功能描述 |
|---------|---------|
| **wiki-cli** | 通过自然语言调用 confluence-cli 工具操作 Confluence Wiki。支持读取、搜索、创建、编辑页面。 |
| **jira-cli** | 通过自然语言调用 jira-cli 工具操作 Atlassian Jira。支持查询、创建、编辑问题，管理史诗、迭代、版本。 |

### 其他工具

| 技能名称 | 功能描述 |
|---------|---------|
| **skill-creator** | 创建、修改和优化 skills。支持性能评估、基准测试和描述优化。 |

---

## Steering 指导配置

Steering 配置用于指导 AI 助手的行为规范。

### ai-coding.md

**AI 生成代码标注规则**

所有 AI 生成的代码必须使用 `@AI_GENERATED` 标记进行注释，以实现可追溯性和审计追踪。

主要规则：
- 使用文件原生注释语法添加开始和结束标记
- 支持多种编程语言和文件格式
- 特定文件类型（如 .csv、.log、.lock 文件）不添加标记
- 所有 AI 生成的代码在提交前必须经过审查

---

## 来源说明

部分 skills 来源于 [Anthropic Skills 仓库](https://github.com/anthropics/skills)，包括但不限于：

- algorithmic-art
- brand-guidelines
- canvas-design
- claude-api
- doc-coauthoring
- docx
- frontend-design
- internal-comms
- mcp-builder
- pdf
- pptx
- skill-creator
- slack-gif-creator
- theme-factory
- web-artifacts-builder
- webapp-testing
- xlsx

这些 skills 遵循其各自的 LICENSE 协议。

---

## 目录结构

```
.kiro/
├── skills/              # 技能模块目录
│   ├── algorithmic-art/
│   ├── brand-guidelines/
│   ├── canvas-design/
│   ├── claude-api/
│   ├── doc-coauthoring/
│   ├── docx/
│   ├── frontend-design/
│   ├── internal-comms/
│   ├── jira-cli/
│   ├── mcp-builder/
│   ├── opencli-adapter-author/
│   ├── opencli-autofix/
│   ├── opencli-browser/
│   ├── opencli-usage/
│   ├── pdf/
│   ├── pptx/
│   ├── skill-creator/
│   ├── slack-gif-creator/
│   ├── theme-factory/
│   ├── web-artifacts-builder/
│   ├── webapp-testing/
│   ├── wiki-cli/
│   └── xlsx/
├── steering/            # 指导配置目录
│   └── ai-coding.md
└── README.md
```
<!-- @AI_GENERATED: end -->
