\# Combinatorial Optimization Paper Writing Skill



本仓库提供一个面向\*\*组合优化论文开发\*\*的 Codex Skill，适用于将已有的算法代码、实验结果、研究记录和文献材料整理为结构规范、实现一致的学术论文。



Skill 名称：



```text

write-combinatorial-optimization-paper

```



适用问题包括但不限于：



\- TSP / Traveling Salesman Problem

\- VRP / Vehicle Routing Problem

\- Bin Packing

\- Cutting and Packing

\- Scheduling

\- Facility Location

\- Assignment Problem

\- Network Optimization

\- Routing

\- Packing

\- 其他组合优化、运筹优化和元启发式算法问题



\---



\# 1. 仓库结构



```text

write-combinatorial-optimization-paper/

├── SKILL.md

└── references/

&#x20;   ├── group-writing-patterns.md

&#x20;   ├── paper-corpus.md

&#x20;   └── problem-profile-template.md

```



各文件作用如下。



\## `SKILL.md`



Skill 的核心文件。



主要定义组合优化论文开发流程，包括：



\- 理解问题定义

\- 检查代码实现

\- 从代码中还原算法

\- 建立数学模型

\- 总结算法贡献

\- 撰写 Algorithm Section

\- 分析算法复杂度

\- 设计实验

\- 设计消融实验

\- 与已有文献进行比较

\- 检查论文与代码实现的一致性

\- 避免未经实验支持的结论



原则：



> 论文中的算法描述必须与真实实现保持一致。



\---



\## `group-writing-patterns.md`



用于记录和总结课题组常用的论文写作方式，包括：



\- Introduction 结构

\- Related Work 组织方式

\- Algorithm Section 写法

\- Contribution 表述

\- 实验分析方式

\- OR / Combinatorial Optimization 论文常见表达



Codex 可以参考这些模式优化论文表达。



\---



\## `paper-corpus.md`



用于记录优秀论文或目标论文中的：



\- 论文结构

\- 算法描述方式

\- 数学符号使用方式

\- 实验设计

\- 消融实验设计

\- 对比实验

\- 写作风格



它不是具体某个研究问题的结论，而是作为论文写作参考语料。



\---



\## `problem-profile-template.md`



用于建立\*\*自己课题的 Problem Profile\*\*。



每个人的研究问题不同，因此不要直接复用其他人的 problem profile。



例如：



```text

TSP

VRP

Scheduling

Bin Packing

Facility Location

```



应该分别建立自己的 profile。



推荐命名：



```text

tsp-application.md

vrp-application.md

scheduling-application.md

bin-packing-application.md

```



\---



\# 2. 安装方法



Codex Skill 默认放在：



Windows：



```text

C:\\Users\\<用户名>\\.codex\\skills\\

```



Linux / macOS：



```text

\~/.codex/skills/

```



将：



```text

write-combinatorial-optimization-paper

```



整个文件夹复制到：



```text

.codex/skills/

```



最终目录应类似：



```text

.codex/

└── skills/

&#x20;   └── write-combinatorial-optimization-paper/

&#x20;       ├── SKILL.md

&#x20;       └── references/

&#x20;           ├── group-writing-patterns.md

&#x20;           ├── paper-corpus.md

&#x20;           └── problem-profile-template.md

```



\---



\# 3. 如何调用 Skill



在 Codex 中可以直接说：



```text

使用 write-combinatorial-optimization-paper skill

```



或者：



```text

$write-combinatorial-optimization-paper

```



然后继续说明需要完成的任务。



例如：



```text

使用 $write-combinatorial-optimization-paper。



请阅读当前项目代码，分析实际实现的算法，

并帮助我整理 Algorithm Section。

```



也可以：



```text

使用 $write-combinatorial-optimization-paper。



请检查论文中的算法描述是否和代码实现一致。

```



\---



\# 4. 第一次使用时建议先建立自己的 Problem Profile



由于不同组合优化问题的：



\- 决策变量

\- 目标函数

\- 约束

\- 搜索空间

\- 邻域结构

\- 算法设计

\- 数据集

\- 评价指标



差异很大，因此建议每个课题首先建立自己的：



```text

problem profile

```



可以让 Codex 基于：



```text

references/problem-profile-template.md

```



自动生成。



例如：



