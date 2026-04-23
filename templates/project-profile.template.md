# Project Profile

## 基本信息

- `workspace_root`:
- `workspace_slug`:
- `audit_target`:
- `scope_summary`:
- `created_at`:
- `updated_at`:

## 仓库拓扑

- `repo_mode`: 单仓 / 多仓 / 待确认
- `in_scope_repos`:
  - 
- `out_of_scope_repos`:
  - 
- `baseline_candidates`:
  - `origin/main`
  - `main`

## 目标边界

- `primary_paths`:
  - 
- `related_paths`:
  - 
- `do_not_touch_paths`:
  - 
- `high_risk_shared_paths`:
  - 

## 配置面识别

- `runtime_source_of_truth`:
  - 
- `secondary_config_surfaces`:
  - 
- `deployment_config_surfaces`:
  - 
- `config_precedence`:
  1. 
  2. 
  3. 

## 生成规则

- `generated_files_or_patterns`:
  - 
- `source_of_truth_files`:
  - 
- `generation_commands`:
  - 
- `generation_doc_paths`:
  - 

## 用户可见暴露策略

- `vendor_exposure_policy`:
- `forbidden_user_visible_terms`:
  - 
- `internal_fields_not_for_frontend`:
  - 

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
  - 

## 审计偏好

- `language`: 简体中文
- `report_style`: 强模板
- `auto_subagent_enabled`: 是 / 否 / 待确认
- `default_compare_baseline`: 最近一次成功报告

## 已确认事实

- 

## 待确认项

- 

## 假设与保守处理规则

- 

## 已知冲突或歧义

- 