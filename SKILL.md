---
name: Seerdesign_demo_Skill
description: SeerDesign 视觉规范 Skill —— 根据用户业务场景，快速生成符合 SeerDesign 规范的高保真 Vue 3 Demo
dependency:
  python: []
  system: []
---

# SeerDesign 视觉规范 Skill

## 1. 任务目标

以**网络安全产品经理**视角理解用户的业务场景，然后根据本技能提供的设计规范，快速生成符合 SeerDesign 视觉标准的高保真 Demo。

## 2. 技术栈

| 项 | 值 |
|---|---|
| 框架 | Vue 3 + TypeScript（`<script setup lang="ts">`） |
| 组件库 | Ant Design Vue 4.x（`a-xxx`） |
| 图标 | `@ant-design/icons-vue`（按需引入） |
| 样式 | `<style scoped lang="less">`，覆盖 antdv 默认样式 |
| 产物 | 单文件 `.vue` 组件，保存至 `src/components/demos/` |

## 3. 核心原则（必须阅读遵循！！）

### 3.1 去壳留核

借用 antdv 的**交互逻辑与 DOM 骨架**（`a-table`、`a-drawer`、`a-form`、`a-select` 等），**视觉皮肤用本技能的 Token 完全覆盖**。任何残留的"阿里默认风"都视为违规。

### 3.2 零默认值（Zero-Assumption Policy）

禁止凭经验使用前端常规默认值。所有视觉属性**必须来自本技能规范文档**：

- 颜色 → 查 `references/tokens/design-color.md`
- 字号/行高/字重 → 查 `references/tokens/design-typography.md`
- 间距/圆角/边框 → 查 `references/tokens/design-atomic-spacing.md`
- 布局/栅格 → 查 `references/tokens/layout-grid.md`

**查不到时停下来追问，不猜值。**

### 3.3 强制自检

每次生成代码后，**必须执行「5.3 设计一致性自检」**作为最后一步。未通过自检的产物禁止交付。

## 4. 工作流

### 4.1 页面 Demo 制作逻辑（必须遵循！）

```
用户输入业务场景
  ↓
① 需求理解：以网络安全产品经理身份分析需求
   - 明确页面类型（Dashboard / 列表管理 / 详情 / 表单 / 导航框架等）
   - 拆解功能模块和数据结构
   - 确认交互流程和信息层级
  ↓
② 读取页面模板：references/page-templates/ 下对应模板
  ↓
③ 读取涉及的组件规范：references/components/ 下对应组件
  ↓
④ 读取 Token 基础：references/tokens/ 下全部 4 个文件
  ↓
⑤ 读取视觉风格 & 编码模式：
   - references/patterns/visual-theme.md
   - references/patterns/impl-vue3.md
  ↓
⑥ 生成 .vue 单文件代码
  ↓
⑦ 执行「5.3 设计一致性自检」→ 修复 → 交付
```

### 4.2 页面模板选择规则

根据用户提及的产品关键词，自动选择对应的页面导航框架：

| 产品关键词 | 对应导航框架目录 | 导航特征 |
|---|---|---|
| **SDP, aTrust, SMG, AF** | `references/page-templates/L-3.0-nav/` | **L 型导航**（顶部一级导航 + 左侧二三级菜单树） |
| **SASE, XDR, aes, ZTP, DSP, AI安全平台, 保护AI平台** | `references/page-templates/Tree-5.0-nav/` | **纯左树导航**（侧边树形菜单 + 右侧业务内容区） |

当用户未明确产品归属时，优先询问或根据功能复杂度选择。

## 5. 资源地图

### 5.1 tokens/ — 数值权威（颜色 / 字号 / 间距 / 阴影）

| 文件 | 内容 |
|---|---|
| [design-color.md](references/tokens/design-color.md) | 品牌色、功能色、灰阶色板、基础色板、阴影规范 |
| [design-typography.md](references/tokens/design-typography.md) | 字体调用顺序、字重规范、字号行高映射表 |
| [design-atomic-spacing.md](references/tokens/design-atomic-spacing.md) | 圆角、边框色、投影、交互手势、Placeholder、间距系统 |
| [layout-grid.md](references/tokens/layout-grid.md) | 布局原语、24 列栅格、间距 Token、高度系统、页面骨架蓝图 |

