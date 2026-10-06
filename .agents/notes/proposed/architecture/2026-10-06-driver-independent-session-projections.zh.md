# Agent Note: 共享会话投影定义与独立驱动器

Status: proposed

[English](2026-10-06-driver-independent-session-projections.md) | 中文

## Problem

默认agent loop（智能体循环）定义inbox与turnBoundary投影。独立原生driver需要相同持久显示语义，并保持自己的执行范围和单一定义owner。

## Proposal

既有core/agent包通过一个session-projections叶目录公开纯定义。两个driver消费同一定义；具体Inbox命令由各driver执行。keys、stateVersion、fold、wire编码和持久错误保持；兼容导出指向同一定义。

本方向已批准并绑定[ADR-002](<../../../../docs/02_架构决策记录/ADR-002_共享会话投影定义与独立驱动器.zh.md>)与[S1-01](<../../../../docs/01_Sprint记录/Sprint01/S1-01/S1-01_方案决策.zh.md>)。proposed生命周期如实表示实现和运行证据仍需后续取得。

## Alternatives considered

导入整个默认loop扩大依赖与执行范围；复制定义产生两个持久语义owner。叶能力保持单一owner，只公开所需定义。

## Acceptance criteria

旧driver与独立driver对最小事件流产生相同fold与wire值。保持inbox版本1、turnBoundary版本2及非法splice错误；import/register时loop/factory/model/tool/process/remote均为零。

构建公开导出、NodeNext consumer、真实Loader和受影响文档检查取得真实证据。完整固定检查和迁移映射由[本票合同](<../../../../docs/01_Sprint记录/Sprint01/S1-01/S1-01_方案决策.zh.md>)持有。

## Risks

兼容导出与包叶产物可能漂移。build、pack、installed export与依赖闭包检查验证真实consumer。原生driver仍需自己的完整Agent/Inbox实现。
