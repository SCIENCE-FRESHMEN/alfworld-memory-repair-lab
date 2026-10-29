# alfworld-memory-repair-lab

ALFWorld embodied agent memory repair experiment lab, addressing memory corruption issues for agents

![]([https://img.shields.io/badge/Python-3.10+-brightgreen](https://img.shields.io/badge/Python-3.10+-brightgreen))
![]([https://img.shields.io/badge/ALFWorld-Ready-blue](https://img.shields.io/badge/ALFWorld-Ready-blue))
![]([https://img.shields.io/badge/Agent-Memory-Repair-orange](https://img.shields.io/badge/Agent-Memory-Repair-orange))
![]([https://img.shields.io/badge/Open-For-Research-important](https://img.shields.io/badge/Open-For-Research-important))
  

## project introduction

Existing large model agents working on ALFWorld suffer from memory drift during multi step household interaction. Agents forget object positions mix up environment states and conflict historical observations. Task success rate drops rapidly as interaction steps increase.

Most existing methods extend prompt length and feed full historical trajectories. These methods raise token cost and cannot solve the root problem. This repository implements memory error detection and online memory repair. It avoids uncontrolled context expansion and corrects inconsistent agent memory.

This repository provides a complete experiment pipeline for ALFWorld. It includes memory error identification modules state consistency repair operators ALFWorld environment wrapper evaluation scripts and baseline implementations. Researchers can run ablation studies and comparative experiments directly on this codebase.

## core features

online memory repair instead of appending all historical observations
the framework scans internal memory graph in runtime detects contradictory missing and misaligned state information and corrects memory errors to reduce decision hallucination
low token consumption compared with full trajectory retrieval baselines
models with smaller parameter sizes can handle long household tasks without relying on extremely large language models
complete ready to use ALFWorld experiment stack
environment connection trajectory collection memory log export and automatic evaluation on seen unseen splits are all encapsulated. Users can finish full experiment runs in short time after repository clone
fine grained error analysis toolkit
the system automatically counts different memory failure types including position forgetting state conflict environment confusion and time sequence disorder. It generates structured failure statistics for agent behavior analysis
modular architecture for easy extension
repair logic memory representation and large model backend are decoupled. New memory algorithms can be integrated with limited interface implementation and compared with existing methods

## performance overview

native agents show obvious memory drift with more interaction steps and often fail completely on unseen scenes
agents enhanced with the memory repair pipeline maintain better stability on long trajectories. Many failed trajectories from native agents can be recovered
the framework achieves better performance on hard unseen room generalization tasks with lower token budget compared with vanilla retrieval memory baselines

this repository fits researchers who meet long trajectory memory drift and hallucination problems on ALFWorld and need a standardized evaluation platform to test new memory ideas

## quick start

### environment setup

```
git clone [https://github.com/SCIENCE-FRESHMEN/alfworld-memory-repair-lab.git](https://github.com/SCIENCE-FRESHMEN/alfworld-memory-repair-lab.git)
cd alfworld-memory-repair-lab

pip install -r requirements.txt

python scripts/download_alfworld.py
```

### run evaluation

```
python run_eval.py --config configs/default_repair.yaml

python run_eval.py --config configs/baseline_no_repair.yaml
```

evaluation results memory failure logs and statistical reports are saved to ./output

## repository structure

```
alfworld-memory-repair-lab
├── agent
│   ├── memory_repair.py
│   └── llm_agent.py
├── alfworld_env
├── configs
├── scripts
├── run_eval.py
└── output
```

## target users

researchers working on embodied agent and large model agent memory who need stable ALFWorld environment
researchers troubled by long trajectory memory drift and state hallucination
researchers with new memory algorithms requiring interactive environment evaluation
researchers collecting memory failure samples to study agent memory failure patterns

## limitation

memory repair cannot eliminate all failures. Performance degrades on extremely long trajectories or observations with insufficient information. Pull requests for improved repair strategies are welcome

## citation

```
@misc{alfworld-memory-repair-lab,
  title={alfworld-memory-repair-lab: A Repair-Oriented Memory Experiment Lab for ALFWorld Embodied Agents},
  author={SCIENCE-FRESHMEN},
  year={2026},
  howpublished={\url{[https://github.com/SCIENCE-FRESHMEN/alfworld-memory-repair-lab.git](https://github.com/SCIENCE-FRESHMEN/alfworld-memory-repair-lab.git)}}
}
```

## contributing

users can submit issues for bugs and pull requests for new repair strategies or baseline implementations

## license

MIT License