### 5.2 patterns/ — 视觉风格 / 编码模式 / Do-and-Don't

| 文件 | 内容 |
|---|---|
| [visual-theme.md](references/patterns/visual-theme.md) | 整体视觉风格关键词、品牌气质、标志性视觉特征、反例 |
| [dos-and-donts.md](references/patterns/dos-and-donts.md) | 17 条成对实践规则 + 12 条自检 checklist |
| [impl-vue3.md](references/patterns/impl-vue3.md) | Vue3 + ant-design-vue 4.x 表格/标签/图标实现规则 |

### 5.3 components/ — 组件视觉规范（20 个文件）

| 文件 | 组件 |
|---|---|
| [comp-alert.md](references/components/comp-alert.md) | 警告提示（普通/告警提示条） |
| [comp-basic-search.md](references/components/comp-basic-search.md) | 基础搜索框 |
| [comp-button.md](references/components/comp-button.md) | 按钮（主按钮/普通按钮） |
| [comp-checkbox.md](references/components/comp-checkbox.md) | 复选框（基础/按钮样式） |
| [comp-date-picker.md](references/components/comp-date-picker.md) | 复合日期筛选器 |
| [comp-detail-card.md](references/components/comp-detail-card.md) | 详情概览卡片 |
| [comp-drawer.md](references/components/comp-drawer.md) | 抽屉 |
| [comp-input.md](references/components/comp-input.md) | 输入框（标准/密码/文本域） |
| [comp-message.md](references/components/comp-message.md) | 全局提示（成功/信息/警告/错误/加载） |
| [comp-modal.md](references/components/comp-modal.md) | 弹窗 |
| [comp-page-title.md](references/components/comp-page-title.md) | 页面标题/页头 |
| [comp-pro-search.md](references/components/comp-pro-search.md) | 复合搜索框 |
| [comp-radio.md](references/components/comp-radio.md) | 单选框 |
| [comp-select.md](references/components/comp-select.md) | 选择器（单选/多选） |
| [comp-stepper.md](references/components/comp-stepper.md) | 步骤条（横向/纵向） |
| [comp-table.md](references/components/comp-table.md) | 表格（含分页器） |
| [comp-tabs.md](references/components/comp-tabs.md) | 标签页 |
| [comp-tag.md](references/components/comp-tag.md) | 标签（浅色/深色/点状/Icon+色块等） |
| [comp-tree.md](references/components/comp-tree.md) | 树组件 |
| [design-form.md](references/components/design-form.md) | 表单规范（表单项、布局模式、场景示例） |
| [nav-sase.md](references/components/nav-sase.md) | SASE 产品导航框架（图标/间距/颜色） |
| [nav-atrust.md](references/components/nav-atrust.md) | aTrust 零信任导航框架 |
| [nav-xdr.md](references/components/nav-xdr.md) | XDR 产品导航框架 |
| [nav-dr.md](references/components/nav-dr.md) | DR 下一代端点安全导航框架 |

### 5.4 page-templates/ — 页面模板 & 导航框架

| 文件 / 目录 | 模板 |
|---|---|
| [dashboard.md](references/page-templates/Tree-5.0-nav/dashboard.md) | Dashboard 数据总览页 |
| [detail.md](references/page-templates/Tree-5.0-nav/detail.md) | 详情页（左主右辅布局） |
| [basic_display_table.md](references/page-templates/Tree-5.0-nav/basic_display_table.md) | 基础展示页布局 |
| [L-3.0-nav/](references/page-templates/L-3.0-nav/) | **L 型导航组件规范**（含基础表格、左树表格、表单配置、步骤配置） |
| [Tree-5.0-nav/](references/page-templates/Tree-5.0-nav/) | **纯左树导航组件规范**（含基础表格、左树表格、表单配置、概览表格） |
| [nav-atrust.md](references/components/nav-atrust.md) | aTrust 零信任导航框架 |
| [nav-dr.md](references/components/nav-dr.md) | DR 下一代端点安全导航框架 |
| [nav-sase.md](references/components/nav-sase.md) | SASE 产品导航框架 |
| [nav-xdr.md](references/components/nav-xdr.md) | XDR 产品导航框架 |