```text

使用 $write-combinatorial-optimization-paper。



我的研究问题是 Vehicle Routing Problem。



请阅读：



1\. 当前项目代码

2\. README

3\. 实验脚本

4\. 当前论文草稿

5\. problem-profile-template.md



根据真实实现建立：



references/vrp-application.md



要求所有算法描述都以实际代码为依据，

不要根据常见 VRP 算法自行补充不存在的模块。

```



\---



\# 5. 推荐的 Problem Profile 内容



自己的 Problem Profile 最好至少包含以下内容。



\## Problem



```text

Problem name

Problem abbreviation

Application background

```



\## Mathematical Model



```text

Decision variables

Objective

Constraints

```



\## Algorithm



```text

Main framework

Initialization

Neighborhood

Local search

Metaheuristic

Repair / perturbation

Stopping criterion

```



\## Implementation



```text

Programming language

Libraries

Important data structures

Parallelization

Caching

Acceleration techniques

```



\## Experiments



```text

Benchmark datasets

Baselines

Metrics

Parameter settings

Stopping conditions

Hardware

```



\## Candidate Contributions



例如：



```text

Contribution 1

Contribution 2

Contribution 3

```



注意：



Contribution 应该由：



```text

实现 + 实验 + 文献对比

```



共同支持，而不是单纯根据代码模块数量总结。



\## Implementation–Paper Consistency



记录论文必须遵守的关键实现事实。



例如：



```text

实际使用 best improvement，而不是 first improvement。



实际只有 swap 和 relocate 两种邻域。



算法没有使用 multiprocessing。



缓存只用于 XX 模块。

```



这样可以避免论文修改过程中逐渐与代码脱节。



\## Forbidden Claims



记录当前证据不足、不应该直接写进论文的结论。



例如：



```text

不能声称达到全局最优。



不能声称显著优于所有 SOTA，除非有完整实验支持。



不能声称某模块降低复杂度，除非有理论或实验依据。

```



\---



\# 6. 推荐论文开发流程



建议不要直接让 Codex “开始写论文”。



更推荐按照下面流程逐步进行。



```text

Step 1

理解问题

&#x20;       ↓

Step 2

检查代码

&#x20;       ↓

Step 3

建立 Problem Profile

&#x20;       ↓

Step 4

还原真实算法流程

&#x20;       ↓

Step 5

确认数学模型

&#x20;       ↓

Step 6

总结 Contribution Candidates

&#x20;       ↓

Step 7

设计实验验证 Contribution

&#x20;       ↓

Step 8

撰写 Algorithm Section

&#x20;       ↓

Step 9

撰写 Experimental Section

&#x20;       ↓

Step 10

Introduction / Related Work

&#x20;       ↓

Step 11

全文 consistency check

```



核心原则：



> 先确定“做了什么”，再决定“怎么写”。



不要先写 Contribution，再回头寻找代码支持。



\---



\# 7. 一个推荐的使用方式



假设项目为：



```text

VRP\_Project/

├── src/

├── include/

├── experiments/

├── results/

└── paper/

```



可以先让 Codex：



```text

使用 $write-combinatorial-optimization-paper。



先不要修改论文。



请阅读当前代码、实验脚本和已有论文草稿，

完成以下工作：



1\. 判断实际求解的优化问题；

2\. 识别算法主框架；

3\. 识别初始化策略；

4\. 识别邻域操作；

5\. 识别局部搜索策略；

6\. 识别停止条件；

7\. 识别实验评价指标；

8\. 找出代码和论文描述不一致的位置；

9\. 根据 problem-profile-template.md 创建当前项目的 problem profile。



所有结论必须能从代码、实验或者已有材料中找到依据。

```



完成以后，再进行：



```text

根据已经确认的 problem profile，

重新整理 Algorithm Section。

```



\---



\# 8. Algorithm Section 推荐开发方式



不要直接说：



```text

帮我写 Algorithm Section。

```



建议分步骤。



首先：



```text

请根据代码还原完整算法流程。

```



然后：



```text

把算法拆成：



1\. Overall framework

2\. Initialization

3\. Solution representation

4\. Candidate generation

5\. Neighborhood search

6\. Acceptance / selection

7\. Stopping criterion

```



再确认：



```text

检查上述描述是否与实现完全一致。

```



最后：



```text

按照组合优化期刊的论文风格，

将确认后的算法整理为正式 Algorithm Section。

```



这种方式可以明显减少：



\- Codex 自行补算法

\- 论文和代码不一致

\- 把常见算法套路误写成自己的实现



\---



