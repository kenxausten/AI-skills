---
name: jira-cli
description: 通过自然语言调用 jira-cli 工具操作 Atlassian Jira。用于查询、创建、编辑问题，管理史诗、迭代、版本等。
---

# Jira CLI Skill

这个skill用于通过自然语言调用 jira-cli 工具操作 Atlassian Jira。

## 工具源
https://github.com/ankitpokhrel/jira-cli

## 安装

### 检查是否已安装
```bash
jira --version
```

### 自动安装

**方式一：npm（推荐）**
```bash
npm install -g @stonerzju/jira-cli
```

**方式二：Go安装**
```bash
go install github.com/ankitpokhrel/jira-cli/cmd/jira@latest
```

**方式三：二进制文件**
从 https://github.com/ankitpokhrel/jira-cli/releases 下载对应平台的二进制文件

### 安装检查
如果命令不存在，AI 应该：
1. 提示用户安装 jira-cli
2. 提供上述安装命令
3. 可以选择使用 `npx @stonerzju/jira-cli` 临时运行

## 快速开始

### 初始化配置
```bash
# 交互式初始化
jira init

# 环境变量配置
export JIRA_API_TOKEN="your-api-token"
export JIRA_AUTH_TYPE="basic"  # basic, bearer, mtls
export JIRA_CONFIG_FILE="~/.config/jira/config.yml"
```

# 配置文件为
 ~/.config/.jira/.config.yml

## 命令映射

### Issue管理
- **自然语言**: 列出问题、查看任务、搜索问题
- **命令**: `jira issue list [--project <项目>] [--status <状态>] [--assignee <负责人>] [--priority <优先级>]`

- **自然语言**: 创建问题、新建任务
- **命令**: `jira issue create [--type <类型>] [--summary "<标题>"] [--description "<描述>"] [--priority <优先级>]`

- **自然语言**: 查看问题详情、查看任务详情
- **命令**: `jira issue view <ISSUE-KEY> [--comments <数量>]`

- **自然语言**: 编辑问题、修改任务
- **命令**: `jira issue edit <ISSUE-KEY> [--summary "<新标题>"] [--description "<新描述>"]`

- **自然语言**: 克隆问题、复制任务
- **命令**: `jira issue clone <ISSUE-KEY> [--summary "<新标题>"]`

- **自然语言**: 删除问题、移除任务
- **命令**: `jira issue delete <ISSUE-KEY> [--cascade]`

- **自然语言**: 链接问题、关联任务
- **命令**: `jira issue link <ISSUE-1> <ISSUE-2> <关系类型>`

- **自然语言**: 添加评论、评论任务
- **命令**: `jira issue comment add <ISSUE-KEY> "<评论内容>"`

- **自然语言**: 记录工时、添加工时
- **命令**: `jira issue worklog add <ISSUE-KEY> "<时间>" [--comment "<备注>"]`

- **自然语言**: 移动问题、转移任务
- **命令**: `jira issue move <ISSUE-KEY> [--status "<新状态>"] [--resolution "<解决结果>"]`

### Epic管理
- **自然语言**: 列出史诗、查看史诗列表
- **命令**: `jira epic list [--project <项目>] [--status <状态>]`

- **自然语言**: 创建史诗、新建史诗
- **命令**: `jira epic create [--name "<史诗名称>"] [--summary "<标题>"] [--description "<描述>"]`

- **自然语言**: 添加问题到史诗、关联任务到史诗
- **命令**: `jira epic add <EPIC-KEY> <ISSUE-KEY> [<ISSUE-KEY2>...]`

- **自然语言**: 从史诗移除问题、取消任务关联
- **命令**: `jira epic remove <ISSUE-KEY> [<ISSUE-KEY2>...]`

### Sprint管理
- **自然语言**: 列出迭代、查看Sprint列表
- **命令**: `jira sprint list [--project <项目>] [--state <状态>]`

- **自然语言**: 查看当前迭代、当前Sprint
- **命令**: `jira sprint list --current`

- **自然语言**: 查看上一个迭代、上一个Sprint
- **命令**: `jira sprint list --prev`

- **自然语言**: 查看下一个迭代、下一个Sprint
- **命令**: `jira sprint list --next`

- **自然语言**: 添加问题到迭代、分配任务到Sprint
- **命令**: `jira sprint add <SPRINT-ID> <ISSUE-KEY> [<ISSUE-KEY2>...]`

- **自然语言**: 创建迭代、新建Sprint
- **命令**: `jira sprint create [--name "<迭代名称>"] [--start-date "<开始日期>"] [--end-date "<结束日期>"]`

- **自然语言**: 关闭迭代、结束Sprint
- **命令**: `jira sprint close <SPRINT-ID> [--name "<新迭代名称>"]`

### 项目管理
- **自然语言**: 列出项目、查看项目列表
- **命令**: `jira project list`

