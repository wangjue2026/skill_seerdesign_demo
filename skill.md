---
name: Seerdesign_demo_Skill
description: SeerDesign 视觉规范 Skill —— 根据用户业务场景，快速生成符合 SeerDesign 规范的高保真 Vue 3 Demo
dependency:
  python: []
  system: []
---

# SeerDesign 视觉规范 Skill

## 1. 任务目标

以**网络安全产品经理**视角理解用户的业务场景，然后根据本技能提供的设计规范，快速生成符合 SeerDesign 视觉标准的高保真 Vue 3 Demo。

## 2. 技术栈

| 项 | 值 |
|---|---|
| 框架 | Vue 3 + TypeScript（`<script setup lang="ts">`） |
|组件库 | Ant Design Vue 4.x（`a-xxx`） |
| 图标 | `@ant-design/icons-vue`（按需引入） |
| 样式 | `<style scoped lang="less">`，覆盖 antdv 默认样式 |
| 产物 | 单文件 `.vue` 组件，保存至 `src/components/demos/` |

## 3. 核心原则（必须阅读遵循！！）

### 3.1 去壳留核

借用 antdv 的**交互逻辑与 DOM 骨架**（`a-table`、`a-drawer`、`a-form`、`a-select` 等），**视觉皮肤用本技能的 Token 完全覆盖**。任何残留的"阿里默认风"都视为违规。

### 3.2 零默认值（Zero-Assumption Policy）

禁止凭经验使用前端常规默认值。所有视觉属性**必须来自本技能规范文档**：

- 颜色 → 查 `SD Global Styles/design-color.md`
- 字号/行高/字重 → 查 `SD Global Styles/design-typography.md`
- 间距/圆角/边框 → 查 `SD Global Styles/design-atomic-spacing.md`
- 布局/栅格 → 查 `SD Global Styles/layout-grid.md`

**查不到时停下来追问，不猜值。**

### 3.3 强制自检

每次生成代码后，**必须执行「6. 验收自检清单」**作为最后一步。未通过自检的产物禁止交付。

## 4. 工作流与规范按需加载协议

### 4.1 页面 Demo 制作逻辑（必须遵循！）

```
用户输入业务场景
  ↓
① 需求理解与产品判断：以网络安全产品经理身份分析需求
   - 识别产品关键词（如 SASE, aTrust, XDR, DR 等）
   - 明确页面类型（Dashboard / 列表管理 / 详情 / 表单 / 导航框架等）
   - 拆解功能模块和数据结构
   - 确认交互流程和信息层级
  ↓
② 读取通用页面模板：SD Page Templates/ 下对应模板
  ↓
③ 读取涉及的通用组件规范：SD Components/ 下对应组件
  ↓
④ 读取 Token 基础：SD Global Styles/ 下全部 4 个文件
  ↓
⑤ 读取视觉风格 & 编码模式：
   - SD patterns/visual-theme.md
   - SD patterns/impl-vue3.md
  ↓
⑥ 【按需读取】具体产品规范：
   - 若提及 SASE/云安全访问服务 -> 加载 z-SASE/nav-sase.md
   - 若提及 aTrust/零信任/SDP -> 加载 z-SASE/nav-atrust.md
   - 若提及 XDR/安全托管服务 -> 加载 z-XDR/nav-xdr.md
   - 若提及 DR/端点安全 -> 加载 z-DR/nav-dr.md
  ↓
⑦ 强制检视：「7. 常见踩坑与绝对红线 (Anti-Patterns)」 —— 必须对照此列表选择正确的封装组件或应用解决方案。
⑧ 生成 .vue 单文件代码（优先引入并使用 SD Base Components 下的二次封装组件）
⑨ 执行「6. 验收自检清单」→ 修复 → 交付
```

### 4.2 页面模板选择规则

根据用户提及的产品关键词，自动选择对应的页面导航框架：

| 产品关键词 | 对应导航框架目录 | 导航特征 |
|---|---|---|
| **SDP, aTrust, SMG, AF** | `SD Page Templates/L-3.0-nav/` | **L 型导航**（顶部一级导航 + 左侧二三级菜单树） |
| **SASE, XDR, DR, aes, ZTP, DSP, AI安全平台, 保护AI平台** | `SD Page Templates/Tree-5.0-nav/` | **纯左树导航**（侧边树形菜单 + 右侧业务内容区） |

