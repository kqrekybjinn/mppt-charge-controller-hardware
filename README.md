# RT-Thread MPPT Power Node Hardware

本仓库整理“基于 Linux + RT-Thread AMP 混合架构的户外光伏自供能智能监测终端”中的 PCB-02 光伏 MPPT 功率控制节点硬件资料，包含原理图 PDF、Gerber/钻孔生产文件和开源发布说明。

## 项目定位

该硬件面向全国大学生嵌入式芯片与系统设计竞赛芯片应用赛道的自主选题方向，是户外光伏自供能智能监测终端的能源侧实时控制节点。板上 STM32G474RET6 运行 RT-Thread，负责光伏输入到电池/直流母线的 DC-DC 转换、MPPT/CC-CV 充电控制、双 INA226 电压电流采样、CAN 通信、温度/风扇/使能/故障等本地实时控制任务。

在整机架构中，Linux 侧负责数据存储、联网、MQTT 网关、语音助手、后台页面和人机交互；RT-Thread 侧负责电源采样、充电控制、故障处理和硬实时保护。本仓库公开的是其中 MPPT 功率控制节点的硬件资料。

当前公开资料更适合用于：

- 查看电路原理和接口定义。
- 复核功率路径、采样路径和控制接口。
- 交给 PCB 厂进行打样前检查。
- 作为 STM32G474 + RT-Thread MPPT 固件和整机能源管理系统的硬件参考。

当前公开资料还不等同于完整 EDA 源工程，因为压缩包内主要是 Gerber/Drill 生产文件，不包含可编辑原理图/PCB 工程源文件。后续可继续补充 EDA 源工程、BOM、贴片坐标和固件仓库链接。

## 目录结构

```text
.
├── README.md
├── LICENSE
├── docs/
│   ├── HARDWARE_OVERVIEW.md
│   ├── INTERFACES.md
│   ├── OPEN_SOURCE_CHECKLIST.md
│   ├── DESIGN_NOTES.md
│   ├── images/
│   │   └── MPPT-schematic-1.png
│   └── release-notes/
│       └── v0.1.0.md
├── hardware/
│   ├── fabrication/
│   │   └── MPPT-gerber-drill-fabrication.zip
│   ├── gerber/
│   │   └── extracted/
│   └── schematic/
│       └── MPPT-schematic.pdf
└── LICENSE_OPTIONS.md
```

## 主要文件

| 文件 | 说明 |
| --- | --- |
| `hardware/schematic/MPPT-schematic.pdf` | 原理图 PDF，一页 |
| `docs/images/MPPT-schematic-1.png` | 原理图预览图，仅用于 README/网页浏览 |
| `hardware/fabrication/MPPT-gerber-drill-fabrication.zip` | 原始 Gerber/Drill 打包文件 |
| `hardware/gerber/extracted/` | 已解压的 Gerber、钻孔和飞针测试文件 |
| `docs/HARDWARE_OVERVIEW.md` | 硬件功能概览 |
| `docs/INTERFACES.md` | 接口和信号说明 |
| `docs/DESIGN_NOTES.md` | 设计说明与发布边界 |
| `docs/OPEN_SOURCE_CHECKLIST.md` | 上传开源前检查清单 |
| `docs/REPOSITORY_SETUP.md` | 新建 Git 仓库和推送命令 |

## 原理图预览

![MPPT schematic](docs/images/MPPT-schematic-1.png)

如果预览图中文字或符号显示异常，请以 `hardware/schematic/MPPT-schematic.pdf` 为准。

## 制造文件

Gerber/Drill 文件位于：

```text
hardware/gerber/extracted/
```

原始压缩包位于：

```text
hardware/fabrication/MPPT-gerber-drill-fabrication.zip
```

下单前应至少完成：

- 使用 Gerber Viewer 复核板框、层叠、焊盘、丝印和阻焊。
- 检查 PTH/NPTH 钻孔是否被 PCB 厂正确识别。
- 确认铜厚、板厚、过孔工艺、阻焊颜色和表面处理。
- 根据实际功率等级复核走线宽度、温升、保险丝、MOSFET、采样电阻和电感电流能力。

## 安全说明

该硬件涉及光伏输入、电池充电、大电流 DC-DC 和锂电/铅酸电池系统。打样和上电前必须配合限流电源、保险丝、BMS、电子负载、隔离调试和必要的硬件过压/过流/过温保护。软件保护不能替代硬件保护。

## 开源许可证

上传公开仓库前必须阅读：

```text
docs/DESIGN_NOTES.md
LICENSE_OPTIONS.md
```

本仓库采用 `CERN-OHL-P-2.0` 许可证发布硬件资料。该许可证适合硬件设计文件、Gerber/Drill、原理图 PDF 和后续可编辑 EDA 工程的开源复用。