\# 9. Contribution 推荐开发方式



Contribution 不建议一次生成。



可以让 Codex首先列：



```text

Candidate Contributions

```



例如：



```text

C1. 新的 solution representation

C2. 新的 construction strategy

C3. 新的 neighborhood

C4. 新的 acceleration mechanism

C5. 新的 hybrid framework

```



然后逐个判断：



```text

Novelty

Implementation evidence

Experimental evidence

Literature support

```



最后只保留真正能够支持的 Contribution。



推荐原则：



```text

Contribution ≠ 模块名称



Contribution =

Novel idea

\+

Clear algorithmic role

\+

Experimental evidence

\+

Difference from existing literature

```



\---



\# 10. 实验设计



对于一个新的算法模块，最好考虑：



```text

Overall comparison

\+

Ablation study

\+

Parameter analysis

\+

Runtime analysis

```



例如提出：



```text

Candidate-window construction

```



则最好设计：



```text

Full algorithm

vs.

without candidate window

```



而不是只给最终结果。



\---



\# 11. 不要跨问题直接复用结论



本 Skill 是通用组合优化论文 Skill。



但是：



```text

不同课题之间不能直接继承 problem-specific knowledge。

```



例如：



一个 Packing 项目中的：



```text

NFP

IFP

geometry feasibility

```



不能自动应用到 VRP。



VRP 中的：



```text

2-opt

3-opt

route exchange

```



也不能自动应用到 Scheduling。



因此：



> 每个项目都应该建立自己的 Problem Profile。



\---



\# 12. 代码优先原则



如果出现以下三者不一致：



```text

论文描述

实验脚本

实际代码

```



不要直接猜测。



应该先确认：



```text

实际运行的版本是什么？

```



然后以真实实验对应的代码实现为准。



特别需要检查：



```text

Branch

Commit

Parameters

Random seed

Thread count

Stopping criterion

Dataset

```



\---



\# 13. 使用 Git 时的建议



如果论文项目使用 Git，建议每次修改论文前先确认：



```bash

git branch --show-current

```



并查看：



```bash

git status

```



如果一个仓库里同时维护：



```text

paper

code

experiments

```



建议明确告诉 Codex：



```text

本次允许修改哪些文件。



哪些目录禁止修改。



是否允许 commit。



是否允许 push。

```



例如：



```text

本次只允许修改：



paper/main.tex



不要修改：



src/

experiments/

results/



修改前确认当前 Git branch。

```



\---



\# 14. 推荐 Prompt 模板



\## 项目理解



```text

使用 $write-combinatorial-optimization-paper。



请阅读当前项目代码、README、实验脚本和论文草稿。



先不要修改任何文件。



请还原：



1\. 问题定义

2\. 数学目标

3\. Solution representation

4\. Initialization

5\. Main algorithm

6\. Neighborhood

7\. Local search

8\. Stopping criterion

9\. Experimental protocol



如果代码与论文描述不一致，请明确指出。

```



\## 建立 Problem Profile



```text

使用 $write-combinatorial-optimization-paper。



根据当前项目真实代码和实验，

参考：



references/problem-profile-template.md



建立当前课题的 problem profile。



不要从其他组合优化问题复制 problem-specific assumptions。

```



\## 检查论文



```text

使用 $write-combinatorial-optimization-paper。



请检查当前 Algorithm Section。



逐项与代码进行对应，并给出：



论文描述

→

对应实现

→

是否一致

→

需要修改的位置

```



\## 总结创新点



```text

使用 $write-combinatorial-optimization-paper。



结合：



1\. 当前实现

2\. 实验结果

3\. 已有文献



提出 candidate contributions。



每个 contribution 分析：



Novelty

Implementation evidence

Experimental evidence

Literature evidence

Risk of overclaiming



暂时不要直接写 Introduction。

```



\---



\# 15. 最重要的原则



使用这个 Skill 时请始终遵守以下原则：



```text

Implementation first.



Evidence before claim.



Problem-specific knowledge stays problem-specific.



Do not invent algorithms.



Do not invent experimental conclusions.



Do not claim novelty without literature comparison.



Keep the paper consistent with the actual solver.

```



这个 Skill 的目标不是让 Codex “自动写一篇论文”。



而是让 Codex参与一个更加规范的研究流程：



```text

代码

\+

实验

\+

文献

\+

数学模型

\+

论文表达

```



并尽可能保证这些内容彼此一致。

