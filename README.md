# CherryStudioTheme.css - Cherry Studio 高性能暗色主题

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Cherry Studio v2](https://img.shields.io/badge/Cherry%20Studio-v2-blueviolet.svg)]()

面向 **Cherry Studio v2** 适配的高性能主题，采用 shadcn 语义变量与玻璃拟态（Glassmorphism）设计，支持浅色/深色双主题，并跟随客户端设置的主题色（`--primary`）自动变色。

## 更新记录

- **2026.09.15**：因 Cherry Studio 更新导致旧主题无法使用，现已适配更新。删去了衬线字体（可在设置页自行调整字体）；将部分元素由写死的绿色改为与用户自定义主题色保持一致；保留原有的遮罩设置。

## 安装

### 使用方式：直接下载

1. 复制或下载 `CherryStudioTheme.css` 文件
2. 打开 Cherry Studio 设置
3. 进入 **「显示设置」→「自定义CSS」**
4. 导入或粘贴 CSS 内容

## 配置

### 设置背景壁纸

在 CSS 文件的 `:root`（浅色）与 `.dark`（深色）中分别修改：

```css
/* 浅色主题壁纸 */
:root {
    --chat-background-image: url("https://example.com/light-bg.png");
}

/* 深色主题壁纸 */
.dark {
    --chat-background-image: url("https://example.com/dark-bg.png");
}
```

支持：
- 本地文件路径（如 `file:///C:/path/to/image.jpg`）
- 在线图片 URL（如 `https://example.com/image.jpg`）

壁纸通过固定背景层（`body::before`）展示，外层再叠加 `--overlay-color` 遮罩，避免壁纸直射文字影响阅读。

### 自定义颜色与透明度

所有颜色均通过 CSS 变量定义，可直接在 `:root` / `.dark` 中覆盖。主题采用「同色系 + 不同透明度」区分层级：

| 变量 | 说明 |
|------|------|
| `--glass` | 卡片层（最高不透明度） |
| `--glass-soft` | 背景 / 侧栏层 |
| `--glass-softer` | 次级层 |
| `--gradient-assistant` | AI 消息气泡渐变 |
| `--gradient-user` | 用户消息气泡渐变 |
| `--gradient-input` | 输入框渐变（实体不透字） |

> 注：`--primary`（主题色）**不硬编码**，由 Cherry Studio 设置里的主题色控制，开关、侧栏选中态等组件会自动跟随。

## 功能说明

### 玻璃拟态层级

- **背景 / 侧栏**：`--glass-soft`，与主背景同色，避免左右割裂
- **卡片**：`--glass`，更不透明，与背景同色系区分
- **浮层**（Popover / Dropdown / Dialog）：与卡片同色或纯色不透壁纸，避免「塑料灰」观感

### 输入框跑马灯霓虹边框

当输入框**获得焦点**时，显示动态渐变边框：

- 颜色方案（`linear-gradient(90deg, ...)`）：
  - 爱马仕橙 `#ff6a01`
  - 紫罗兰 `#8a2be2`
  - 青色 `#00d4ff`
- 采用 `background + mask` 实现，不受全局 `box-shadow: none` 影响

### 统一圆角与原子化覆盖

- 所有圆角统一走 `--radius` 变量（默认读 `--cs-radius-lg`）
- 针对 Tailwind `bg-*`、`rounded-*` 等编译后硬编码的类做兜底覆盖，让玻璃背景生效

### 响应式与无障碍

- 移动端（`max-width: 768px`）缩小跑马灯边框并加速动画
- 尊重 `prefers-reduced-motion`，关闭动画与过渡
- 尊重 `prefers-contrast: high`，提供更高对比的跑马灯配色

## 许可证

本项目采用 [GNU Affero General Public License v3.0](./LICENSE) 或更高版本许可（AGPL-3.0+）。

### 重要说明

- 你可以自由使用、修改和分发本软件
- 任何修改版本必须以相同许可证发布
- 网络使用（如 SaaS）也要求提供源代码
- 必须保留原始版权声明和许可证文本

### 来源

本项目包含来自以下项目的代码或灵感：

| 项目 | 许可证 | 用途 |
|------|--------|------|
| [just-flowing-border.css](https://github.com/Cle2ment/CherryStudio_themes/blob/master/themes/just-flowing-border.css) | MIT-like | 输入框跑马灯边框动画 |
| [LuminaFlow.css](https://github.com/RMSHE-MSH/LuminaFlow-for-CherryStudio) | AGPL-3.0 | CSS 变量组织结构 |
| CherryStudio-by-bilibili.css | Unknown | 主题概念与字体引用参考 |
| Hatsune Miku.css | Unknown | 变量组织概念参考 |

详见 [NOTICE](./NOTICE) 文件。

## 贡献

欢迎贡献代码、报告问题或提出建议！

## 致谢

- [Cherry Studio](https://github.com/CherryHQ/cherry-studio) - 优秀的 AI 客户端
- 所有参考项目的作者
- 社区贡献者

---
- 这是本人在 GitHub 上发布的第一个项目，尚处于学习与探索阶段。
- 如有任何问题或建议，欢迎通过 Issue 提出，非常感谢您的关注与指教！