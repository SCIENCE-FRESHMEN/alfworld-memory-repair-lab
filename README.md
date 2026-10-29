# alfworld‑memory‑repair‑lab

> 
> 🚀 ALFWorld 智能体记忆修复实验工坊 —— 专治 Embodied Agent “记性崩坏”，把翻车的记忆拉回SOTA赛道

![]([https://img.shields.io/badge/Python-3.10+-brightgreen](https://img.shields.io/badge/Python-3.10+-brightgreen))
![]([https://img.shields.io/badge/ALFWorld](https://img.shields.io/badge/ALFWorld)‑Ready-blue)
![]([https://img.shields.io/badge/Agent](https://img.shields.io/badge/Agent)‑Memory‑Repair‑orange)
![]([https://img.shields.io/badge/Open](https://img.shields.io/badge/Open)‑For‑Research‑important)
  

**别人还在堆上下文，我们直接修复坏掉的记忆。**

## ✨ 项目简介

现在大模型Agent在ALFWorld里有多狼狈？多步 household 交互跑几步记忆就跑偏：遗忘物体位置、混淆环境状态、把历史观察张冠李戴，明明任务还没结束，智能体已经活在“平行宇宙”，成功率疯狂跳水。

市面上绝大多数方案还在疯狂加长prompt、无脑塞更多历史上下文，token开销爆炸还治标不治本。**本工坊不走堆长度的老路，主打记忆错误检测+在线修复，在不暴力膨胀上下文窗口的前提下，把跑偏的Agent记忆强行掰回正轨。**

> 
> 毫不夸张的说：这是一套专为ALFWorld交互任务量身打造的记忆诊断修复实验床。同样的基座大模型，套上我们的记忆修复流水线， unseen 未见场景下任务成功率直接甩开原生基线一大截，小模型也能打出让人惊喜的表现。不用换天价大权重，靠记忆纠错就实现性能跃迁。

本仓库完整开放整套实验链路：记忆错误识别模块、状态一致性修复算子、ALFWorld环境封装、完整评测脚本、多组基线复现代码。做Embodied Agent记忆方向的同学，拿过去就能跑 ablation、刷对比实验、快速验证脑洞，省去从零对接ALFWorld的大量脏活累活。

## 🔥 核心亮点（吹爆版）

- 🩹 **记忆在线修复，而不是无脑追加历史**
不把全部轨迹无脑丢进prompt。实时扫描智能体内部记忆图谱，定位矛盾、丢失、错位的状态节点，就地修正错误记忆，从根源减少决策幻觉。
- ⚡ **极致Token友好，拒绝上下文内卷**
同等任务表现，上下文开销远低于全量历史回放方案。小参数量模型也能驾驭长轨迹 household 任务，不必死磕昂贵超大模型。
- 🧪 **开箱即打的ALFWorld完整实验工坊**
环境对接、轨迹采集、记忆日志导出、seen/unseen集合自动评测全部封装完毕。别人花一两周搭的实验底座，你clone下来半天就能跑完整套对比实验。
- 📊 **完备的错误分析工具链**
自动统计记忆错误类型：物体位置遗忘、状态冲突、环境混淆、时序错乱，输出细粒度故障报告，帮你看透Agent到底是哪里“记性坏掉”。
- 🧩 **模块化设计，自由插拔你的脑洞**
修复逻辑、记忆表示、后端LLM基座全部解耦。你想上新的记忆算法？只需要实现少量接口，直接接入这套评测框架，快速和已有方案同台竞技。

## 📈 效果速览（口头吹嘘版）

在ALFWorld标准测试集上：

- 原生Agent很容易随着步骤增加发生记忆漂移，unseen场景经常直接崩盘；
- 接入本项目记忆修复流水线后，长轨迹任务稳定性肉眼可见提升，大量之前直接废掉的任务轨迹被成功救回；
- 对比传统简单检索记忆基线，在高难度未见房间泛化场景优势尤其突出，用更低的token拿到更高成功率。

> 
> 实话讲，如果你正在踩坑：Agent跑ALFWorld越往后越乱、长步长直接摆烂、换大模型改善依然有限，那这个仓库大概率就是你找了很久的实验底座。

## 🛠️ 快速开始

### 环境安装

```
git clone [https://github.com/SCIENCE](https://github.com/SCIENCE)‑FRESHMEN/alfworld‑memory‑repair‑lab.git
cd alfworld‑memory‑repair‑lab

# 安装依赖
pip install -r requirements.txt

# 配置ALFWorld环境，下载数据集
python scripts/download_alfworld.py
```

### 快速跑一遍带记忆修复的评估

```
# 使用默认配置，在ALFWorld测试集运行修复增强Agent
python run_eval.py --config configs/default_repair.yaml

# 对比原生无修复基线
python run_eval.py --config configs/baseline_no_repair.yaml
```

跑完之后结果、记忆故障日志、统计报告全部输出至`./output`目录，直接拿来写实验、画图表。

## 📂 仓库结构

```
alfworld‑memory‑repair‑lab
├── agent/                # Agent主体，记忆修复核心逻辑
│   ├── memory_repair.py  # 记忆错误检测与修复算子【重点】
│   └── llm_agent.py      # LLM驱动智能体封装
├── alfworld_env/         # ALFWorld环境适配层
├── configs/              # 各种实验配置，基线/修复方案直接切换
├── scripts/              # 数据集下载、数据分析、日志解析脚本
├── run_eval.py           # 主评测入口
└── output/               # 输出评测结果、记忆错误日志
```

## 🧠 适合哪些人

✅ 做Embodied Agent、LLM智能体记忆研究，苦于ALFWorld环境搭建繁琐；
✅ 被Agent长轨迹记忆漂移、状态幻觉反复折磨；
✅ 想验证新记忆算法，需要一套现成的交互式环境评测床；
✅ 需要大量记忆故障样例，用来分析Agent记忆失效模式。

> 
> 如果你想搞新idea，这个仓库给你铺好了跑道，剩下就看你的想象力。

## ⚠️ Limitation（客观保留一点底线）

记忆修复不是魔法，极端超长轨迹、极度模糊的观察输入依然存在修复边界。欢迎提交PR改进修复策略，一起把Agent记性变得更强。

## 📝 Citation

如果你在科研工作中使用本仓库代码或实验框架，可以引用：

```
@misc{alfworld‑memory‑repair‑lab,
  title={alfworld‑memory‑repair‑lab: A Repair‑Oriented Memory Experiment Lab for ALFWorld Embodied Agents},
  author={SCIENCE‑FRESHMEN},
  year={2026},
  howpublished={\url{[https://github.com/SCIENCE](https://github.com/SCIENCE)‑FRESHMEN/alfworld‑memory‑repair‑lab.git}}
}
```

## 🤝 Contributing

欢迎issue提bug、提交修复策略、新增基线对比。有酷炫记忆算法想法直接PR，一起卷Agent记忆的新高度！

## License

MIT License
