# Agent Note: Native factory fork before local history

Status: proposed

English | [中文](2026-10-06-native-factory-fork.zh.md)

## Problem

The ordinary fork command constructs a local seed before the factory can identify native ownership. The native driver needs the exact completed boundary and its own persistent target.

## Proposal

The existing factory exposes an optional caller-bound fork capability. The command delegates before local body/seed work, using a live header or one persistence stat and direct workspace membership. Errors preserve the confirmed target and original native details. One stable intent survives repeated clicks. An ordinary factory retains its existing behavior.

This direction is approved for [ADR-001](<../../../../docs/02_架构决策记录/ADR-001_宿主工厂分叉能力与调用所有权.md>) and [S1-02](<../../../../docs/01_Sprint记录/Sprint01/S1-02/S1-02_方案决策.md>). The proposed lifecycle records that implementation and runtime evidence remain future work.

## Alternatives considered

A native adapter inside ordinary create receives an already composed local seed. The optional factory capability places ownership at the existing factory slot while preserving the ordinary branch.

## Acceptance criteria

Native fork performs zero local body/snapshot/seed/compose/model/create work, validates source and workspace before claim, preserves caller scope and errors, and returns the actually published handle. Ordinary prefix, inbox, preset, cold-source and subagent-workspace assertions remain effective.

Built exports, NodeNext consumers, actual Loader tests and affected documentation checks provide real evidence. The full fixed checks and migration mapping remain in [the Issue contract](<../../../../docs/01_Sprint记录/Sprint01/S1-02/S1-02_方案决策.md>).

## Risks

A reply may be lost after native effect. Recovery reads the original intent and target; a confirmed effect permits only missing local publication/attach work. Cross-Issue integration remains with HOST.
