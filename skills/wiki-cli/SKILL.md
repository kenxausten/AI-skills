---
name: wiki-cli
description: 通过自然语言调用 confluence-cli 工具操作 Confluence Wiki。用于读取、搜索、创建、编辑页面等。
---

# Confluence CLI Skill

这个skill用于通过自然语言调用 confluence-cli 工具操作 Confluence Wiki。

## 工具源
https://github.com/pchuri/confluence-cli

## 安装

### 检查是否已安装
```bash
confluence --version
```

### 自动安装

**方式一：npm（推荐）**
```bash
npm install -g confluence-cli
```

**方式二：Homebrew（macOS/Linux）**
```bash
brew install pchuri/tap/confluence-cli
```

**方式三：直接运行（无需安装）**
```bash
npx confluence-cli --help
```

### 安装检查
如果命令不存在，AI 应该：
1. 提示用户安装 confluence-cli
2. 提供上述安装命令
3. 可以选择使用 `npx confluence-cli` 临时运行

## 快速开始

### 初始化配置
```bash
# 交互式初始化
confluence init

# 非交互式初始化
confluence init --domain "wiki.eniot.io" --api-path "/rest/api" --auth-type "basic" --email "your-id" --token "your-password"
```

# 配置文件
~/.confluence-cli/config.json

### 环境变量配置
```bash
export CONFLUENCE_DOMAIN="wiki.eniot.io"
export CONFLUENCE_API_TOKEN="your-password"
export CONFLUENCE_EMAIL="your-id"
export CONFLUENCE_API_PATH="/rest/api"
export CONFLUENCE_AUTH_TYPE="basic"
export CONFLUENCE_READ_ONLY=true
```

## 命令映射

### 读取页面
- **自然语言**: 读取页面、查看页面内容、获取页面
- **命令**: `confluence read <pageId或URL> [--format markdown|html|text]`

### 页面信息
- **自然语言**: 页面详情、页面信息、查看页面元数据
- **命令**: `confluence info <pageId或URL>`

### 搜索页面
- **自然语言**: 搜索、查找页面、搜索内容
- **命令**: `confluence search "<关键词>" [--limit <数量>]`

### 列出空间
- **自然语言**: 列出所有空间、查看空间列表
- **命令**: `confluence spaces`

### 查找页面
- **自然语言**: 按标题查找页面、找页面
- **命令**: `confluence find "<标题>" [--space <空间Key>]`

### 列出子页面
- **自然语言**: 列出子页面、查看页面层级
- **命令**: `confluence children <pageId> [--recursive] [--format tree|list|json]`

### 创建页面
- **自然语言**: 创建页面、新建页面
- **命令**: `confluence create "<标题>" <空间Key> --content "<内容>" --format markdown`

### 创建子页面
- **自然语言**: 创建子页面、在某页面下创建新页面
- **命令**: `confluence create-child "<标题>" <父页面Id> --content "<内容>" --format markdown`

### 更新页面
- **自然语言**: 更新页面、修改页面内容
- **命令**: `confluence update <pageId> [--title "<新标题>"] [--content "<新内容>"] [--file <文件路径>] --format markdown`

### 移动页面
- **自然语言**: 移动页面、迁移页面
- **命令**: `confluence move <pageId> <新父页面Id> [--title "<新标题>"]`

### 删除页面
- **自然语言**: 删除页面、移除页面
- **命令**: `confluence delete <pageId> [--yes]`

### 附件操作
- **列出附件**: `confluence attachments <pageId> [--pattern "*.png"] [--limit <数量>]`
- **下载附件**: `confluence attachments <pageId> --download --dest <目录>`
- **上传附件**: `confluence attachment-upload <pageId> --file <文件路径> [--comment "<备注>"]`
- **删除附件**: `confluence attachment-delete <pageId> <attachmentId> [--yes]`

### 评论操作
- **列出评论**: `confluence comments <pageId> [--format markdown|json]`
- **添加评论**: `confluence comment <pageId> --content "<评论内容>"`
- **删除评论**: `confluence comment-delete <commentId> [--yes]`

### 属性操作
- **列出属性**: `confluence property-list <pageId>`
- **获取属性**: `confluence property-get <pageId> <key>`
- **设置属性**: `confluence property-set <pageId> <key> --value '<JSON值>'`
- **删除属性**: `confluence property-delete <pageId> <key> [--yes]`

### 导出页面
- **自然语言**: 导出页面、下载页面
- **命令**: `confluence export <pageId> --dest <目录> [--format markdown|html|text]`

### 编辑工作流
- **导出编辑**: `confluence edit <pageId> --output <文件>`
- **更新内容**: `confluence update <pageId> --file <文件> --format storage`

### 配置文件管理
- **列出配置**: `confluence profile list`
- **切换配置**: `confluence profile use <profile名称>`
- **添加配置**: `confluence profile add <名称> --domain <域名> --auth-type basic --email <邮箱> --token <token>`
- **删除配置**: `confluence profile remove <名称>`

### 格式转换
- **自然语言**: 转换格式、markdown转confluence格式
- **命令**: `confluence convert --input-file <文件> --input-format markdown --output-format storage`

### 使用统计
- **自然语言**: 查看使用统计
- **命令**: `confluence stats`

## 参数说明

| 参数 | 说明 |
|------|------|
| pageId | 页面ID（数字） |
| URL | 页面URL（需包含pageId参数） |
| spaceKey | 空间Key（如DEV、TEST） |
| --format | 输出格式：markdown、html、text、storage、json |
| --limit | 限制返回结果数量 |
| --recursive | 递归列出所有子页面 |
| --yes | 跳过确认提示 |
| --file | 指定文件路径 |
| --dest | 指定目标目录 |
| --content | 内联内容 |
| --profile | 使用指定配置文件 |

## 使用示例

### 读取页面
```
用户: 读取ID为147535715的页面
AI: confluence read 147535715 --format markdown
```

### 搜索内容
```
用户: 搜索包含"API文档"的页面
AI: confluence search "API文档" --limit 10
```

### 创建新页面
```
用户: 在DEV空间创建一个名为"新功能说明"的页面
AI: confluence create "新功能说明" DEV --content "# 新功能\n\n这里是新功能说明" --format markdown
```

### 列出子页面
```
用户: 列出页面123456789的所有子页面
AI: confluence children 123456789 --recursive --format tree
```

### 导出页面
```
用户: 导出页面147535715到当前目录
AI: confluence export 147535715 --dest . --format markdown
```

### 上传附件
```
用户: 给页面123456789上传一个PDF文件
AI: confluence attachment-upload 123456789 --file ./report.pdf
```

## 注意事项

1. **只读模式**: 建议设置 `CONFLUENCE_READ_ONLY=true` 避免意外修改
2. **API Token**: 需要在 Atlassian 账户设置中生成 API Token
3. **认证方式**: 支持 basic、bearer、cookie、mtls 认证
4. **页面ID获取**: 可以从页面URL中获取（如 pageId=147535715）
