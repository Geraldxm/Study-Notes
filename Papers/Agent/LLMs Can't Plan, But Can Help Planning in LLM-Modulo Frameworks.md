# **Concepts**

## 第一性原理

“我们运用第一性原理，而不是比较思维去思考问题是非常重要的。我们在生活中总是倾向于比较，对别人已经做过或者正在做的事情我们也都去做，这样发展的结果只能产生细小的迭代发展。第一性原理的思想方式是用物理学的角度看待世界，也就是说一层层拨开事物表象，看到里面的本质，再从本质一层层往上走。”这是他眼中的“第一性原理思维模型”——回溯事物的本质，重新思考怎么做。

![](https://i-blog.csdnimg.cn/blog_migrate/ca68d59ad190dac3d7627b9a7eecce10.jpeg)


# **Structure**

## **Why LLMs Cant't Plan**

- **「自主模式下的局限性」**：LLMs在自主模式下（即没有外部验证或提示的情况下）并不能生成可执行的规划
- **「无法自我验证」**：LLMs无法验证自己生成的规划，因此无法通过自我批评来改进。
- **「知识获取与执行规划的混淆」**：文章指出，许多声称LLMs具有规划能力的论文实际上混淆了从LLMs中提取的一般规划知识与可执行规划之间的区别。规划任务需要不仅仅是规划领域知识，还需要能够将这些知识组装成一个可执行的规划，考虑到子目标/资源的相互作用。LLMs通常在提取规划知识方面做得很好，但这并不意味着它们能够生成可执行的规划
- **「对自我改进的误解」**：有研究声称LLMs可以通过生成规划、自我批评规划然后使用这些规划来自我改进（例如通过生成合成数据来微调自己）。然而，由于LLMs无法验证自己的解决方案，这种自我改进的方法实际上是不可行的。

## **LLM-Modulo**

基于以上理解，本文作者提出了LLM-Modulo框架（如下图所示），旨在结合LLMs的长处和外部基于模型的验证器的优势，通过更紧密的双向交互机制，使LLMs在规划任务中发挥更有意义的角色。
![](https://developer.qcloudimg.com/http-save/yehe-5990800/a378885d622f0197250dfc450e26bf22.png)

LLM-Modulo框架的基础架构是一个生成-测试-批评循环。具体来说，框架通过让LLMs生成候选规划，并利用一系列外部验证器对这些规划进行评估和反馈，确保了规划的准确性和可靠性。**「LLMs在生成创意和潜在解决方案方面表现出色，而外部验证器则严格检查规划是否满足所有必要的约束条件」**。这种结合神经网络和符号逻辑的方法，不仅提高了规划任务的准确性，还增强了框架的灵活性和扩展性，使其能够适应各种不同的规划场景。

**领域专家**在整个过程中发挥着至关重要的作用，他们的知识用于指导和细化LLM生成的规划，确保规划符合实际需求和约束。此外，通过微调过程，LLM可以从每次成功的规划中学习，逐渐提高其生成高质量规划的能力。这种持续学习和适应的能力，使得框架能够处理复杂的规划问题，包括那些包含不确定性和动态变化的问题


# **Q&As**

Q: What is your take-away message from this paper?
Q: 你从这篇论文中得出的主要信息是什么？

**「本文作者核心观点是：大语言模型（LLMs）自身无法进行规划推理」**，但是却能在解决规划问题上发挥积极的作用。为此，作者还提出了一个新的**LLM-Modulo框架**，这个框架把大型语言模型和一些外部的验证工具结合起来，使LLMs在规划任务中发挥了重要作用。


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