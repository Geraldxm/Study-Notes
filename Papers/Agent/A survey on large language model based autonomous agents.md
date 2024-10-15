# **Concepts**

## Autonomous agentsAutonomous agent

能够自主感知、决策和行动的计算系统或实体。它们在没有人为干预的情况下，可以根据环境的变化和内部目标做出决策，并执行相应的行动。

特征有：自主性、感知能力、决策能力、行动能力（影响环境）、目标导向

## Human-level Intelligence

- 多领域的高水平智能
- 学习能力
- 推理和决策
- 情感和社交
- 语言理解和生成
- 灵活和适应性

## **Agent** (Most Importantly)

definition: 自主行动、感知环境、做出决策并与其他Agent或人类进行交互的计算机程序或实体

- 自主性、反应性、社交性和适应性


# **Structure**

## 2. Construction of LLM-based Autonomous Agent

GOAL: perform diverse tasks by using LLMs

(1) which architecture should be designed to better use LLMs
- culminating in a comprehensive unified framework

(2) give the designed architecture, how to enable the agent to acquire capabilities for accomplishing specific tasks.
- summarize the strategies for agent capability acquisition based on whether they fine-tune the LLMs

###  2.1 Agent architecture design
#### 2.1.1 Profiling module
- aims to indicate the profiles of the agent roles
- encompass
	- personal basic information
	- personalities
	- relationships
- 为代理创建特定的配置文件
	- 手工制作 Handcrafting
		- flexible but labor-intensive
	- LLM 生成
		- can be few-shot
		- time-saving but lack precision
	- 数据对齐方法
		- 使用选民的真实属性

#### 2.1.2 Memory module
- 存储感知到的信息，形成记忆
- memory structure
	- 从人类记忆得到灵感，有长时记忆和短时记忆
	- 短期记忆类似transformer的上下文窗口
	- 长期记忆类似外部存储向量，需要快速查询和检索
	- 统一内存 Unified Memory
		- LLM上下文有限制，难以将所有内存放入prompt
	- 混合存储 Hybrid Memory
		- 明确模拟了长短期记忆
		- 短期记忆缓冲最近的感知
		- 长期记忆巩固重要信息
		- 有多种实现方式
- memory formats
	- 自然语言内存
		- 语义丰富好观察
	- embedding
		- 检索效率高
	- databases
		- 代理使用sql语句
	- structured list
		- 适合存储结构化的数据
- memory operations
	- memory reading
		- 关键是如何从历史行为中提取有价值的信息
		- 可以考虑 recency, relevance, importance，调比例设置重要程度
	- memory writing
		- 如何存储相似的信息？
			- 计数，压缩
		- 当内存溢出，如何删除信息
			- 换出策略
	- **memory refleting**
		- 智能体的记忆反思能力如何使其能够从过去的经验中提炼出有价值的知识和见解，进一步激发更高层次的认知和决策能力。这种能力不仅限于直接的经历回顾，而是涉及到更深层次的探索和反思过程。
#### 2.1.3 Planning module
- 旨在赋予agent任务分解和解决能力
- 没有反馈的计划 planning without feedback
	- 单路径推理，任务被分解为几个级联的中间步骤
		- CoT, Zero-shot CoT, Re-Prompting (在生成计划前检查步骤是否满足条件), ReWOO (计划和观察分离)
	- 多路径推理，Self-Consistent COT, ToT, GoT (图状), AoT, RAP
	- external planner，LLM+P (转换为PDDL), LLM-DP, CO-LLM (认为LLM擅长指定高层次的计划，因此低层次的任务使用外部计划器)
- 有反馈的计划 Planning with feedback
	- 人类个体可以根据外部反馈迭代制定计划
	- 从环境、人类、模型中获得
	- 从环境
		- ReAct: 思维-动作-观察
		- Voyager: 中间进度，执行错误，自我验证
		- DEPS: 建议告知代理任务失败的详细原因，使他们能够更有效地修改计划
		- Inner Monologue: 在agent采取行动后向其提供三种类型的反馈，1-任务成功，2-passive场景描述，3-active场景描述
	- 从人类
		- Inner Monologue: 代理旨在在3D视觉环境中执行高级自然语言指令。它具有主动征求人类对场景描述的反馈的能力
	- 从模型
#### 2.1.4 Action module
- 将agent的决策转化为具体的结果
- 受profile，memory，planning的影响
- action goal
	- 行动的预期结果是什么
- action production
	- 动作如何生成
	- memory recollection
	- plan following
