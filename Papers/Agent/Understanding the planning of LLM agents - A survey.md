# **Concepts**

# **Structure**

## **3. Task Decomposition**

在现实世界的场景中，环境往往具有复杂性和可变性，因此通过一步规划过程解决复杂任务是一项艰巨的挑战。

一般分为 decomposition-first and interleaved decomposition

对于分解优先的方法，优势在于在子任务和原始任务之间建立更强的相关性，降低任务遗忘和幻觉的风险。然而，由于子任务在开始时是预先确定的，因此需要额外的调整机制，否则某个步骤中的一个错误将导致失败，这将在第6节中讨论。另一方面，交错分解和子规划根据环境反馈动态调整分解，提高容错性。然而，对于复杂的任务，过长的轨迹可能会导致LLM出现幻觉，在后续的子任务和子规划中偏离最初的目标。

### 3.1 Decomposition-First Methods

分解优先方法首先将任务分解为子目标，然后依次为每个子目标制定计划。

### 3.2 Interleaved Decomposition Methods

每个分解只显示当前状态下的一两个子任务。

## **4. Multi-plan Selection**

尽管LLM具有很强的推理能力，但LLM生成的单个计划可能不是最优的，甚至是不可行的。一种更自然的方法是多平面选择，包括两个主要步骤：多平面生成和最优方案选择。

由于LLM在排名任务中的表现仍在审查中，因此需要进一步验证和微调其在这一特定背景下的能力。LLM的随机性为选择增加了随机性，可能会影响所选计划的一致性和可靠性。

### 4.1 Multi-Plan Generation

多计划生成涉及生成十几条计划路径，以组成候选计划集。主流方法考虑在生成模型的解码过程中使用不确定性。

### 4.2 Optimal Plan Selection

应用了朴素多数投票策略，将得票最多的计划视为最优选择。受益于树架构，思想之树（ToT）[Yao等人，2023]支持树搜索算法，如传统的BFS和DFS。在选择要扩展的节点时，它使用LLM来评估多个操作并选择最佳操作。

与ToT类似，LLMMCTS[赵等人，2023b]和RAP[郝等人，2023]也使用树结构来帮助多计划搜索。与ToT不同，他们采用蒙特卡洛树搜索（MCTS）算法进行搜索。LLM A*[Shio和Wang，2023]利用人工智能中的经典A*算法来辅助LLM进行搜索。从当前位置到目标位置的切比雪夫距离用作选择最优路径的启发式成本函数。

## **5. External Planner-Aided Planning**

尽管大型语言模型（LLM）展现出强大的推理和任务分解能力，但当面对具有复杂约束的环境时，如数学问题解决或生成可接受的动作，会出现挑战。为了应对挑战，有几种方法将LLM与外部规划者相结合。基于引入的规划器，这些方法可分为符号规划器和神经规划器。

### 5.1 Symbolic Planner

几十年来，符号规划师一直是自动化规划领域的基本组成部分。这些方法基于成熟的符号形式化模型，如PDDL模型[Aeronautiques等人，1998；Haslum等人，2019]，采用符号推理来识别从初始状态到期望目标状态的最佳路径。

### 5.2 Neural Planner

神经规划者是使用强化学习或模仿学习技术对收集到的规划数据进行训练的深度模型，在特定领域内显示出有效的规划能力。

SwiftSage[Lin等人，2023]利用认知心理学的双重过程理论，将计划过程分为慢思维和快思维。缓慢的思维过程涉及复杂的推理和理性思考，而快速思维则类似于通过长期训练发展起来的本能反应。作者利用通过模仿学习训练的DT模型作为快速生成计划的快速思维模型。当计划执行过程中出现错误，表明问题更复杂时，代理会切换到慢速思维过程，LLM会根据当前状态进行推理和规划。这种快思维和慢思维的结合已被证明在效率方面非常有效。

##  **6. Reflection and Refinement**

反思和提炼是规划过程中不可或缺的组成部分。它们增强了LLM代理规划的容错性和纠错能力。由于现有的幻觉问题和对复杂问题的推理能力不足，LLM代理可能会在规划过程中因反馈有限而出错并陷入“思维循环”。反思和总结失败有助于代理纠正错误，并在后续尝试中打破这种循环。

## **7. Memory-augmented Planning**

对于代理人来说，记忆是提高计划能力和增长潜力的关键途径。关于LLM代理中的记忆机制，目前有两种主要方法通过记忆来增强计划能力：基于RAG的记忆和具身记忆。

基于RAG和基于微调的内存方法增强了LLM Agent的规划能力，每种方法都有其独特的优势和局限性。基于RAG的方法主要在自然语言文本中提供实时、低成本的外部存储器更新，但依赖于检索算法的准确性。微调通过参数修改提供了更大的存储容量，但内存更新成本很高，难以保留细粒度的细节。

### 7.1 RAG-based Memory

这种方法的核心思想是在任务规划过程中从记忆中检索与任务相关的经验。在这些方法中，记忆通常存储在附加存储器中，形式多种多样

### 7.2 Embodied Memory

体现记忆涉及用代理的历史经验样本微调LLM，将记忆嵌入模型参数中。通常，经验样本是从代理与环境的交互中收集的，其中可能包括关于环境的常识知识、与任务相关的先验知识以及成功或失败的经验。虽然训练一个包含数十亿个参数的语言模型的成本是巨大的，但通过仅训练一小部分参数，如LoRA、QLoRA、P-tuning等，可以利用参数高效微调（PEFT）技术来降低成本并加快速度。

## **8. Evaluation**



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