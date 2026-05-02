# 宠物急救分诊与到院前协同平台

GitHub 仓库：`https://github.com/puY123610/-sos.git`

这是一个宠物急救分诊、医院联系、导航和到院前协同平台。它不是 AI 宠物医生，不提供诊断、开药、剂量或安全承诺。

## 当前状态

当前阶段是工程骨架阶段。

已经存在：

- TypeScript monorepo 目录边界：`apps/`、`services/`、`packages/`。
- 小程序优先的用户端骨架：`apps/miniapp/`。
- 医院后台、运营后台、后端 API 和共享包占位目录。
- workspace 占位配置：`package.json`、`pnpm-workspace.yaml`。
- 环境变量样例：`.env.example`。
- AI/Codex 长期协作规则：`AGENTS.md`。

尚未存在：

- 可运行微信小程序工程。
- Taro、NestJS、Next.js、Prisma 初始化工程。
- 页面、组件、接口、数据库模型或业务函数。
- 依赖安装、测试脚本、构建脚本或 CI 实现。

在 Owner 明确批准进入可运行开发阶段前，本仓库只维护工程骨架和文档，不写业务实现。

## 产品定位

MVP 要帮助宠物主人在紧急情况下尽快完成：

1. 点击首页大 SOS 按钮。
2. 回答尽量少的问题。
3. 系统补充联系方式、定位、宠物档案和提交时间。
4. 系统把 SOS 信息发送到医院后台。
5. 医生通过电话指导紧急措施。
6. 平台沉淀结构化、可授权、可脱敏的数据。

用户端不展示红黄绿风险等级；后台可以保留红旗标记，用于医院优先处理和安全兜底。

## 技术方向

正式进入工程实现后，采用一个 TypeScript monorepo：

- 小程序/H5：Taro + React + TypeScript。
- 医院后台：Next.js + React + TypeScript。
- 运营后台：Next.js + React + TypeScript。
- 后端 API：NestJS + TypeScript。
- 数据库：PostgreSQL。
- ORM：Prisma。
- 地图供应商：高德地图。
- AI：只做后端抽象，MVP 默认关闭。

MVP 阶段不得擅自引入 Python、Java、Go、Rust、原生 iOS 或原生 Android。

## 目录结构

```text
.
├── README.md                    # GitHub 项目首页，给人看的项目说明
├── AGENTS.md                    # 给 Codex/AI agent 看的长期规则
├── 计划模板.md                   # 复杂任务计划模板
├── 更新记录.md                   # 文档、骨架和后续功能变更记录
├── .env.example                 # 环境变量样例，只放占位值
├── apps/                        # 前端应用骨架
│   ├── miniapp/                 # 小程序优先用户端骨架
│   ├── hospital-admin/          # 医院后台骨架
│   └── ops-admin/               # 运营后台骨架
├── services/
│   └── api/                     # 后端 API 骨架
├── packages/                    # 共享包骨架
│   ├── shared-types/
│   ├── api-client/
│   ├── safety-rules/
│   └── config/
└── docs/
    ├── 架构说明.md
    ├── 接口文档.md
    ├── 安全要求.md
    └── 分支与回滚.md
```

各子目录内的 `说明.md` 只说明模块边界，不代表已有实现。

## 文档入口

建议按以下顺序阅读：

1. `README.md`
2. `AGENTS.md`
3. `docs/架构说明.md`
4. `docs/接口文档.md`
5. `docs/安全要求.md`
6. `docs/分支与回滚.md`
7. `计划模板.md`
8. `更新记录.md`
9. `/Users/jack/Desktop/pet.md`

## 如何进入开发

当前还没有启动、测试或构建命令，因为 `package.json` 尚未定义 `scripts`。

进入可运行开发阶段前，需要 Owner 明确批准：

- 是否开始初始化 `apps/miniapp` 的 Taro + React + TypeScript 工程。
- 是否同步初始化 `services/api` 的 NestJS 工程。
- 是否同步初始化医院后台和运营后台。
- 是否开始安装依赖。
- 首批真实医院数据来源和校验方式。

建议第一批工程任务只补齐工程地基：pnpm workspace、strict TypeScript、lint、typecheck、test、build 和 CI。

## 医疗安全边界

系统不得：

- 诊断疾病。
- 开药。
- 提供药物剂量。
- 承诺安全或治愈。
- 建议红旗症状下延迟就医。
- 让 AI 替代医生指导急救。

系统可以：

- 收集结构化急救信息。
- 把 SOS 信息发送给医院后台。
- 支持医生回拨和处理记录。
- 生成病例摘要。
- 在后台保留红旗标记。
- 为后续授权、脱敏后的 AI 训练沉淀数据。

## 文档命名规则

保留英文文件名的例外：

- `README.md`
- `AGENTS.md`
- `.env.example`
- 必要工具配置文件

除此之外，新增 Markdown 文档必须使用中文文件名，内容也默认使用中文。新增英文命名文档前必须先得到 Owner 明确批准。
