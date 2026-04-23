# Project Profile

## 基本信息

- `workspace_root`: `/path/to/workspace`
- `workspace_slug`: `workspace-a1b2c3d4`
- `audit_target`: `checkout demo minimal-intrusion audit`
- `scope_summary`: `只审计 checkout demo 相关前端页面、后端接口和本地联调配置，不覆盖整个站点`
- `created_at`: `2026-04-23 12:00:00`
- `updated_at`: `2026-04-23 12:10:00`

## 仓库拓扑

- `repo_mode`: 多仓
- `in_scope_repos`:
  - `frontend/site`
  - `backend/gateway`
  - `deploy/local-debug`
- `out_of_scope_repos`:
  - `legacy-admin`
  - `mobile-app`
- `baseline_candidates`:
  - `origin/main`
  - `main`

## 目标边界

- `primary_paths`:
  - `frontend/site/src/features/checkout-demo`
  - `backend/gateway/api`
- `related_paths`:
  - `frontend/site/src/app/checkout-demo`
  - `deploy/local-debug`
- `do_not_touch_paths`:
  - `backend/**/etc/**`
  - `deploy/prod/**`
- `high_risk_shared_paths`:
  - `frontend/site/src/service/**`
  - `frontend/site/src/components/AppShell/**`

## 配置面识别

- `runtime_source_of_truth`:
  - `deploy/local-debug/*.yaml`
- `secondary_config_surfaces`:
  - `backend/**/etc/dev/*.yaml`
  - `backend/**/etc/test/*.yaml`
- `deployment_config_surfaces`:
  - `deploy/prod/**/*.yaml`
- `config_precedence`:
  1. `deploy/local-debug/*.yaml`
  2. `backend/**/etc/**/*.yaml`
  3. `deploy/prod/**/*.yaml`

## 生成规则

- `generated_files_or_patterns`:
  - `internal/handler/routes.go`
  - `internal/types/types.go`
  - `*.pb.go`
- `source_of_truth_files`:
  - `api/*.api`
  - `proto/*.proto`
- `generation_commands`:
  - `make api`
  - `make proto`
- `generation_doc_paths`:
  - `README.md`

## 用户可见暴露策略

- `vendor_exposure_policy`: `不允许第三方厂商名、provider 字段和内部错误直出到前端`
- `forbidden_user_visible_terms`:
  - `provider`
  - `internal_vendor`
- `internal_fields_not_for_frontend`:
  - `providerVoiceId`
  - `vendorBucketName`

## 风险分类

- `builtin_risk_types_enabled`:
  - 配置面误改
  - 生成文件误改
  - 高风险共享层改动
  - mock/live 污染
  - contract 漂移
  - 构建/环境风险
  - 用户可见信息泄漏
  - 可维护性/回滚风险
- `project_specific_risk_types`:
  - `公开演示链路污染`

## 审计偏好

- `language`: 简体中文
- `report_style`: 强模板
- `auto_subagent_enabled`: 是
- `default_compare_baseline`: 最近一次成功报告

## 已确认事实

- 本次只读审计，不改代码
- 当前目录是多仓聚合根
- 本地联调以 `deploy/local-debug` 为准

## 待确认项

- 是否需要纳入 `payment-rpc`

## 假设与保守处理规则

- 若 `payment-rpc` 未确认纳入，则只在跨仓引用命中时做旁路检查

## 已知冲突或歧义

- `backend/etc/dev` 与 `deploy/local-debug` 都有同名配置项，需以真实启动参数复核