当用户未明确产品归属时，优先询问或根据功能复杂度选择。

## 5. 资源地图

### 5.1 SD Global Styles/ — 数值权威（颜色 / 字号 / 间距 / 阴影）

| 文件 | 内容 |
|---|---|
| [design-color.md](SD%20Global%20Styles/design-color.md) | 品牌色、功能色、灰阶色板、基础色板、阴影规范 |
| [design-typography.md](SD%20Global%20Styles/design-typography.md) | 字体调用顺序、字重规范、字号行高映射表 |
| [design-atomic-spacing.md](SD%20Global%20Styles/design-atomic-spacing.md) | 圆角、边框色、投影、交互手势、Placeholder、间距系统 |
| [layout-grid.md](SD%20Global%20Styles/layout-grid.md) | 布局原语、24 列栅格、间距 Token、高度系统、页面骨架蓝图 |

### 5.2 SD patterns/ — 视觉风格 / 编码模式 / Do-and-Don't

| 文件 | 内容 |
|---|---|
| [visual-theme.md](SD%20patterns/visual-theme.md) | 整体视觉风格关键词、品牌气质、标志性视觉特征、反例 |
| [dos-and-donts.md](SD%20patterns/dos-and-donts.md) | 17 条成对实践规则 + 12 条自检 checklist |
| [impl-vue3.md](SD%20patterns/impl-vue3.md) | Vue3 + ant-design-vue 4.x 表格/标签/图标实现规则 |

### 5.3 SD Components/ — 通用组件视觉规范

| 文件 | 组件 |
|---|---|
| [comp-alert.md](SD%20Components/comp-alert.md) | 警告提示（普通/告警提示条） |
| [comp-basic-search.md](SD%20Components/comp-basic-search.md) | 基础搜索框 |
| [comp-button.md](SD%20Components/comp-button.md) | 按钮（主按钮/普通按钮） |
| [comp-checkbox.md](SD%20Components/comp-checkbox.md) | 复选框（基础/按钮样式） |
| [comp-date-picker.md](SD%20Components/comp-date-picker.md) | 复合日期筛选器 |
| [comp-detail-card.md](SD%20Components/comp-detail-card.md) | 详情概览卡片 |
| [comp-drawer.md](SD%20Components/comp-drawer.md) | 抽屉 |
| [comp-input.md](SD%20Components/comp-input.md) | 输入框（标准/密码/文本域） |
| [comp-message.md](SD%20Components/comp-message.md) | 全局提示（成功/信息/警告/错误/加载） |
| [comp-modal.md](SD%20Components/comp-modal.md) | 弹窗 |
| [comp-page-title.md](SD%20Components/comp-page-title.md) | 页面标题/页头 |
| [comp-pro-search.md](SD%20Components/comp-pro-search.md) | 复合搜索框 |
| [comp-radio.md](SD%20Components/comp-radio.md) | 单选框 |
| [comp-select.md](SD%20Components/comp-select.md) | 选择器（单选/多选） |
| [comp-stepper.md](SD%20Components/comp-stepper.md) | 步骤条（横向/纵向） |
| [comp-table.md](SD%20Components/comp-table.md) | 表格（含分页器） |
| [comp-tabs.md](SD%20Components/comp-tabs.md) | 标签页 |
| [comp-tag.md](SD%20Components/comp-tag.md) | 标签（浅色/深色/点状/Icon+色块等） |
| [comp-tree.md](SD%20Components/comp-tree.md) | 树组件 |
| [design-form.md](SD%20Components/design-form.md) | 表单规范（表单项、布局模式、场景示例） |

### 5.4 SD Page Templates/ — 页面模板 & 导航框架

