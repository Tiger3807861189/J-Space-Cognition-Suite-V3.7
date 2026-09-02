# J-Space Cognition Suite V3.7

[English](README.md)

[![Concept DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21971181.svg)](https://doi.org/10.5281/zenodo.21971181)

J-Space Cognition Suite 是一套面向深度推理、长程工作、工具调用、验证与恢复的模型不可知推理时控制系统。

它以 Skill 形式封装，从而支持跨平台使用、选择性加载与低摩擦集成。

套件将智能体可访问的工作表征组织为一个可主动管理的工作空间。整体由一个入口、九个按需加载的模块、四份支撑资料，以及一个用于保存长任务状态的可选标准库控制器组成。

J-Space 在推理阶段运行，模型权重和训练过程保持原有状态。

## 快速开始

### 方式 A：手动安装

1. 下载或克隆本仓库。
2. 找到当前 AI 宿主使用的用户级 Skills 目录。
3. 将完整的 [`j-space/`](j-space/) 目录复制进去，确保最终入口位于 `<Skills 目录>/j-space/SKILL.md`。
4. 使用可用的 Python 3 解释器运行完整性检查：

   ```text
   <python-command> <Skills 目录>/j-space/scripts/verify_suite.py
   ```

   请将 `<python-command>` 替换为宿主可用的 Python 3 命令，常见形式包括 `python`、`python3` 或 `py -3`。
   
5. 如果宿主只在启动时发现 Skills，请重新加载宿主。

- `j-space/` 目录应保持完整，因为 `SKILL.md` 会通过相对路径访问 `modules/`、`references/` 和 `scripts/`。

- 仓库根目录的 `LICENSE` 与 `THIRD_PARTY_NOTICES.md` 仍属于分发内容。

- 若单独再分发 `j-space/`，应同时附带这两个文件的副本。

### 方式 B：让 AI 安装

把下面的提示词复制给能够访问文件和本仓库的 AI 智能体：

```text
请从以下仓库安装 J-Space Cognition Suite：https://github.com/Tiger3807861189/J-Space-Cognition-Suite-V3.7

请先检查当前宿主的配置或文档，确认用户级 Skills 目录。将仓库中的完整 j-space/ 目录安装为 j-space/，并保持 SKILL.md、modules/、references/ 和 scripts/ 的相对结构。如果目标位置已经存在 j-space，请先比较并询问我，再执行替换。

安装后，请使用可用的 Python 3 解释器运行 scripts/verify_suite.py。完成后告诉我安装路径和校验结果，并说明当前宿主应如何调用这个 Skill。请简要解释 fast、full、loop 三种 pass，以及可选控制器负责记录长任务状态而不负责选择解法。如果当前宿主没有原生 Skill 加载能力，请说明如何通过 system/developer 指令和选择性文件检索完成接入，不要把这种接入报告成原生安装。
```

### 开始使用

通过宿主提供的 Skill 选择器、`/j-space`、`$j-space`，或者直接要求 AI 使用：

```text
请在这个任务中使用 j-space。审查这个仓库，保持现有架构，逐项验证发现，并在所有受影响文件之间维持一致状态。
```

入口门控会自动选择适合当前任务的最轻 pass。

## 运行模式

| Pass | 适用工作 | 加载内容 |
|---|---|---|
| `fast` | 单步任务，或一眼可以核验的结果 | 不加载额外机制 |
| `full` | 若干相互依赖的步骤和一个边界明确的交付物 | 一到两个相关模块；交付前运行 `ship` |
| `loop` | 多阶段、多文件、多轮、工具调用或持久状态 | 账本、接缝、checkpoint、寄存器审计和恢复 |

简短输出要求会改变外部回答长度，验证强度仍与任务底线保持一致。简单任务保持轻量，长程任务只在需要时获得持久状态。

## 核心机制

| 机制 | 作用 |
|---|---|
| 选择性工作空间加载 | 只保持一到两个承重概念活跃，其余内容外化保存 |
| 广播枢纽 | 让所有依赖分支共享名称、数值、约束和风格锚点 |
| 稠密轨 | 以紧凑且可解码的内部记法承载长链条，随后回到清晰外部语言 |
| 结论前桥接推理 | 让结论依赖的中间概念先进入活动状态 |
| 元认知控制 | 把置信度、不一致和失败信号路由为明确的下一动作 |
| 经验逃逸与验证 | 将停滞推导转化为有边界的测试，并记录验证方式与覆盖范围 |
| 第一人称能动性与功能性回响 | 用 `I`、`we`、`let's` 和 `we need` 将工作空间状态绑定到后续动作与检查 |

这些机制按需加载，并不是每个请求都要执行的固定清单。

## 可选控制器

[`j-space/scripts/jspace.py`](j-space/scripts/jspace.py) 将 `loop` 状态外化到当前任务工作区的 `.jspace/` 中。调用时使用脚本在 Skill 中的实际路径，并保持任务工作区为当前目录。

| 命令 | 用途 |
|---|---|
| `note --goal "..." --next "..."` | 打开账本，定义完成条件和第一个动作 |
| `note --next "..."` | 在 checkpoint 或 seam 后替换唯一的下一动作 |
| `note --core "名称 — 定义性事实"` | 记录一个枢纽项 |
| `note --core "名称 — 定义性事实" --core-slot 1` | 交换指定的活动枢纽项 |
| `note --check "..." --by "..."` | 追加包含验证方式与覆盖范围的 checkpoint |
| `note --open "..." --settled-by "..."` | 记录开放问题和收束条件 |
| `note --close N --check "..." --by "..."` | 以新记录的 checkpoint 关闭编号为 `N` 的问题 |
| `seam` | 重读当前状态并报告近期变化 |
| `ship FILE` | 检查输出文本中的寄存器泄漏和失效特征 |
| `resume` | 在长间隔后重新加载 premise、invariants 和完整账本 |

```text
<python-command> <skill-root>/scripts/jspace.py note --goal "完成条件" --next "第一个动作"
<python-command> <skill-root>/scripts/jspace.py note --open "解析器是否保持状态？" --settled-by "覆盖全部账本区段与边界输入的单元测试"
<python-command> <skill-root>/scripts/jspace.py note --close 1 --check "解析器保持状态" --by "单元测试覆盖全部账本区段与边界输入"
<python-command> <skill-root>/scripts/jspace.py seam
<python-command> <skill-root>/scripts/jspace.py ship OUTPUT_FILE
<python-command> <skill-root>/scripts/jspace.py resume
```

控制器负责记录和报告状态，解法仍由模型选择。它只使用 Python 标准库，并且只在任务的 `.jspace/` 目录中写入工作状态。

## 通用模型接入

具有原生 Skill 加载能力的环境可以直接安装 `j-space/`。对于聊天或 API 环境，可将 [`j-space/SKILL.md`](j-space/SKILL.md) 作为 system 或 developer 指令，并通过文件工具或检索工具开放 `modules/` 与 `references/`。

相关文件按需检索；选择性加载本身就是运行设计的一部分。

## Benchmark

### 1. 主表

| Benchmark                | GLM-5.3-Flash | GLM-5.3-Flash **+ J-Space V3.7** | GLM-5.3 | Opus-5 | Fable 5.1 |
| ------------------------ | ------------: | -------------------------------: | ------: | -----: | --------: |
| HLE (w/ tools)           |          55.3 |                                  |    62.5 |   64.7 |      65.0 |
| Terminal Bench 2.1       |          84.3 |                                  |    88.2 |  *89.1 |     *91.4 |
| NL2Repo                  |             — |                                  |    58.0 |      — |         — |
| DeepSWE v1.1             |          63.4 |                                  |    66.9 |   68.8 |      67.4 |
| Agents' Last Exam        |          26.3 |                                  |    28.5 |   31.6 |         — |
| AutomationBench (Public) |          48.8 |                                  |    48.2 |   50.3 |         — |
| GDPVal-AA v2             |          1773 |                                  |    1769 |   1861 |      1853 |

\* Terminal Bench 2.1 的 Opus-5 与 Fable 5.1 为第三方独立测评（Artificial Analysis，Terminus 2 harness，pass@1 三次重复平均），无官方数据。

### 2. 速度与 token 效率

| Benchmark                | 速度 | token 效率 |
| ------------------------ | ---: | ---------: |
| HLE (w/ tools)           |      |            |
| Terminal Bench 2.1       |      |            |
| NL2Repo                  |      |            |
| DeepSWE v1.1             |      |            |
| Agents' Last Exam        |      |            |
| AutomationBench (Public) |      |            |
| GDPVal-AA v2             |      |            |

## 跨模型兼容性

该套件的运行效应已在 DeepSeek、Qwen、GLM、GPT 与 Claude 模型系列上复现。具体幅度会随基础能力、上下文策略、工具 Harness、采样配置和 Benchmark 实现而变化。

可迁移单元是工作空间加载、选择性路由、状态外化、验证和恢复组成的协议，并不依赖特定厂商的 tokenizer 或模型 API。

## 项目结构

```text
J-Space-Cognition-Suite-V3.7/
├── .github/workflows/verify.yml    # 三平台完整性检查和回归测试
├── CITATION.cff                    # 机器可读的引用元数据
├── CONTRIBUTING.md                 # 贡献与来源说明要求
├── LICENSE                         # Apache License 2.0
├── README.md                       # 英文工程指南
├── README.zh-CN.md                 # 中文工程指南
├── THIRD_PARTY_NOTICES.md          # 外部材料的归属与许可边界
├── tests/test_jspace.py            # 标准库控制器回归测试
└── j-space/
    ├── SKILL.md                    # 唯一入口、门控、路由与 invariants
    ├── modules/                    # 九个按需加载的协议模块
    ├── references/                 # 证据、诱导方法、问题建模与工作示例
    └── scripts/
        ├── jspace.py               # 可选 loop 控制器
        ├── workspace-ledger.md     # 账本模板和契约
        └── verify_suite.py         # 编写期完整性检查
```

`SKILL.md` 是唯一注册入口。模块和参考资料按需加载，使控制系统自身保持较低的上下文压力。

维护者可以在套件根目录运行：

```text
<python-command> j-space/scripts/verify_suite.py
<python-command> -m unittest discover -s tests -v
```

## 技术依据与适用边界

J-Space 采用 Anthropic 相关可解释性研究建立的操作性工作空间术语。在本套件中，第一人称语言被作为一种控制语法：可访问状态描述会绑定到明确的动作、检查与收束。

套件关注可报告性、主动保持、中间计算、广播、监控和因果敏感性等可观察功能属性。详细的研究解释、术语、证据边界与来源维护在
[`j-space/references/j-space-science.md`](j-space/references/j-space-science.md) 中。

设计原则：

> **内部稠密，按需可解码，外部保持清晰。**

只使用任务真正需要的机制。

## 版本轨迹

J-Space 已连续经历：

**V1 → V1.5 → V1.8 → V2 → V2.5 → V2.6 → V3 → V3.1 → V3.2 → V3.5 → V3.5Turbo → V3.6 → V3.7**

V3.7 套件包含一个入口、九个聚焦模块、四份支撑资料、一个可选运行控制器、一个编写期验证器、一套标准库回归测试、三平台 CI、Apache-2.0 许可和机器可读引用元数据。

V3.7 的问题模型路由吸收了由 [@lanting200](https://github.com/lanting200) 发起的 PR，拒绝消息修复与账本重述说明回应了由 [@raelldottin](https://github.com/raelldottin) 与 [@menoxz](https://github.com/menoxz) 提出的问题，并包含 [@afeer123](https://github.com/afeer123) 的提交贡献。

## 开源协议

J-Space Cognition Suite 采用 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) 开源，允许在遵守声明保留与专利条款的前提下使用、修改、再分发及商业集成。完整条款见 [`LICENSE`](LICENSE)。引用或概述的外部材料仍遵循其来源条款，具体归属与边界见 [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md)。若只再分发运行时 `j-space/` 目录，应同时附带仓库根目录的这两个文件。
