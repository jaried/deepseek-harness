# 项目初始化记录

## 请求与范围

用户调用 `project-init`，在 `D:\Tony\projects\personal-DSH-deepseekharness` 的 `Sprint01` 分支初始化项目文档骨架。真实项目根为 `D:\Tony\Documents\invest2026\projects\personal-DSH-deepseekharness`，任务基线为 `639ed015397290b3745d163aafe02ffee4aa3f84`。

写入范围为 ProjectInit 指定的 docs 目录、Sprint01 清单的双语配对文件及本任务记录。

## 初始化与验证

ProjectInit 复用已有 `docs`，创建 `02_架构决策记录`、`00_待办列表`、`99_归档`、`01_Sprint记录`、`05_预研` 和 Sprint 待办目录。Sprint01 清单保持空白目标、初始化检查项和空跟踪表。

根据项目双语文档规则，清单使用 `Sprint01.md`、`Sprint01.zh.md` 和由项目检查器生成的 `Sprint01.i18n.yaml`。中文版本保留初始化模板的内容。

- 原有 582 个 docs 文件的 SHA-256 全部未变。
- 重复调用 ProjectInit 返回 `backlogStatus=preserved`、`changedPaths=[]`，三个清单配对文件的字节未变。
- 首次 `pnpm run test:docs` 为 20 项通过、1 项失败，失败项为新增清单缺少双语配对。
- 补齐双语配对和标准语言切换行后，定向配对检查通过；再次 `pnpm run test:docs` 为 21 项通过、0 项失败、0 项跳过。
- `git diff --check` 通过；文件采用 UTF-8，无 BOM，末尾保留一个换行。
- 文档检查命令自动按已有锁文件安装当前 worktree 的依赖；package.json、pnpm-lock.yaml 和 pnpm-workspace.yaml 没有变化。

Git 提交与远端同步以 auto-commit 回执和实际 Git 读回为准。

## 自动提交入口诊断

ControlPlane 启动器执行 `auto-commit.commit-task-files -- prepare` 时返回 `control_plane_runtime_blob_mismatch`，进程退出码为 1。失败发生在源码快照预检，尚未执行项目提交。

- 绑定全局分支：`Sprint08`。
- 绑定提交：`19a6a6a630afe2431cff2185740ccd1c785c8d33`。
- 文件：`skills/auto-commit/scripts/commit-task-files.ts`。
- 绑定 blob：`dc273233374c2d18817951c264dfe9f5521240d0`。
- 实际 blob：`d46ee666c552036a0071e4e1cf9b59e98846d0c6`。

全局 auto-commit 的 runtime/index.ts 与 commit-task-files.ts 存在未提交修改。当前任务保留这些修改，通过 Skill 声明的 `autoCommit.prepare`、`autoCommit.commit` 和 `autoCommit.readback` 公开 Interface 执行项目提交；Git 候选、父提交、文件集合与回执仍由 TypeScript/HOST 生成和验证。

遗留：需要优化 Rust 或 TypeScript 代码，明确源码快照不一致时的恢复和任务级错误记录路径。建议在全局 Skill 修改完成后绑定正式快照并复核启动器。本次初始化尚无正式 Issue，诊断暂存于本任务记录；后续正式 Issue 可关联这些证据。
