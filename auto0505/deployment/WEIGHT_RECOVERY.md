# RF 冻结权重恢复入口（2026-10-22）

本轮未找到原权重在本机的可用副本，也未核验任何H20挂载目录。以下是可恢复相同字节资产的上游固定版本下载入口；不要把示例落盘目录当成已经挂载。

19个文件全部与 `runtime-image/weight_manifest.json` 的原冻结SHA256一致：4个大模型用实时Hub LFS SHA256元数据核对，其他文件按可用的LFS元数据或实际小文件下载计算SHA256。未下载四个大模型，也未做模型加载/GPU复验。原始逐项记录在 [rf_weight_sources.json](rf_weight_sources.json)。总计35,377,948,947字节。

| 落盘相对路径 | 固定版本下载 | 字节 | SHA256 |
|---|---|---:|---|
| `flux-dev/flux1-dev.safetensors` | [black-forest-labs/FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev/resolve/3de623fc3c33e44ffbe2bad470d0f45bccf2eb21/flux1-dev.safetensors) | 23802932552 | `4610115bb0c89560703c892c59ac2742fa821e60ef5871b33493ba544683abd7` |
| `flux-schnell/ae.safetensors` | [black-forest-labs/FLUX.1-schnell](https://huggingface.co/black-forest-labs/FLUX.1-schnell/resolve/741f7c3ce8b383c54771c7003378a50191e9efe9/ae.safetensors) | 335304388 | `afc8e28272cd15db3919bacdb6918ce9c1ed22e96cb12c4d5ed0fba823529e38` |
| `t5-encoder-bf16/model.safetensors` | [city96/t5-v1_1-xxl-encoder-bf16](https://huggingface.co/city96/t5-v1_1-xxl-encoder-bf16/resolve/1b9c856aadb864af93c1dcdc226c2774fa67bc86/model.safetensors) | 9524648592 | `565cb2487351282e8e4dbeb88e63f4ad28217ce0439f5a8e6525a924807d2d9b` |
| `clip-vit-l14/model.safetensors` | [openai/clip-vit-large-patch14](https://huggingface.co/openai/clip-vit-large-patch14/resolve/32bd64288804d66eefd0ccbe215aa642df71cc41/model.safetensors) | 1710540580 | `a2bf730a0c7debf160f7a6b50b3aaf3703e7e88ac73de7a314903141db026dcb` |

## 在接手主机恢复

在独立下载环境使用HF CLI，保留任务数值运行时的冻结依赖。FLUX两个仓库标记为gated，下载需要已有相应访问权限的HF登录；本交接未代用户申请或接受许可，脚本/仓库不含token。T5使用与原哈希一致的 `city96/t5-v1_1-xxl-encoder-bf16`，不要改成44GB的完整Google T5或其他精度/分片版本。

下面的 `/data/rfsteps/weights` 只是建议的恢复位置，需按实际持久盘修改。

```bash
RF_ASSET_ROOT=/data/rfsteps/weights
mkdir -p "$RF_ASSET_ROOT"
hf download black-forest-labs/FLUX.1-dev flux1-dev.safetensors --revision 3de623fc3c33e44ffbe2bad470d0f45bccf2eb21 --local-dir "$RF_ASSET_ROOT/flux-dev"
hf download black-forest-labs/FLUX.1-schnell ae.safetensors --revision 741f7c3ce8b383c54771c7003378a50191e9efe9 --local-dir "$RF_ASSET_ROOT/flux-schnell"
hf download city96/t5-v1_1-xxl-encoder-bf16 model.safetensors .gitattributes README.md config.json special_tokens_map.json spiece.model tokenizer_config.json --revision 1b9c856aadb864af93c1dcdc226c2774fa67bc86 --local-dir "$RF_ASSET_ROOT/t5-encoder-bf16"
hf download openai/clip-vit-large-patch14 model.safetensors .gitattributes README.md config.json merges.txt preprocessor_config.json special_tokens_map.json tokenizer.json tokenizer_config.json vocab.json --revision 32bd64288804d66eefd0ccbe215aa642df71cc41 --local-dir "$RF_ASSET_ROOT/clip-vit-l14"
```

完成后从仓库根执行原校验/准备入口：

```bash
python3 auto0505/deployment/prepare_weights.py --source "$RF_ASSET_ROOT"
```

prepare_weights.py会校验全部19个文件，再拷贝到可信构建context；不修改原数值协议/锚点，不通过候选artifacts移交权重。H20路径、空间、下载权限和真实模型加载由执行session核实；此清单不代表已下载/已挂载或平台验收通过。
