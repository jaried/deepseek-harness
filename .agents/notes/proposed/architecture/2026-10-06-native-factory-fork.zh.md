# Agent Note: 宿主工厂分叉能力与调用所有权

Status: proposed

[English](2026-10-06-native-factory-fork.md) | 中文

## Problem

ordinary fork命令在factory识别原生所有权前已构造本地seed。原生driver需要精确完成边界与自己的持久target。

## Proposal

既有factory公开可选的caller-bound fork能力。command在本地正文/seed前委托，使用live header或一次persistence stat及直接workspace关联。错误保留已确认target和原native details；再次点击复用稳定意图。ordinary factory保持既有行为。

本方向已批准并绑定[ADR-001](<../../../../docs/02_架构决策记录/ADR-001_宿主工厂分叉能力与调用所有权.zh.md>)与[S1-02](<../../../../docs/01_Sprint记录/Sprint01/S1-02/S1-02_方案决策.zh.md>)。proposed生命周期如实表示实现和运行证据仍需后续取得。

## Alternatives considered

ordinary create内部的native Adapter接到已组成的本地seed。可选factory能力在既有slot确定所有权，同时保持ordinary分支。

## Acceptance criteria

native fork读取本地正文/snapshot/seed、compose/model/create均为零；claim前验证source和workspace，保留caller scope与错误，只返回实际发布handle。ordinary prefix、inbox、preset、cold source与subagent workspace assertion继续有效。

构建公开导出、NodeNext consumer、真实Loader和受影响文档检查取得真实证据。完整固定检查和迁移映射由[本票合同](<../../../../docs/01_Sprint记录/Sprint01/S1-02/S1-02_方案决策.zh.md>)持有。

## Risks

native效果产生后可能丢失回执。恢复读取原意图与target；已确认效果只补缺失的本地publication/attach。跨票集成由HOST负责。
