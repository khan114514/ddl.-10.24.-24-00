# 完整大包下载与恢复

本仓库上传可浏览源码、配置、文本证据、四题复核和 Skill。DD/Bifrost 完整附件保留在已经核验的原 Release；这里提供唯一对应的链接，未在本仓库重复上传这些大文件。以下附件是历史/复核输入，不是新通过的返修提交。

| 题目 / 附件 | 字节数 | SHA256 |
|---|---:|---|
| [auto0492-dd-complete.zip.001](https://github.com/khan114514/7-others/releases/download/review-2026-10-22/auto0492-dd-complete.zip.001) | 1900000000 | `99638f957ed3398224accd40c91db80288590e811a4d48c1719772f0fdbd1852` |
| [auto0492-dd-complete.zip.002](https://github.com/khan114514/7-others/releases/download/review-2026-10-22/auto0492-dd-complete.zip.002) | 1900000000 | `3c26773e445be712c51f086c10111e308e66ba8e8136ffe0e3604ca6ff486391` |
| [auto0492-dd-complete.zip.003](https://github.com/khan114514/7-others/releases/download/review-2026-10-22/auto0492-dd-complete.zip.003) | 1846534682 | `fc9f6edf2d58abda4bc448af0ddd583e809e2cbf5ac7b34bffec6c6a8025b12c` |
| [auto0783-complete.zip](https://github.com/khan114514/7-others/releases/download/review-2026-10-22/auto0783-complete.zip) | 814694203 | `c97e90c1e23768b61b992fa0b03b0894a4a7d425b33bafe077160ff911aa2e3c` |

下载后先核对各分卷的大小和 SHA256。DD 在同一目录执行：

```bash
cat auto0492-dd-complete.zip.001 auto0492-dd-complete.zip.002 auto0492-dd-complete.zip.003 > auto0492-dd-complete.zip
shasum -a 256 auto0492-dd-complete.zip
```

完整 DD ZIP SHA256：`4f3ed4b5164bfd052d9e699da6b47726450fe1cd0dac3af65896732295ebb096`；完整 Bifrost ZIP SHA256：`c97e90c1e23768b61b992fa0b03b0894a4a7d425b33bafe077160ff911aa2e3c`。分卷总计 5,646,534,682 字节；Bifrost 为 814,694,203 字节。

上述完整附件此前已从 GitHub 远端核对大小/哈希，原记录保存在 `handoff/upstream/release_verification.json`，本次另做链接可用性核验，不把旧核验改写成新下载记录。

RF 当前工作包直接在 `auto0505/package/`，依赖和19文件权重清单在 `auto0505/deployment/`；精确大权重不在 Git 中，需要接手者按部署说明校验并提供。

OneDC 历史源码和六份正式原始日志在 `auto0776/source/onedc_v9/`；大资产/旧环境的百度网盘目录、包名、大小、SHA256 和恢复办法见 [资产恢复](auto0776/assets/RECOVERY.md)。网盘备份存在不等于已解包核验当前运行环境。

只把本仓库当专家材料，不整体交给解题 Actor。Hidden 准备按对应私有路径/安全入口完成。

## RF新增可恢复下载源（2026-10-22）

四个大权重及15个配套文件已逐项找到与原冻结SHA256一致的固定版本来源，见 [RF权重恢复](auto0505/deployment/WEIGHT_RECOVERY.md) 和 [19文件源映射](auto0505/deployment/rf_weight_sources.json)。这是下载来源核验，不是大模型已下载或H20已挂载。OneDC资产包已在网盘主窗口确认可见，并于本次对话生成七天有效分享入口，链接和提取码在对话中单独交付；该私有分享链接不写入公开仓库。下载后仍须校验归档清单中的字节数与SHA256。

## Bifrost现存分片核验（2026-10-22）

在用户指定的既有存储上找到六个完整checkpoint分片，逐字节SHA256与题包冻结清单全部一致，共29,663,264,600字节；具体主机和目录在本次用户对话单独交付。[本次校验记录](handoff/verification/bifrost_recovered_shards_verified.json)仅确认原分片字节，不表示已恢复完整模型目录、张量准备/GPU运行或目标平台验收。不要使用同目录的 `.partial-*` 文件。
