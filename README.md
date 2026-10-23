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

**方案 A**（2026-10-23 IA 改版）
- 侧栏：AI任务 · 任务明细 · 企微承接账号 · 看板 · 通话明细 · 系统说明（合并原外呼池/策略/意向池/任务监控；AI任务页顶部含可折叠「实时观察」）
- AI任务：新建含并发独占、任务时间、禁拨时段（21:00–09:00）、未接再呼、**线索分配比例**（公海池分层 A–E，合计100%）
- 任务明细：按任务切换客户列表；筛选项含意向待分配；**批量分配指定承接人**
- 企微承接：渠道活码式成员 + 组织架构弹窗；加微策略初始化**仅轮询**（昵称/邀请模版/欢迎语/失败重试）
- 看板布局：KPI → 图表 → 明细表；列表基础字段统一 **通话ID · 洋葱ID · 外呼手机号**；企微承接去掉「今日漏斗」Tab
- 任务「详情」抽屉 Tab：概览 / 拨打明细 / 失败重试 / 实时通话 / 操作日志
- 通话「总结」抽屉 Tab：转译 / AI通话总结 / 录音信息 / 回写字段

**方案 B**
- 任务「详情」→ 抽屉 Tab：概览 / 线索明细 / 失败重试 / 实时并发 / 日志
- 通话详情（recMask）：转译 / AI通话总结 / 修正意向 / **录音信息** / **回写CRM字段**
- 全局配置：外呼准入 / 频次与配额 / 时段与合规 / 渠道与并发 / **通道明细**
- 看板子 Tab：总览 / 通道 / 意向 / 明细
- 智能查询 · 个人信息 Tab 保持可切换