- action space
	- 有哪些可用的动作
	- external tools
		- APIs
			- TaskMatrix.AI: 数百万个API
		- Databases
		- External models
		- Internal knowledge
- action impact
	- 动作的影响是什么
	- 环境变化
	- 内部状态变化
	- 触发新的行动
### 2.2 Agent capability acquisition

agent的架构类似于“硬件”设计，而处理特定任务的能力、技能和经验可以视为“软件”资源。

一般通过是否需要微调来对 LLM 进行分类。

#### with fine-tuning
- 使用人工注释数据集
- 使用 LLM 生成

#### without fine-tuning
- prompt engineering
- designing proper agent evolution mechanisms
	- 试错法 trail-and-error
	- 集智 crowd-sourcing
	- 经验积累 experience accumulation
	- 自我驱动 self-driven
		- 自主设定目标，探索环境和接受激励
		- 多个模型互相对话来解决问题
		- 
## 3. Diverse Applications
### 3.1 社会科学
- 心理学
- 政治学和经济学
- 社会模拟
- 法理学
- 研究助理

### 3.2 自然科学
- 文件和数据管理: 用于查询和利用信息
- 实验助理: 自动化科学实验
- 自然科学教育

### 3.3 工程
- 土木工程: 用于设计优化复杂结构
- CS 和 SE: 自动化设计、编码、测试、调试、生成文档；虚拟团队，扮演多种开发过程中的角色；代码提示
- 工业自动化
- 机器人和具身智能
## 4. Evaluation Strategies
- 主观评价
	- 人工评分
	- 图灵测试
	- 用其他 agent 评价
- 客观评价
	- Metrics 指标
		- 任务成功
		- 人类相似度
		- 效率
	- Protocol 协议
		- 现实世界模拟: 执行任务，评估和人类执行任务的相似程度
		- 社会评估: 是否和人类有相似的社会职能，包括协作能力、分析推理能力等
		- 多任务评估: 
		- 软件测试
	- Benchmark 基准

## 5. Challenges and Future Directions

# **Q&As**

Q: What is your take-away message from this paper?
Q: 你从这篇论文中得出的主要信息是什么？

Q: What is the motivation for this work (both people problem and technical problem), and its distillation into a research question? Why doesn’t the people problem have a trivial solution? What are the previous solutions and why are they inadequate?
Q: 这项工作的动机是什么（包括人的问题和技术问题），以及如何将其提炼为一个研究问题？为什么人的问题没有一个简单的解决方案？之前有哪些解决方案，为什么它们不够完善？

Q: What is the proposed solution (hypothesis, idea, design)? Why is it believed it will work? How does it represent an improvement? How is the solution achieved?
Q: 提出的解决方案是什么（假设、想法、设计）？为什么认为它会奏效？它如何体现了改进？该解决方案是如何实现的？

Q: What is the author’s evaluation of the solution? What logic, argument, evidence, artifacts (e.g., a proof-of-concept system), or experiments are presented in support of the idea?
Q: 作者对该解决方案的评价是什么？有哪些逻辑、论点、证据、工件（例如概念验证系统）或实验来支持这一想法？

Q: What is your analysis of the identified problem, idea and evaluation? Is this a good idea? What flaws do you perceive in the work? What are the most interesting or controversial ideas? For work that has practical implications, ask whether this will work, who would want it, what it will take to give it to them, and when might it become a reality?
Q: 你对所识别的问题、想法和评估的分析是什么？这是一个好主意吗？你认为这项工作有哪些缺陷？最有趣或最具争议的想法是什么？对于具有实际意义的工作，问问它是否会奏效，谁会需要它，需要什么才能实现，以及它何时可能成为现实？

Q: What are the paper’s contributions (author’s and your opinion)? Ideas, methods, software, experimental results, experimental techniques...?
Q: 这篇论文的贡献是什么（作者的和你的看法）？包括想法、方法、软件、实验结果、实验技术等？

Q: What are future directions for this research (author’s and yours, perhaps driven by shortcomings or other critiques)?
Q: 这项研究的未来方向是什么（作者的和你的看法，可能由不足之处或其他批评驱动）？

Q: What questions are you left with? What questions would you like to raise in an open discussion of the work (review interesting and controversial points, above)? What do you find difficult to understand? List as many as you can, at least three, not including questions that can be answered quickly by searching the internet?
Q: 你还剩下哪些问题？在公开讨论这项工作时你想提出哪些问题（回顾上面有趣和有争议的观点）？你觉得哪些地方难以理解？尽可能多列出问题，至少三个，并且不包括那些可以通过快速搜索互联网得到解答的问题。