| 文件 / 目录 | 模板 |
|---|---|
| [page-left-nav.md](SD%20Page%20Templates/page-left-nav.md) | 左侧导航页面通用内容模块规范 |
| [page-l-nav.md](SD%20Page%20Templates/page-l-nav.md) | L 型导航页面通用内容模块规范 |
| [L-3.0-nav/framework.md](SD%20Page%20Templates/L-3.0-nav/framework.md) | L 型导航基本框架与尺寸规范 |
| [L-3.0-nav/base-table-page.md](SD%20Page%20Templates/L-3.0-nav/base-table-page.md) | L 型导航基础表格页规范 |
| [L-3.0-nav/left-tree-table-page.md](SD%20Page%20Templates/L-3.0-nav/left-tree-table-page.md) | L 型导航左树右表页规范 |
| [L-3.0-nav/form-config-page.md](SD%20Page%20Templates/L-3.0-nav/form-config-page.md) | L 型导航表单配置页规范 |
| [L-3.0-nav/step-config-page.md](SD%20Page%20Templates/L-3.0-nav/step-config-page.md) | L 型导航步骤配置页规范 |
| [Tree-5.0-nav/framework.md](SD%20Page%20Templates/Tree-5.0-nav/framework.md) | 纯左树导航基本框架与尺寸规范 |
| [Tree-5.0-nav/base-table-page.md](SD%20Page%20Templates/Tree-5.0-nav/base-table-page.md) | 纯左树导航基础表格页规范 |
| [Tree-5.0-nav/left-tree-table-page.md](SD%20Page%20Templates/Tree-5.0-nav/left-tree-table-page.md) | 纯左树导航左树右表页规范 |
| [Tree-5.0-nav/form-config-page.md](SD%20Page%20Templates/Tree-5.0-nav/form-config-page.md) | 纯左树导航表单配置页规范 |
| [Tree-5.0-nav/overview-table-page.md](SD%20Page%20Templates/Tree-5.0-nav/overview-table-page.md) | 纯左树导航总览展示表格页规范 |
| [Tree-5.0-nav/dashboard.md](SD%20Page%20Templates/Tree-5.0-nav/dashboard.md) | 纯左树导航数据大屏总览页规范 |
| [Tree-5.0-nav/detail.md](SD%20Page%20Templates/Tree-5.0-nav/detail.md) | 纯左树导航详情页规范 |
| [Tree-5.0-nav/basic_display_table.md](SD%20Page%20Templates/Tree-5.0-nav/basic_display_table.md) | 纯左树导航基础展示表格页规范 |


### 5.5 业务产品专属导航规范目录（按提示词需求读取）

这些是各具体产品的专属业务规范和导航布局，与 SD 公共规范存在扩充关系。开发时请根据具体的提示词动态调用：

| 产品分类 | 物理文件路径 | 包含内容 |
|---|---|---|
| **SASE** | [nav-sase.md](z-SASE/nav-sase.md) | SASE 产品导航框架（图标 / 间距 / 色彩 / 菜单树） |
| **SASE (aTrust)** | [nav-atrust.md](z-SASE/nav-atrust.md) | aTrust 零信任导航框架及客户端菜单对齐体系 |
| **XDR** | [nav-xdr.md](z-XDR/nav-xdr.md) | Sangfor XDR 导航框架规范（GPT 标签 / 双行 Header / 互斥手风琴） |
| **DR** | [nav-dr.md](z-DR/nav-dr.md) | DR 下一代端点安全导航框架及视觉红线说明 |

### 5.6 assets/ — 资产文件

| 文件 | 内容 |
|---|---|
| [css-overrides.css](assets/css-overrides.css) | CSS 覆盖模板（色彩变量、字体变量、AntD 覆盖代码） |

---

## 6. 验收自检清单

每次生成代码后，**必须逐条核查**（来源：`SD patterns/dos-and-donts.md`）：

| # | 检查项 | 查询来源 |
|---|---|---|
| 1 | 颜色全部使用 CSS 变量或 Token，无硬编码 hex | `SD Global Styles/design-color.md` |
| 2 | 间距值属于 {2, 4, 8, 12, 16, 24, 32} | `SD Global Styles/design-atomic-spacing.md` |
| 3 | 字号属于 {12, 14, 16, 20, 24, 30} | `SD Global Styles/design-typography.md` |
| 4 | 字重仅为 400 或 600 | `SD Global Styles/design-typography.md` |
| 5 | 行高 = 字号 + 8px | `SD Global Styles/design-typography.md` |
| 6 | 圆角按层级：控件 2px / 容器 4px / 表格 0px | `SD Global Styles/design-atomic-spacing.md` |
| 7 | 阴影使用 Token（dropshadow-s1/s2/s3） | `SD Global Styles/design-color.md` |
| 8 | 按钮 mode 语义正确（一屏一个 primary） | `SD patterns/dos-and-donts.md` |
| 9 | 状态色级别选对（info/warning/risk/error/fatal） | `SD Global Styles/design-color.md` |
| 10 | 禁止蓝色外发光阴影（focus 态 box-shadow: none） | `SD Global Styles/design-atomic-spacing.md` |
| 11 | 动效使用 motion Token（0.18s/0.24s/0.3s） | `SD patterns/visual-theme.md` |
| 12 | 可点击元素 hover 时 cursor: pointer | `SD Global Styles/design-atomic-spacing.md` |

