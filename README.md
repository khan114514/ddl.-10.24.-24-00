# 四题返修集中交接：492 / 505 / 776 / 783

> 当前优先适用[2026-10-22扩展豁免](handoff/CURRENT_REVIEW_POLICY.md)：保留此前五项，新增QA05/H02联网及外部查表约束、H03当前镜像选择/交付依据、H05当前调用证据，并汇总到QA17。所列事项无需整改或补跑；旧说明中相冲突的补证要求由本口径覆盖，其他核心要求继续处理。豁免不表示实跑完成。


更新：2026-10-22（Asia/Shanghai）。本仓库集中保存这四题的既有源码、返修进度、最新复核意见、证据和最新本地 AutoResearch Skill，便于统一接手。当前四题均有核心返修或待核项，尚未重新验收通过。

**接手从 [四题操作说明](START_HERE.md) 开始，使用 [统一接手 Prompt](TAKEOVER_PROMPT.txt)。**

新增文件：[完整豁免口径](handoff/CURRENT_REVIEW_POLICY.md) · [报告与判定示例](handoff/REPORTING_EXEMPTIONS.md) · [未填写的报告附录模板](handoff/REVIEW_POLICY_ADDENDUM_TEMPLATE.json)。四题目录各有 `CURRENT_REVIEW_POLICY.md`，说明如何覆盖旧返修意见。

| 题号 | 题目 | 当前材料入口 | 最新返修意见 |
|---|---|---|---|
| 492 | Distilled Decoding / DD | [源码与文本证据](auto0492/source/) · [完整包下载](DOWNLOADS.md) | [修改建议](auto0492/repair_plan.md) · [双独立报告](auto0492/qa/) |
| 505 | RF 时间步 / Taming Rectified Flow | [当前返修工作包](auto0505/package/) · [重建与执行手册](handoff/START_HERE.md) | [修改建议](auto0505/repair_plan.md) · [双独立报告](auto0505/qa_latest/) |
| 776 | OneDC 图像压缩 | [历史完整源码与原始证据](auto0776/source/onedc_v9/) · [接手手册](auto0776/START_HERE.md) | [修改建议](auto0776/repair_plan.md) · [双独立报告](auto0776/qa_latest/) |
| 783 | Bifrost-1 | [源码与文本证据](auto0783/source/) · [完整包下载](DOWNLOADS.md) | [修改建议](auto0783/repair_plan.md) · [双独立报告](auto0783/qa/) |

## 最新 Skill

五套主技能和必要辅助文件已随仓库上传，可直接从本仓库读取：

- [autoresearch](skills/autoresearch/SKILL.md)：三期任务工作流与路由。
- [autoresearch-manager](skills/autoresearch-manager/SKILL.md)：持续返修、证据与验收管理。
- [autoresearch-remote-cli](skills/autoresearch-remote-cli/SKILL.md)：授权远程执行与独立研究。
- [autoresearch-task-qa](skills/autoresearch-task-qa/SKILL.md)：只读内容质检。
- [autoresearch-baseline-quality](skills/autoresearch-baseline-quality/SKILL.md)：Baseline 合理性专项。

[V4 合同](skills/autoresearch/references/phase3-v4-contract.md)与 [2026-10-22 用户扩展豁免](handoff/CURRENT_REVIEW_POLICY.md)一起生效。五套已与本机当前安装版逐文件核对，导出差异及哈希见 [技能来源清单](handoff/SKILL_SNAPSHOT.json)。辅助 systematic-debugging 也保留。

本地规则已整合 V4，对应教程所称 0.3.10；**本仓库没有真实官方 0.3.10 发布包及独立格式/GPU/指纹工具**。随附旧工具保留实际身份，不能重命名冒充新版。详见 [工具版本](handoff/SKILL_VERSIONS.md)。

## 完整性与资产

```bash
python3 release_tools/verify_handoff.py --restore-empty-dirs
python3 auto0776/tools/verify_handoff.py
```

两项仅核验交接文件与已有原始证据，不代表 GPU、Harbor 或最终题目 QA 通过。

DD/Bifrost 的完整大包已在原仓库 Release 发布，本仓库集中提供 [精确下载链接、大小与 SHA256](DOWNLOADS.md)，源码与报告可在这里直接浏览。RF/OneDC 的专家工作副本已经在本仓库；未包含的大模型权重、网盘恢复位置和获取要求见对应部署/资产说明。不要把 `git clone` 成功当成已取得全部运行资产。

原始报告、旧分数和暂停状态保留。此次是集中交接，没有新启动训练、双轨研究或平台提交；最终交付仍须基于真实修复和同一完整 ZIP 的双独立质检。
