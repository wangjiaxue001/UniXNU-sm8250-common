# UniXNU-sm8250-common

Qualcomm SM8250（kona）的共享硬件描述与平台操作，供 SM8250 板型复用。

## 范围

- `soc.toml`：SoC 标识、硬件数据来源、已核对组件的规范 ID
- `dts/sm8250.dtsi`：共享硬件描述（板级 DTS include 此文件）
- `configs/sm8250.config`：SoC 级内核配置片段
- `patches/xnu/series`：SoC 级 XNU 补丁序列（当前为空）
- `kits/`：共享平台操作，按构建配置接入源码或静态库

## 输入

板型需要提供自己的内存、保留区、外设连线、固件选择和电源策略。
寄存器地址一律取自目标设备，不在此仓库推断。

## 已验证设备

| 设备 | SoC | 结果 |
| --- | --- | --- |
| — | — | 尚无已验证板型 |

在此表出现真机结果之前，本仓库的硬件值仅代表来源设备上的观测，不代表通用正确性。

## 待完成

1. `dts/sm8250.dtsi` 现有 cpus／psci／GIC（`intc`）／UFS 主机（`ufshc`）。
   usb、i2c/spi、mdss、pdc、rpmh 按[驱动适配顺序](https://unixnu.com/zh/porting/drivers)
   逐项追加，每项都要带 `unixnu,adt-name` 才进 ADT。
2. **UFS 组件不匹配**：本仓 UFS 节点用原厂 `compatible = "qcom,ufshc"`，而 ShengUfs 的
   `IONameMatch` 是 `qcom,sm8550-ufshc`。二者不会绑定，需要扩展该 personality
   （或改用它能识别的名字），属于组件侧改动，需单独审核。
3. `timebase-frequency = <19200000>` 是 SM8250 架构常量（原厂 DT 不提供），待真机核对。
4. `soc.toml` 的 `source_revision` 需替换为已审查提交。
5. `configs/sm8250.config` 保持为空，直到某项设置在 SM8250 上真机验证。
6. 首个板型（`cmi`）bring-up 后，把共享部分回填到这里并更新已验证设备表。

## 文档

- [选择与添加 SoC 支持](https://unixnu.com/zh/porting/soc-support)
- [设备仓库](https://unixnu.com/zh/porting/device-repository)
- [设备树](https://unixnu.com/zh/porting/device-tree)