**全部通过后方可交付。任何一项不通过，必须修复后重新自检。**

## 7. 常见踩坑与绝对红线 (Anti-Patterns)

为了根治由于 Ant Design 默认样式导致的各类视觉偏差，我们在 `SD Base Components/` 目录下提供了二开基础组件。在制作 Demo 时，**必须强制检视以下常见问题，并直接套用给出的解决办法**：

| 组件 | 常见错误现象 | 强制解决办法 (必须执行) |
|---|---|---|
| **按钮 (Button)** | 自动添加未声明的图标；文字变成红色；默认高度不是 32px | **必须使用 `<SdButton>`**。该组件已默认锁死 32px 高度。若使用原生 `<a-button>`，必须显式加上 `style="height: 32px;"` 且绝不能乱猜图标、禁止红色文字。 |
| **表格 (Table)** | 出现第一行空白行；字段过多时不会自动冻结操作列；表格内 Switch 开关样式异常 | **必须使用 `<SdTable>`**。若无法使用，则必须：1. CSS 强行清除第一行空白；2. Columns 中最后的操作列必须加上 `fixed: 'right'`；3. 覆盖 Switch 高度至规范尺寸。 |
| **选择器 (Select)** | 高度不对；描边圆角不对；下拉面板里面的样式不对 | **必须使用 `<SdSelect>`**。若无法使用，原生 `a-select` 必须手动约束 `.ant-select-selector { height: 32px !important; border-radius: 2px !important; }`。 |
| **表单 (Form)** | 星号不对齐；Label 与内容间距过大；内容区的组件长短不一无法两端对齐 | **必须使用 `<SdForm>`**。原生使用时必须：1. 统一设定表单项宽度（如 `width: 100%`）；2. 使用统一的 Label 栅格比例；3. CSS 强行修正 `::before` 星号的对齐。 |
| **抽屉 (Drawer)** | 关闭按钮自动跑到最左上角；保存/取消按钮在右下方（位置异常） | **必须使用 `<SdDrawer>`**。若使用原生，必须通过 `#title` 和 `#extra` 插槽手动将关闭按钮放在左侧，动作按钮放在指定位置，禁止使用默认 header 布局。 |
| **搜索框 (Search)** | 尺寸默认给了 40px；输入框内又套了一个框 | **必须使用 `<SdSearch>`**。若使用原生 `<a-input-search>`，必须强制设置 `size="middle"` (对应 32px，千万别用 large)，并仔细检查 DOM 结构避免二次嵌套。 |

> **最高指令**：在遇到上述组件时，你的首选方案是引入 `import { SdButton, SdTable, SdSelect, SdForm, SdDrawer, SdSearch } from '../../../SKillS/skill_seerdesign_demo/SD Base Components';` 并直接使用它们，而不是每次写冗长的 CSS 来修补 `a-xxx`。

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
| **“样式快修”** 或 **“界面微调”** | **极速视觉/布局修复模式** | 1. **禁用浏览器子代理**：100% 禁用 headless 浏览器加载 and 模拟操作。<br>2. **静态 DOM 级推导**：直接结合项目文件和组件库的原生 DOM 骨架进行逻辑样式覆盖。<br>3. **极速写入与 Diff**：利用代码修改工具秒级写入 CSS 规则，立即交付，由用户本地刷新实时验证。 |
| **“极速改码”** 或 **“代码秒修”** | **直接静态修改模式** | 1. **跳过完整文档流**：不强制撰写实现计划 `implementation_plan.md` 等繁琐的工程文档。<br>2. **点对点外科手术式修改**：仅对目标文件指定行进行极速修改，确保无其他冗余代码改动。 |
| *(无特殊指令说明)* | **标准全栈工程流** | 执行完整的设计自检、编写 `implementation_plan.md`、配合浏览器子代理（`browser_subagent`）进行多阶段验证及完整的走查报告。 |

