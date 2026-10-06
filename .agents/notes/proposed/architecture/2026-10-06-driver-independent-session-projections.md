# Agent Note: Driver-independent session projection definitions

Status: proposed

English | [中文](2026-10-06-driver-independent-session-projections.zh.md)

## Problem

The default agent loop defines inbox and turn-boundary projections. An independent native driver needs the same durable display semantics without loading that model loop or duplicating its definitions.

## Proposal

The existing core/agent package exports the pure definitions from one session-projections leaf directory. Both drivers consume the same definitions; concrete Inbox commands stay with each driver. Keys, state versions, folds, wire encoding and durable errors remain unchanged. Compatibility exports point to the same definitions.

This direction is approved for [ADR-002](<../../../../docs/02_架构决策记录/ADR-002_共享会话投影定义与独立驱动器.md>) and [S1-01](<../../../../docs/01_Sprint记录/Sprint01/S1-01/S1-01_方案决策.md>). The proposed lifecycle records that implementation and runtime evidence remain future work.

## Alternatives considered

Importing the entire default loop expands dependencies and execution; copying definitions gives durable semantics two owners. The leaf capability keeps one owner and exposes only requested definitions.

## Acceptance criteria

The old and independent drivers produce identical folds and wire values for the minimal event stream. Inbox version 1 and turnBoundary version 2 and invalid-splice errors remain. Import/register performs zero loop/factory/model/tool/process/remote work.

Built exports, NodeNext consumers, actual Loader tests and affected documentation checks provide real evidence. The full fixed checks and migration mapping remain in [the Issue contract](<../../../../docs/01_Sprint记录/Sprint01/S1-01/S1-01_方案决策.md>).

## Risks

Compatibility exports and package leaf outputs can drift. Build, pack, installed-export and dependency-closure checks verify the actual consumer. The native driver still owes its own complete Agent/Inbox implementation.
