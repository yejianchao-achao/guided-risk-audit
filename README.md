# Guided Risk Audit

`guided-risk-audit` 是一个面向 Codex 的显式调用 skill，用于先半自动建立项目画像，再执行只读风险审计与复跑对比。

## 能力概览

- 半自动建档：先扫描仓库，再只追问少量高影响问题
- 只读审计：不改代码、不生成 patch、不提交 commit
- 结构化输出：按固定模板输出风险结论，不走自由摘要
- 复跑对比：复用项目画像，并和上一次成功报告比较
- 自动分片：大范围多仓审计时，可自动进入只读子 agent 分片模式

## 适用场景

- 最小侵入审计
- demo/mock 污染审计
- 配置面误改审计
- 高风险共享层越界审计
- 二次复审与报告对比

## 安装

将整个仓库放到 Codex 的 skills 目录下：

```bash
git clone https://github.com/yejianchao-achao/guided-risk-audit.git "${CODEX_HOME:-$HOME/.codex}/skills/guided-risk-audit"
```

如果已经存在同名目录，先备份或删除旧目录，再重新拉取。

## 调用方式

这个 skill 只在显式点名时触发，例如：

- `使用 guided-risk-audit skill，审计当前目录的最小侵入风险`
- `使用 guided-risk-audit skill，先建项目画像，再做只读风险审计`
- `使用 guided-risk-audit skill，重跑并和上次报告比较`

## 运行模式

- `bootstrap`：扫描工作区，生成项目画像草稿，最多追问 5 轮
- `audit`：基于画像执行只读风险审计
- `rerun`：基于画像复跑，并与最近一次成功报告或用户指定报告对比

## 默认行为

- 当前目录优先，但允许显式指定路径
- 只读，不修改文件
- 当前环境允许时，大范围多仓审计会自动开启只读子 agent 分片
- 报告和项目画像都写入本地状态目录，不污染项目仓库

默认状态目录：

```text
${CODEX_HOME:-~/.codex}/state/guided-risk-audit/<workspace-slug>/
```

其中默认包含：

- `project-profile.md`
- `reports/latest.md`
- `reports/YYYY-MM-DD-HHMMSS.md`

## 仓库结构

```text
.
├── SKILL.md
├── templates/
│   ├── bootstrap-questions.md
│   ├── project-profile.template.md
│   └── report.template.md
├── references/
│   └── risk-taxonomy.md
└── examples/
    └── project-profile.example.md
```

## 核心设计原则

- 显式调用，避免误触发
- 先建画像，再审计
- 证据优先，证据不足标记为 `待确认`
- 相对主线改动和本地未提交改动必须分开看
- 生成文件问题必须回溯源文件和生成命令
- 配置问题必须先识别真实生效面

## 分享建议

这是一个纯 Markdown 技能包，不依赖额外脚本。复制整个目录即可分发。

如果新安装的 skill 没有立刻出现在会话可用技能列表里，重新打开一个新会话通常更稳。
