# AGENTS.md — UniXNU-sm8250-common

## 职责

本仓库只放**多个 SM8250 板型共享**的内容：CPU 拓扑、控制器资源、共享平台操作、
SoC 级配置片段与补丁系列。板级连接、内存、保留区、固件、分区和电源策略属于设备仓库。

## 必读

- [选择与添加 SoC 支持](https://unixnu.com/zh/porting/soc-support)
- [设备树](https://unixnu.com/zh/porting/device-tree)
- [设备仓库规范](https://unixnu.com/zh/porting/device-repository)
- [组件目录](https://unixnu.com/zh/reference/components)
- [配置参考](https://unixnu.com/zh/reference/configuration)

## 规则

1. 硬件地址、中断号、控制器版本必须有来源（上游 DTS 提交或目标设备观测），
   写入时在注释里注明来源。
2. 不写未验证的 `CONFIG_XNU_*`：未知名称会被 defconfig 静默接受。
3. 可复用控制器代码进组件仓库，不进 `kits/`；`kits/` 只放 SoC 平台操作。
4. 改动同步：使用本仓库的设备仓库、README 的已验证设备表、中英文站点页面。
5. 提交前缀：`feat(<area>)`、`fix(<area>)`、`docs`、`build(<area>)`、`chore`。
