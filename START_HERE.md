# 四题统一接手说明

> 当前优先适用[2026-10-22扩展豁免](handoff/CURRENT_REVIEW_POLICY.md)：保留此前五项，新增QA05/H02联网及外部查表约束、H03当前镜像选择/交付依据、H05当前调用证据，并汇总到QA17。所列事项无需整改或补跑；旧说明中相冲突的补证要求由本口径覆盖，其他核心要求继续处理。豁免不表示实跑完成。


本次把既有工作集中到一个仓库，不重新认领题目。先读 [当前规则](handoff/CURRENT_REVIEW_POLICY.md)、[V4 合同](skills/autoresearch/references/phase3-v4-contract.md)，再核对 [四题状态清单](handoff/FOUR_TASKS.json)。四题最新静态复核均为 NOT_READY；不要把交接完整性通过当作题目 PASS。

## 492 / DD

入口：`auto0492/source/dd_v5_0_3_recovery_20261006/`。大模型、数据与完整原 ZIP 按 [下载说明](DOWNLOADS.md)获取；`source_manifest.json` 说明源码视图与完整附件的关系。

优先读 [修改建议](auto0492/repair_plan.md) 和 `auto0492/qa/`：当前 Public Reference 归一化约 0.91093，超过当前 0.8 上限；成对随机性/重复协议、完整模型重载和合法双轨有效时长需据实闭环。不得削弱 B、倒调 U、剪裁分数或把模型重载伪装成独立训练。执行拓扑需迁移到单 sandbox 单容器、自身 GPU，移除 Compose、外部 GPU/SSH 和不支持的 storage/network 声明；完整单轮预算覆盖训练、重载和评分。

## 505 / RF 时间步

入口：`auto0505/package/`，当前 `3.5.0-a100-repair`；保留已经完成的本地修复和验证。`handoff/START_HERE.md`、`handoff/REPAIR_MATRIX.md` 和 `auto0505/tools/` 提供原运行时编辑源与可重复组装步骤。组装前先把新增改动回写生成源，不能误用初始化脚本清空真实新轨迹。

最新意见：`auto0505/repair_plan.md`、`auto0505/qa_latest/`。当前上传版本轨迹仍为空；旧 Seed 访问过参考材料，不能作为干净轨迹。需处理题面允许重复节点而积分器存在除零路径的边界问题，补可操作的镜像/权重入口，并完成真实 GPU/Harbor 链路和干净双轨。已完成的 CPU/权限测试不改标为 FLUX 实跑。A100 是该题历史人类授权，H20/L20 迁移补证按放宽口径单列。

## 776 / OneDC

入口：`auto0776/START_HERE.md` 和 `auto0776/source/onedc_v9/`。六份正式原始评分日志、59 轮审计材料与资产恢复说明已保留。先运行该题的 `tools/verify_handoff.py`，复制历史源码至新作者工作目录后再改。

最新意见：`auto0776/repair_plan.md`、`auto0776/qa_latest/`。成对方法改善与码率门已有可复算依据，勿无条件重跑。核心是运行拓扑/资产可获取性、真实独立研究时长和轨迹整理：合格历史窗口上界约 5.14/5.23h，旧 14h 口径不能直接沿用。每轮恰八字段、连续真实映射，区分模型失败与控制器采纳；只补实际缺口，不补造轮次或日志。

## 783 / Bifrost

入口：`auto0783/source/`，含旧 `Task/`、`Runtime/` 及 workspace 适配；完整原包按下载说明取得。先看 `auto0783/repair_plan.md`、`auto0783/qa/`。

正式成对推理记录和改善可复算；核心返修是单容器自身 GPU、移除 broker/远程工作容器，区分有效 Hard Gate 与格式/超时/基础设施异常，补当前 Reference 的 Public/Dev 原始结果并规范轨迹、唯一最终方法。两位审查者对七小时例外充分性有分歧：先整理现有证据闭环，不直接要求盲目跑满十小时，不把未确认时长填成已通过。

## 通用交付与工具

最新主 Skill 统一在顶层 `skills/`。`auto0776/skills/` 是保留的题内可移植副本，根技能为当前主入口；具体导出哈希见 `handoff/SKILL_SNAPSHOT.json`。所有原始报告及其结论保持原样；五项放宽不足可后补，其他核心问题继续处理。

完整官方 0.3.10 发布包、独立格式/GPU/指纹脚本尚缺，不能由本仓库生成。实际拿到后记录来源、版本和哈希，按真实 CLI 运行。打包工具只打包和算 SHA，不授予 PASS。最终报告在被审 ZIP 外，两个独立审查绑定同一 ZIP；之后修改包则如实记录新版本。正式平台验收、长实验、12h 稳定性都必须有真实记录。

本仓库所做的新验证仅限交接清单、已存在证据关联、最新技能快照和远端发布完整性。没有新开展模型实验或替代任何动态验收。
