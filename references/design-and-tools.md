# 设计流程与可选工具

核对日期：2026-10-25。本文总结我们的设计工作方法；第三方工具链接用于按需接入，不随包分发其源码。版本、费用和许可证在实际采用时复查。

## 1. 先看真实产品

- 阅读目标项目的产品、技术栈、既有设计决策和当前用户授权；根目录配置了某个 registry 不代表业务项目使用该框架。
- 在真实浏览器查看桌面及手机的核心流程，记录最明显的三项问题：用户能否理解用途、找到主操作、成功完成任务。
- 写一个简短设计 brief：用户/场景、主要动作、页面内容、已有素材、功能边界与约束。使用真实产品截图和真实功能，不编数据、评价或合作关系。
- 对生成类工具，表单、校验、产物预览、下载/打印及移动端任务完成优先；对桌面软件，用实际运行截图说明价值。不要为使用设计工具额外添加无关装饰。

## 2. 先定方向，再实施

大幅改版且尚无已批准方向时，提供三个有明显区别的方向，使用同一份真实产品内容，同时展示桌面和手机首屏。差异来自信息结构、排版与产品展示方式，而非仅换主题色。小修或已经批准方向的延续无需重做探索。

实施前记录：

| 设计项 | 必须明确的内容 |
| --- | --- |
| 字体 | 正文/标题字体、字阶、字重、行高、回退字体、目标语言字符覆盖 |
| 颜色 | 背景/文字/边框/主动作/错误/成功 tokens 和对比度 |
| 布局 | 内容宽度、栅格、间距、断点和手机端重排 |
| 组件 | 默认、悬停、键盘焦点、禁用、加载、错误、成功、空状态 |
| 动效 | 使用理由、性能影响、减少动态效果的替代；不进入二维码与打印输出 |
| 产品资产 | 原始来源、许可证、是否允许商业使用及再分发、替代文本 |

React 项目可按需选 React 组件；原生 HTML/JS 项目保持其实现方式。不能为了组件库或动效迁移框架。

## 3. 可选的 Skill 分工

| 工具 | 什么时候选 | 产物与核验 |
| --- | --- | --- |
| [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | 设计系统或某个具体 UX 问题 | 产品/栈匹配的建议；检查命中内容后记录适用规则。上游 [MIT](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/blob/main/LICENSE)。 |
| [Claude Design](https://github.com/jiji262/claude-design-skill) | 有真实 brief 的方向探索或 HTML 原型 | 可见的多个方向与浏览器预览。上游 [MIT](https://github.com/jiji262/claude-design-skill/blob/main/LICENSE)；不同安装的本地改动不自动代表上游。 |
| [Web Interface Guidelines](https://github.com/vercel-labs/web-interface-guidelines) | 实现后审查交互和可访问性 | 有文件位置、用户影响的发现；自动审查不能替代真实操作。 |
| 哥飞 SEO 工具箱 / `gefei-seo-toolbox` | 需要实时选词或竞品证据 | 国家、语言、日期、来源、费用和限制清楚的数据记录；服务入口 [seo.web.cafe](https://seo.web.cafe/)，按现有账户授权和工具规则调用。不是本包内的开源依赖。 |
| `rankup` / 其他已装 SEO Skill | 项目已有对应调度或专项审查入口 | 补足当前缺口，避免重复调研及重复配置。未安装时先用本文流程，不静默下载任意来源。 |

只读取本次任务所需的 Skill。没有安装时可以按本流程完成工作；需要专有数据而无法获取时，保留未知，不用常识编数字。

## 4. MCP 与资源接入

### shadcn MCP + React Bits registry

[shadcn 官方 MCP](https://ui.shadcn.com/docs/mcp) 可读取 registry、搜索与查看组件。[React Bits 官方接入](https://reactbits.dev/get-started/mcp) 使用这个服务器。项目若已有 `components.json`，合并而非覆盖：

```json
{
  "registries": {
    "@react-bits": "https://reactbits.dev/r/{name}.json"
  }
}
```

本地接入曾以 `npx -y shadcn@4.22.1 mcp` 完成实际搜索测试。这是已核验的版本示例，不是“永远最新”或任意项目兼容保证。新的环境按官方客户端配置安装，并检查来源及所需执行权限；先只读搜索/查看，再决定是否安装组件。

[shadcn/ui 的许可证](https://github.com/shadcn-ui/ui/blob/main/LICENSE.md)为 MIT。**React Bits 当前许可证是 MIT 加 Commons Clause 条件**，限制组件/工具/部分导出物独立打包再分发；不能直接当作纯 MIT 组件合集收入本包。实际采用前读取[当前原文](https://github.com/DavidHDev/react-bits/blob/main/LICENSE.md)，本仓库仅链接接入方法。

### 外部服务与参考站

| 资源 | 使用方式 | 选择条件与边界 |
| --- | --- | --- |
| [Spline MCP](https://docs.spline.design/generate/plugins/chatgpt) | 官方托管服务器 `https://mcp.spline.design/mcp` | 可选外部服务，需要账户/OAuth，计划可能有限额。配置服务器后仍需授权和调用核验；仅在 3D 能解释产品时使用。 |
| [Frontify](https://help.frontify.com/en/articles/14787214-frontify-mcp) | 官方账户品牌资产 MCP | 有相应账户与品牌资产才引入；不是公共免费素材全集。 |
| [Fontshare](https://www.fontshare.com/) | 字体选择、授权后的 CSS | 成功请求字体 CSS，不代表所有字体许可相同或覆盖所有语言；不随包分发字体。 |
| [Noun Project API](https://api.thenounproject.com/getting_started.html) | 图标检索 | 需凭证并核对当前计划、具体资产许可；密钥不进浏览器代码。 |
| [Unsplash API](https://unsplash.com/documentation) | 需要照片的产品可检索 | 按当前 API 文档处理访问凭证、署名、热链和下载事件；不要为纯工具表单强加照片。 |
| [Blush](https://blush.design/license) | 授权插画 | 按资产和账户计划选择；不打包或转售素材库。 |
| [Coolors](https://coolors.co/) / [CTA Gallery](https://www.cta.gallery/) / [Shape of AI](https://www.shapeof.ai/) | 配色/操作层级/AI 交互的浏览参考 | 提炼原则并原创实现，不冒充已经连接的 API 或可复制的源码库。 |

工具状态分别写“发现入口 / 已配置 / 已授权 / 成功调用 / 已用于产品并验证”，并记录日期。配置存在不等于可用；可调用不等于设计已经改善。令牌及登录状态保存在本地合适的凭证位置，不随经验条目发布。

## 5. 实际验收与交付

- 浏览器检查真实桌面/手机布局、主流程、长文案、目标语言、错误/空/成功状态和横向溢出。
- 键盘完成核心任务，检查焦点、可见标签、错误关联、对比度及减少动态效果；按产品风险检查慢网/加载失败。
- 工具输出需单独验证：例如二维码的解码内容、静区、扫描与打印可用性不能由漂亮截图代替。
- 确认既有路由、SEO、分析、支付、登录与导出行为保留。列出做过的检查、发现及未验证项。
- 展示真实预览再依当前授权发布。安装工具的记录、设计方案、已部署效果是不同产物。

来源背景：[最初触发本次设计工具整理的帖子](https://x.com/yanliudreamer/status/2113188741452103685)。本文的实施流程来自项目自己的决策和核验，不转载帖子正文或第三方 Skill。