### 5.5 assets/ — 资产文件

| 文件 | 内容 |
|---|---|
| [css-overrides.css](assets/css-overrides.css) | CSS 覆盖模板（色彩变量、字体变量、AntD 覆盖代码） |

## 6. 验收自检清单

每次生成代码后，**必须逐条核查**（来源：`references/patterns/dos-and-donts.md`）：

| # | 检查项 | 查询来源 |
|---|---|---|
| 1 | 颜色全部使用 CSS 变量或 Token，无硬编码 hex | `tokens/design-color.md` |
| 2 | 间距值属于 {2, 4, 8, 12, 16, 24, 32} | `tokens/design-atomic-spacing.md` |
| 3 | 字号属于 {12, 14, 16, 20, 24, 30} | `tokens/design-typography.md` |
| 4 | 字重仅为 400 或 600 | `tokens/design-typography.md` |
| 5 | 行高 = 字号 + 8px | `tokens/design-typography.md` |
| 6 | 圆角按层级：控件 2px / 容器 4px / 表格 0px | `tokens/design-atomic-spacing.md` |
| 7 | 阴影使用 Token（dropshadow-s1/s2/s3） | `tokens/design-color.md` |
| 8 | 按钮 mode 语义正确（一屏一个 primary） | `patterns/dos-and-donts.md` |
| 9 | 状态色级别选对（info/warning/risk/error/fatal） | `tokens/design-color.md` |
| 10 | 禁止蓝色外发光阴影（focus 态 box-shadow: none） | `tokens/design-atomic-spacing.md` |
| 11 | 动效使用 motion Token（0.18s/0.24s/0.3s） | `patterns/visual-theme.md` |
| 12 | 可点击元素 hover 时 cursor: pointer | `tokens/design-atomic-spacing.md` |

**全部通过后方可交付。任何一项不通过，必须修复后重新自检。**

## 7. 注意事项

- 严禁使用 AntD 默认的蓝色焦点阴影
- 严禁使用 `size="small"` 控制表格行高，必须通过 CSS 强制锁定
- 严禁使用 rgba / hex 透明度拼接作为标签背景色，必须使用 Token
- 所有颜色必须使用 SeerDesign Token CSS 变量
- 图标使用 `@ant-design/icons-vue` 的稳定图标，不确定是否存在时优先省略
- 如果规范中查不到某个值，**停下来追问用户**，不得猜测

## 8. 高效开发与快修协议 (Style Quick-Fix / Hotfix Mode)

为了保障在敏捷迭代和细节打磨阶段的高效交付，当用户在输入提示词中明确提及“快修”意图（包含以下特定修饰指令）时，系统必须立即跳过重型自动化工具和多阶段计划文档，切换为**“静态分析、极速编码”**的秒修模式。

### 8.1 快修指令对照表

| 触发指令词 | 激活工作模式 | 行为特征与执行约束 |
|---|---|---|
| **“样式快修”** 或 **“界面微调”** | **极速视觉/布局修复模式** | 1. **禁用浏览器子代理**：100% 禁用 headless 浏览器加载和模拟操作。<br>2. **静态 DOM 级推导**：直接结合项目文件和组件库的原生 DOM 骨架进行逻辑样式覆盖。<br>3. **极速写入与 Diff**：利用代码修改工具秒级写入 CSS 规则，立即交付，由用户本地刷新实时验证。 |
| **“极速改码”** 或 **“代码秒修”** | **直接静态修改模式** | 1. **跳过完整文档流**：不强制撰写实现计划 `implementation_plan.md` 等繁琐的工程文档。<br>2. **点对点外科手术式修改**：仅对目标文件指定行进行极速修改，确保无其他冗余代码改动。 |
| *(无特殊指令说明)* | **标准全栈工程流** | 执行完整的设计自检、编写 `implementation_plan.md`、配合浏览器子代理（`browser_subagent`）进行多阶段验证及完整的走查报告。 |

### 8.2 编码响应时效要求
- 样式快修与极速改码模式下，系统应在 **10 至 20 秒**内完成定位、修改并交付，实现闪电级的敏捷配合。
