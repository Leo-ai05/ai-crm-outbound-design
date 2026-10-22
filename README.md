# AI外呼 × 武汉电销 CRM 设计包

面向 **洋葱学园 · 武汉电销系统（重洋启思电销系统 / WH_CRM_v2）** 的 AI 外呼结合方案，含两套可点击静态原型与系统说明。

## 打开方式（本地）

```bash
cd /Users/zhushengwu/Desktop/ai-crm-outbound-design
# 或 box 同步副本
cd /workspace/ai-crm-outbound-design

# 方式1：直接用浏览器打开
open index.html          # macOS
xdg-open index.html      # Linux

# 方式2：本地静态服务（可选）
python3 -m http.server 8765
# 浏览器访问 http://127.0.0.1:8765/
```

- Hub：`index.html` — A/B 对比入口、CRM 绑定要点、顶栏方案切换  
- 方案A：`scheme-a/index.html` — 独立板块 · AI外呼中心  
- 方案B：`scheme-b/index.html` — 客户池嵌合 · 四步向导  
- 文档：`docs/scheme-a-system.md` · `docs/scheme-b-system.md` · `docs/comparison.md`  

## 在线地址（部署后）

整包托管到 Axure 静态目录后访问：

```
https://axure.yc345.tv/platform/zhushengwu/ai-crm-outbound-design/
```

相对路径已按文件夹结构编写，总览 / 方案A / 方案B 顶栏可互相切换（本地 file:// 与在线同源均可用）。

> 原型内 mermaid 图使用 jsDelivr CDN；完全离线时请读 docs 中的 mermaid 源码。

## 参考输入（已吸收）

- `crm-refs/PRD-AI外呼机器人-CRM融合版.md`  
- `crm-refs/README-AI外呼CRM融合.md`  
- `crm-refs/PRD-CRM线索池私域筛选.md`  
- `crm-refs/PRD-企微承接额度.md`  
- `crm-refs/fusion-proto/`（Element Plus / pure-admin 视觉与客户池字段）  
- 外呼数据中心 `pages.yc345.tv/waihudata` 指标口径  

## 目录

```
ai-crm-outbound-design/
├── README.md
├── index.html
├── scheme-a/index.html
├── scheme-b/index.html
├── docs/
│   ├── scheme-a-system.md
│   ├── scheme-b-system.md
│   └── comparison.md
└── assets/          # 参考样式备份等
```

## 交互完善记录（2026-10-22）

### 全局方案切换导航

三页均增加 sticky 顶栏（`#001529` / `#409eff`）：**总览** · **方案A · 独立板块承接式** · **方案B · 深度绑定嵌合式**。方案页顶栏置于 CRM 侧栏之上，不替换侧栏。

### Tab / 详情抽屉（bindTabs 接线，无孤儿 data-tab）

**方案 A**
- 外呼策略 / 企微承接 / 意向池 / 看板：原有 Tab 保持；看板新增「明细导出」字段勾选；意向池新增「分配明细」
- 任务监控「详情」→ 抽屉 Tab：概览 / 拨打明细 / 失败重试 / 实时通话 / 操作日志
- 通话明细 / 意向「总结」→ 抽屉 Tab：转译 / AI通话总结 / 录音信息 / 回写字段
- 意向行操作：分配 + 总结 + 详情

**方案 B**
- 任务「详情」→ 抽屉 Tab：概览 / 线索明细 / 失败重试 / 实时并发 / 日志
- 通话详情（recMask）：转译 / AI通话总结 / 修正意向 / **录音信息** / **回写CRM字段**
- 全局配置：外呼准入 / 频次与配额 / 时段与合规 / 渠道与并发 / **通道明细**
- 看板子 Tab：总览 / 通道 / 意向 / 明细
- 智能查询 · 个人信息 Tab 保持可切换