- **自然语言**: 打开项目、访问项目
- **命令**: `jira open <PROJECT-KEY>`

### 看板管理
- **自然语言**: 列出看板、查看看板列表
- **命令**: `jira board list [--project <项目>]`

### 版本管理
- **自然语言**: 列出版本、查看Release列表
- **命令**: `jira release list [--project <项目>]`

### 用户信息
- **自然语言**: 获取我的信息、当前用户
- **命令**: `jira me`

- **自然语言**: 打开问题、在浏览器中查看
- **命令**: `jira open <ISSUE-KEY>`

## 参数说明

| 参数 | 说明 |
|------|------|
| ISSUE-KEY | 问题键（如PROJ-123） |
| PROJECT-KEY | 项目键（如PROJ） |
| EPIC-KEY | 史诗键（如PROJ-456） |
| SPRINT-ID | 迭代ID（数字） |
| --project/-p | 指定项目 |
| --status/-s | 状态过滤 |
| --assignee/-a | 负责人过滤 |
| --priority/-y | 优先级过滤 |
| --type/-t | 问题类型 |
| --summary/-s | 问题标题 |
| --description/-b | 问题描述 |
| --labels/-l | 标签（可多个） |
| --components/-c | 组件（可多个） |
| --fix-version | 修复版本 |
| --plain | 纯文本输出模式 |
| --raw | 原始JSON输出 |
| --csv | CSV格式输出 |
| --table | 表格视图（用于epic/sprint） |
| --no-input | 跳过交互式提示 |
| --current | 当前迭代 |
| --prev | 上一个迭代 |
| --next | 下一个迭代 |
| --state | 迭代状态（active, future, closed） |
| --cascade | 级联删除（包含子任务） |

## 使用示例

### 列出问题
```
用户: 列出我负责的高优先级问题
AI: jira issue list -a$(jira me) -yHigh
```

### 创建问题
```
用户: 创建一个Bug类型的问题
AI: jira issue create -tBug -s"新发现的Bug" -yHigh -lbug -b"Bug描述" --no-input
```

### 查看问题详情
```
用户: 查看PROJ-123问题的详情
AI: jira issue view PROJ-123 --comments 5
```

### 添加评论
```
用户: 给PROJ-123添加评论"已修复"
AI: jira issue comment add PROJ-123 "已修复"
```

### 记录工时
```
用户: 给PROJ-123记录2小时工时
AI: jira issue worklog add PROJ-123 "2h" --comment "修复Bug"
```

### 列出当前迭代
```
用户: 查看当前迭代的所有问题
AI: jira sprint list --current
```

### 创建史诗
```
用户: 创建一个名为"新功能开发"的史诗
AI: jira epic create -n"新功能开发" -s"新功能开发史诗" -b"史诗描述" --no-input
```

### 列出项目
```
用户: 列出所有我有权限的项目
AI: jira project list
```

## 高级用法

### JQL查询
```bash
# 使用JQL查询
jira issue list --jql "project = PROJ AND status = 'In Progress'"

# 组合查询
jira issue list -q "summary ~ 'bug' AND priority = High"
```

### 批量操作
```bash
# 批量添加问题到迭代
jira sprint add 123 PROJ-1 PROJ-2 PROJ-3

# 批量添加问题到史诗
jira epic add PROJ-100 PROJ-1 PROJ-2 PROJ-3
```

### 输出格式控制
```bash
# JSON格式输出（适合脚本处理）
jira issue list --raw

# CSV格式输出
jira issue list --csv

# 纯文本输出
jira issue list --plain --columns key,summary,status,assignee
```

### 时间过滤
```bash
# 最近7天创建的问题
jira issue list --created -7d

# 最近30分钟更新的问题
jira issue list --updated -30m

# 本月创建的问题
jira issue list --created month
```

## 注意事项

1. **认证配置**: 首次使用需要运行 `jira init` 配置Jira实例信息
2. **API Token**: 需要在Atlassian账户设置中生成API Token
3. **项目权限**: 只能访问有权限的项目
4. **输出格式**: 默认使用交互式UI，脚本处理时使用 `--plain` 或 `--raw` 参数
5. **批量限制**: 批量操作通常限制为50个问题
6. **Jira版本**: 支持Jira Cloud和Jira Server/Data Center

## 故障排除

### 常见问题
1. **命令不存在**: 确保已正确安装jira-cli
2. **认证失败**: 检查 `jira init` 配置和API Token
3. **权限不足**: 确认有项目访问权限
4. **网络问题**: 检查Jira实例可访问性

### 调试模式
```bash
# 启用详细日志
export JIRA_DEBUG=true
jira issue list
```

### 配置文件位置
- Linux/macOS: `~/.config/jira/config.yml`
- Windows: `%APPDATA%\jira\config.yml`
