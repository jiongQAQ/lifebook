# Spec Kit 使用流程指南

## 📦 第一步：初始化项目

### 在当前项目中初始化
```bash
# 使用 Claude Code（推荐）
specify init --here --ai claude

# 或使用 GitHub Copilot
specify init --here --ai copilot

# 或使用 Cursor
specify init --here --ai cursor
```

### 创建新项目
```bash
specify init my-project --ai claude
cd my-project
```

---

## 🔄 第二步：开发工作流（7步循环）

### 1️⃣ 建立项目宪法（只需运行一次）
```bash
/speckit.constitution
```

**示例提示**：
```
创建项目原则：
1. 代码质量：使用 TypeScript 严格模式，所有函数必须有类型注解
2. 测试标准：最低 80% 代码覆盖率，使用 Jest 进行单元测试
3. 用户体验：响应式设计，支持移动端，遵循无障碍标准
4. 性能要求：首次内容绘制 < 1.5s，Time to Interactive < 3s
5. 架构原则：组件化设计，关注点分离，DRY 原则
```

**生成的文件**：`.specify/memory/constitution.md`

---

### 2️⃣ 创建功能规范
```bash
/speckit.specify
```

**示例提示**：
```
我想创建一个个人生活记录应用的仪表板功能：

功能描述：
- 显示用户的每日活动统计（步数、卡路里、睡眠时间）
- 展示本周的目标完成进度（使用进度条）
- 显示最近的日记条目（最新3条）
- 提供快速操作按钮：添加日记、记录运动、设置目标

用户故事：
1. 作为用户，我希望一打开应用就能看到今天的活动摘要
2. 作为用户，我希望看到本周目标的完成情况，激励自己
3. 作为用户，我希望快速访问最近的日记，回顾生活
```

**生成的内容**：
- 创建新的 Git 分支（如 `001-dashboard-feature`）
- 生成 `.specify/specs/001-dashboard-feature/spec.md`

---

### 3️⃣ 澄清需求（可选但推荐）
```bash
/speckit.clarify
```

AI 会询问澄清性问题，例如：
- "如果获取活动数据失败怎么办？"
- "进度条应该显示什么颜色？"
- "日记条目应该显示多少字符？"

**好处**：减少后续返工

---

### 4️⃣ 创建技术计划
```bash
/speckit.plan
```

**示例提示**：
```
技术栈选择：
- 框架：Next.js 14（App Router）
- UI 库：shadcn/ui + Tailwind CSS
- 图表：Recharts 
- 状态管理：Zustand
- 数据获取：React Query
- 图标：Lucide React

架构要求：
- 使用 Server Components 渲染静态内容
- 使用 Client Components 处理交互
- API 路由处理数据请求
- 使用 Suspense 和 Loading 状态
```

**生成的文件**：
- `plan.md` - 技术实施计划
- `research.md` - 技术调研文档
- `quickstart.md` - 快速开始指南
- `data-model.md` - 数据模型

---

### 5️⃣ 生成任务列表
```bash
/speckit.tasks
```

**生成的内容**：
详细的任务分解，例如：
```
□ Task 1: 创建仪表板页面组件 (app/dashboard/page.tsx)
□ Task 2: 创建活动统计卡片组件 (components/ActivityCard.tsx)
□ Task 3: 创建进度条组件 (components/ProgressBar.tsx)
□ Task 4: 创建日记列表组件 (components/RecentEntries.tsx)
□ Task 5: 实现数据获取 API (app/api/stats/route.ts)
[P] Task 6-8: 可并行执行的样式和测试任务
□ Task 9: 集成测试
□ Task 10: 性能优化
```

**生成的文件**：`tasks.md`

---

### 6️⃣ 验证一致性（可选）
```bash
/speckit.analyze
```

**功能**：检查 spec、plan、tasks 之间的一致性和冲突

---

### 7️⃣ 实施功能
```bash
/speckit.implement
```

AI 会按照任务列表逐步实施：
1. 创建文件和组件
2. 编写代码
3. 运行测试
4. 修复错误
5. 验证功能

**注意**：AI 会执行本地命令（npm、git 等），确保工具已安装

---

## 🔁 后续功能开发

对于每个新功能，重复步骤 2-7：
```bash
/speckit.specify    # 新功能规范
/speckit.clarify    # 澄清（可选）
/speckit.plan       # 技术计划
/speckit.tasks      # 任务分解
/speckit.analyze    # 验证（可选）
/speckit.implement  # 实施
```

---

## 💡 最佳实践

### ✅ DO（推荐做法）
1. **详细描述需求**：在 specify 阶段提供用户故事、验收标准
2. **使用 clarify**：在 plan 之前运行，减少返工
3. **增量开发**：一次一个功能，不要贪多
4. **人工审核**：检查 AI 生成的 spec、plan、code
5. **提交节点**：每个功能完成后提交到 Git

### ❌ DON'T（避免做法）
1. **不要跳过 constitution**：它是整个项目的基石
2. **不要在 specify 阶段谈技术栈**：聚焦"是什么"而非"怎么做"
3. **不要盲目信任 AI**：生成的代码需要测试和验证
4. **不要一次实施多个任务**：容易丢失上下文
5. **不要忘记写测试**：在 constitution 中要求 TDD

---

## 🛠️ 常用命令

```bash
# 检查安装
specify check

# 升级 Spec Kit
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git

# 查看已安装的工具
uv tool list

# 卸载
uv tool uninstall specify-cli
```

---

## 📂 项目结构

初始化后的目录结构：
```
lifebook/
├── .specify/
│   ├── memory/
│   │   └── constitution.md       # 项目宪法
│   ├── scripts/                  # 自动化脚本
│   ├── specs/                    # 功能规范
│   │   └── 001-dashboard/
│   │       ├── spec.md           # 功能规范
│   │       ├── plan.md           # 技术计划
│   │       ├── tasks.md          # 任务列表
│   │       ├── research.md       # 技术调研
│   │       └── quickstart.md     # 快速开始
│   └── templates/                # 模板文件
├── .github/                      # GitHub 配置
└── [你的项目文件]
```

---

## 🎯 实战示例

### 示例 1：添加用户认证功能

```bash
# 1. 创建规范
/speckit.specify

提示：我想添加用户认证功能，包括：
- 邮箱密码登录
- Google OAuth
- 记住登录状态（7天）
- 忘记密码流程

# 2. 技术计划
/speckit.plan

提示：使用 NextAuth.js v5，Prisma ORM，PostgreSQL 数据库

# 3. 生成任务
/speckit.tasks

# 4. 实施
/speckit.implement
```

### 示例 2：优化现有功能

```bash
/speckit.specify

提示：优化仪表板加载性能：
- 实现增量静态再生成（ISR）
- 添加 Skeleton Loading
- 使用 React Suspense 分步加载
- 优化图片（使用 Next.js Image）
```

---

## 🔗 学习资源

- 官方文档：https://github.com/github/spec-kit
- 视频教程：https://www.youtube.com/playlist?list=PL4cUxeGkcC9h9RbDpG8ZModUzwy45tLjb
- 博客文章：https://blog.logrocket.com/github-spec-kit/

---

## 🆘 故障排除

### 问题 1：slash 命令不可用
**解决**：确保在支持的 AI 编辑器中（VS Code + Copilot / Claude Code）

### 问题 2：Git 分支未自动创建
**解决**：检查 `.specify/scripts/` 脚本权限，手动运行 `chmod +x`

### 问题 3：AI 生成的代码有问题
**解决**：这很正常！人工审核并修改，或重新运行命令并给出更详细提示

---

**祝你使用愉快！🎉**
