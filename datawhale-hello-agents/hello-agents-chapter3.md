# Datawhale Hello-Agents 第三章学习记录

学习材料：

- Datawhale Hello-Agents: https://github.com/datawhalechina/hello-agents
- 第三章《大语言模型基础》: https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter3/%E7%AC%AC%E4%B8%89%E7%AB%A0%20%E5%A4%A7%E8%AF%AD%E8%A8%80%E6%A8%A1%E5%9E%8B%E5%9F%BA%E7%A1%80.md

## 1. 今日学习进度

今天开始学习第三章《大语言模型基础》，已经学到：

- 第三章主题和学习目标
- 3.1 语言模型与 Transformer 架构
- 3.1.1 从 N-gram 到 RNN
- 语言模型的基础任务
- 统计语言模型与链式法则
- 马尔可夫假设与 N-gram
- Bigram 概率的计数估计
- N-gram 的数据稀疏性与泛化能力问题
- 神经网络语言模型与词嵌入
- 余弦相似度与词向量关系
- RNN/LSTM 的上下文传递
- Transformer 出现的原因
- 3.1.2 Transformer 架构解析
- Encoder-Decoder 总体结构
- 输入嵌入与位置编码
- Self-Attention 自注意力机制
- Q/K/V 的直觉
- 注意力分数、注意力权重与 Value 加权汇总

今天先停在注意力权重这里。下次继续从 Multi-Head Attention 以及 Transformer 后续模块开始。

## 2. 第三章主题和学习目标

第三章主题是大语言模型基础。它不是直接讲 Agent 产品形态，而是补现代 LLM Agent 的底层能力来源：语言模型为什么能理解上下文、生成文本，并作为现代 Agent 的认知核心。

本章核心线索：

```text
语言模型
-> N-gram 与统计语言模型
-> 神经网络语言模型与词向量
-> RNN/LSTM
-> Transformer
-> Decoder-Only
-> 提示工程、分词、模型调用、模型选择
-> 缩放法则与模型局限
```

本章学习目标：

- 理解语言模型的基本任务：估计词序列或下一个 token 的概率。
- 理解从 `N-gram -> 神经网络语言模型/RNN -> Transformer` 的演进逻辑。
- 理解提示词、分词、模型选择分别在与 LLM 交互时解决什么问题。
- 理解大模型能力提升背后的代价和局限，例如幻觉、成本、可控性和上下文限制。

关键理解：

> LLM 的强大能力不是从“会聊天”开始的，而是从“在上下文中预测下一个 token”这个基础任务逐步发展出来的。

## 3. 语言模型的基础任务

语言模型最基础的任务，不是回答问题，也不是像数据库一样查标准答案，而是：

> 估计一个词序列出现的概率，或在已有上下文下预测下一个 token 的概率。

例子：

```text
我今天去学校学习
学校今天我去学习
```

第一句话通常比第二句话更自然，所以语言模型应该给第一句话更高概率。

生成文本时，模型本质上是在不断做：

```text
给定前面的上下文，下一个最可能出现的 token 是什么？
```

重要区分：

| 方式 | 含义 |
| --- | --- |
| 数据库查询 | 找到已有的标准答案或结构化记录 |
| 语言模型生成 | 基于上下文一步步预测 token，生成看起来合理的回答 |

所以 LLM 的回答有概率性和随机性。它可以生成流畅内容，但不保证一定是事实正确的标准答案。

## 4. 统计语言模型与链式法则

统计语言模型会把一句话的概率拆成一串条件概率相乘。

例如：

```text
datawhale agent learns
```

可以拆成：

```text
P(datawhale agent learns)
= P(datawhale)
  * P(agent | datawhale)
  * P(learns | datawhale, agent)
```

其中 `|` 表示 given，也就是“在......条件下”。

例如：

```text
P(learns | datawhale, agent)
```

表示：

> 在已经看到 `datawhale agent` 的条件下，下一个词是 `learns` 的概率。

链式法则的问题是：如果句子很长，最后一个词可能要依赖前面所有词。

```text
P(第100个词 | 前面99个词)
```

真实语料里，“前面 99 个词完全一样”的情况可能根本没有出现过，因此很难可靠统计。

## 5. 马尔可夫假设与 N-gram

为了解决完整历史太长、无法可靠统计的问题，N-gram 引入了马尔可夫假设：

> 当前词不依赖完整历史，只依赖前面有限几个词。

例如原来想计算：

```text
P(learns | datawhale, agent)
```

如果用 Bigram，也就是 `N=2`，只看前面 1 个词：

```text
P(learns | agent)
```

如果用 Trigram，也就是 `N=3`，看前面 2 个词：

```text
P(learns | datawhale, agent)
```

N-gram 的本质：

> 它不是让模型真正理解语言，而是用局部词组的统计规律近似语言概率。

例子：

```text
我 喜欢 吃 苹果
```

Bigram 会统计：

```text
我 -> 喜欢
喜欢 -> 吃
吃 -> 苹果
```

它看到的是相邻词之间的搭配频率，而不是“我喜欢吃苹果”这个完整语义。

## 6. Bigram 概率的计数估计

Bigram 概率可以通过语料库中的计数估计：

```text
P(w_i | w_{i-1}) = Count(w_{i-1}, w_i) / Count(w_{i-1})
```

读成人话就是：

> 某个词后面接另一个词的概率 = 这两个词连续按顺序出现的次数 / 前一个词出现的总次数。

示例语料：

```text
datawhale agent learns
datawhale agent works
```

估算：

```text
P(datawhale agent learns)
= P(datawhale) * P(agent | datawhale) * P(learns | agent)
```

逐个计算：

```text
P(datawhale) = 2 / 6 = 0.333
P(agent | datawhale) = Count(datawhale agent) / Count(datawhale) = 2 / 2 = 1
P(learns | agent) = Count(agent learns) / Count(agent) = 1 / 2 = 0.5
```

所以：

```text
P(datawhale agent learns) = 0.333 * 1 * 0.5 = 0.167
```

今天纠正的重点：

- `Count(datawhale agent)` 不是“同时出现”，而是“连续、按顺序出现”。
- `datawhale agent` 和 `agent datawhale` 不是一回事。
- `P(learns | agent)` 的分母是 `agent` 出现的总次数，不是 `agent learns` 出现的次数。

## 7. N-gram 的两个核心缺陷

### 7.1 数据稀疏性

如果某个词组没有在语料里出现过，N-gram 会把它的概率估成 0。

例如语料只有：

```text
datawhale agent learns
datawhale agent works
```

那么：

```text
P(sleeps | agent) = Count(agent sleeps) / Count(agent) = 0 / 2 = 0
```

但现实中 `agent sleeps` 不一定不可能，只是这个小语料里没见过。

关键区分：

```text
没见过 != 不可能
```

### 7.2 泛化能力差

N-gram 把词当成孤立符号，不理解词和词之间的语义相似关系。

例如它见过：

```text
agent learns
```

但没见过：

```text
robot learns
```

它不会自动意识到 `agent` 和 `robot` 在某些语境里相似，因此不能把 `agent learns` 的经验迁移到 `robot learns`。

关键理解：

> 更大的语料库可以缓解数据稀疏，但不能从根本上解决 N-gram 的泛化问题。因为 N-gram 的表示方式仍然是词面计数，不是语义表示。

## 8. 神经网络语言模型与词嵌入

为了解决 N-gram 把词当孤立符号的问题，神经网络语言模型引入了一个重要想法：

> 用连续向量表示词。

这个向量叫词嵌入，也叫词向量。

直觉上，每个词不再只是一个离散 ID，而是在高维语义空间里的一个点。

例如：

```text
agent 和 robot 距离比较近
agent 和 apple 距离比较远
```

因为 `agent` 和 `robot` 在很多上下文里更相似，而 `apple` 和它们关系更弱。

神经网络语言模型大致做两件事：

1. 把 token 映射成向量，也就是词嵌入。
2. 根据前面 token 的向量，预测下一个 token 的概率分布。

与 N-gram 的区别：

| 模型 | 主要方式 | 局限或优势 |
| --- | --- | --- |
| N-gram | 统计词面搭配 | 难以泛化到没见过但语义相似的表达 |
| 神经网络语言模型 | 学习连续语义表示 | 更容易利用词之间的相似关系做泛化 |

今天纠正的理解：

> 词向量不是显式地先查同义词，再复制经验；而是让语义相似的词在向量空间中表示接近，神经网络因此更容易把相似模式迁移过去。

## 9. 余弦相似度与词向量关系

词被表示成向量后，就可以用数学方法衡量词与词之间的关系。

余弦相似度的直觉：

```text
两个向量方向越接近，语义越相似。
两个向量方向越不相关，语义关系越弱。
```

大致可以理解为：

```text
1   ：方向几乎一样，强相关
0   ：方向接近垂直，关系弱
-1  ：方向相反，负相关
```

例如：

```text
similarity(agent, robot) > similarity(agent, apple)
```

因为 `agent` 和 `robot` 的语义关系可能比 `agent` 和 `apple` 更接近。

经典例子：

```text
vector("King") - vector("Man") + vector("Woman") ≈ vector("Queen")
```

这个例子说明：

> 词向量空间不只表示单词本身，还可能捕捉一些抽象关系，例如性别、身份、类别等语义方向。

注意：

> 这不代表模型像人一样真正理解王室制度，而是说明词向量空间中可以学到某些可计算的语义关系。

## 10. RNN/LSTM：按顺序传递上下文

词向量解决了“词是孤立符号”的问题，但语言还有顺序问题。

N-gram 只看固定窗口。RNN 的想法是：

> 按顺序读文本，并维护一个隐藏状态，把前文信息逐步压缩和传递下去。

隐藏状态可以理解为：

> 模型读到当前为止的上下文摘要。

例如：

```text
我 昨天 去 图书馆 借 了 一本 ...
```

RNN 会按顺序更新状态：

```text
读到“我” -> 状态更新
读到“昨天” -> 状态继续更新
读到“图书馆” -> 状态继续更新
读到“借” -> 状态继续更新
```

到了预测下一个词时，隐藏状态理论上包含前文信息，所以更可能预测出：

```text
书
```

LSTM 是 RNN 的改进版，主要想缓解：

> 普通 RNN 在长句子里容易忘掉很早之前的信息。

今天纠正的理解：

> RNN 不是每次重新读取所有前文，而是按顺序读，并把前文信息压缩进隐藏状态里逐步传递。

## 11. 为什么还需要 Transformer

RNN/LSTM 虽然比 N-gram 更能处理上下文，但仍然有两个明显问题：

| 问题 | 含义 |
| --- | --- |
| 长距离依赖难 | 早期信息要经过很多步传到后面，中途容易衰减或被遗忘 |
| 并行效率低 | 必须按顺序处理 token，很难同时处理整句话 |

Transformer 的核心变化是：

> 不再主要依赖顺序传递隐藏状态，而是用注意力机制，让 token 在上下文窗口内直接关注其他相关 token。

例子：

```text
这本书虽然封面普通，但内容非常精彩，我很喜欢它。
```

当模型处理“它”时，应该能直接关注前面的“这本书”，而不是完全依赖 RNN 一步步传递过来的隐藏状态。

关键理解：

> Transformer 更适合解决长距离依赖和并行计算效率问题，但它不是无限全局理解。它仍然受上下文窗口、训练数据和模型能力限制。

## 12. Transformer 的 Encoder-Decoder 总体结构

经典 Transformer 来自论文《Attention Is All You Need》，总体结构是 Encoder-Decoder：

```text
输入句子 -> Encoder 编码 -> Decoder 解码 -> 输出句子
```

以机器翻译为例：

```text
输入：I love learning agents.
输出：我喜欢学习智能体。
```

Encoder 负责：

> 处理输入句子，生成带上下文关系的表示。

Decoder 负责：

> 根据 Encoder 提供的信息和已有输出，一个 token 一个 token 生成目标句子。

直觉理解：

```text
Encoder：负责理解输入
Decoder：负责生成输出
```

但这里的“理解”不是人类意识意义上的理解，而是：

> 把输入转成一组可计算的上下文向量表示。

## 13. 输入嵌入与位置编码

Transformer 的输入首先要变成向量。

### 13.1 输入嵌入

输入嵌入做的是：

```text
token -> embedding vector
```

模型不能直接处理文字本身，要先把 token 映射成数字向量。

### 13.2 位置编码

Transformer 不像 RNN 那样天然按顺序读 token。它可以并行处理多个 token，所以如果只给 token 向量，模型不知道谁在前、谁在后。

因此需要位置编码告诉模型：

```text
这个 token 在第 1 个位置
这个 token 在第 2 个位置
这个 token 在第 3 个位置
```

通常 Transformer 的真正输入是：

```text
输入嵌入 + 位置编码
```

例子：

```text
我 喜欢 你
你 喜欢 我
```

这两句话包含一样的词，但顺序不同，含义不同。没有位置编码，模型很难区分它们。

关键理解：

> 输入嵌入告诉模型“这个 token 是什么”，位置编码告诉模型“这个 token 在哪里”。

## 14. Self-Attention 自注意力机制

自注意力机制让模型在处理某个 token 时，可以查看同一句子里的其他 token，并判断哪些 token 对当前 token 更重要。

例子：

```text
这本书虽然封面普通，但内容非常精彩，我很喜欢它。
```

当模型处理“它”时，应该重点关注“这本书”相关 token，而不是只关注离它最近的词。

Self-Attention 里的 `self` 指的是：

> 同一个输入序列内部的 token 互相看彼此。

不是说某个 token 只有 Query，另一个 token 只有 Key 或 Value。更准确地说：

> 每个 token 都会生成自己的 Q、K、V。当前 token 用自己的 Q 去匹配上下文中其他 token 的 K，再根据权重汇总它们的 V。

Self-Attention 相比 RNN 的优势：

- 可以在上下文窗口内直接建立远距离 token 关系；
- 不需要所有信息都一步步通过隐藏状态传递；
- 更适合并行计算。

## 15. Q/K/V 的直觉

Q/K/V 是自注意力机制中的三个核心向量。

| 向量 | 全称 | 直觉理解 |
| --- | --- | --- |
| Q | Query | 我现在想找什么信息？ |
| K | Key | 我这里有什么特征，能不能被别人匹配上？ |
| V | Value | 如果别人关注我，我能提供什么内容？ |

每个 token 都会生成自己的 Q、K、V。

从当前 token 的角度看：

```text
当前 token 的 Q -> 匹配其他 token 的 K -> 得到注意力分数
```

然后：

```text
注意力分数 -> 归一化成注意力权重 -> 用权重加权汇总各 token 的 V
```

用“它”和“这本书”的例子：

```text
“它”的 Query：我在找我指代的对象
“这 / 本 / 书”这些 token 的 Key：我可能是一个可被指代的对象
匹配度高 -> 注意力权重高
“这 / 本 / 书”这些 token 的 Value：提供关于“书”的语义信息
```

今天重点纠正的误区：

- Token 不一定等于一个完整单词，也不是一句话。
- 中文里的“这本书”在真实模型里可能被切成 `这 / 本 / 书` 等多个 token。
- 不是“有的 token 只有 Q，有的 token 只有 K，有的 token 只有 V”。
- 每个 token 都同时有 Q、K、V，只是在一次注意力计算里用途不同。

## 16. 注意力分数、注意力权重与 Value

Q 和 K 匹配后，先得到的是：

> 原始相关性分数，也叫匹配分数。

它还不是注意力比例。

流程是：

```text
Q/K 原始匹配分数
-> softmax/归一化
-> 注意力权重
-> 权重乘以各 token 的 V
-> 加权汇总成当前 token 的新上下文表示
```

注意力权重通常加起来是 1，可以理解成当前 token 对上下文中各 token 分配的注意力比例。

例子：

```text
这: 0.10
本: 0.15
书: 0.45
我: 0.05
它: 0.10
其他: 0.15
```

如果“书”的权重是 `0.45`，“我”的权重是 `0.05`，那么“书”的 V 对“它”的新表示影响更大。

关键理解：

> 权重乘以 V，不是在判断 V 好不好，而是在决定从这个 token 的 V 里拿多少信息。

加权汇总后的结果也不是最终答案，而是：

> 当前 token 更新后的上下文表示。

这个表示后续还会经过更多 Transformer 层、前馈网络、归一化等处理，最后才影响输出 token 的概率。

## 17. 今日问答纠偏

今天重点纠正了几个理解：

- 语言模型不是查数据库拿标准答案，而是在上下文中预测 token，因此可能有随机性和幻觉。
- 链式法则中的 `|` 表示 given，也就是在某些条件已经发生时计算概率。
- Bigram 统计的是相邻且有顺序的词对，不能说成简单“同时出现”。
- `Count(agent works)` 和 `Count(works agent)` 不一样，因为顺序不同。
- N-gram 的两个核心缺陷是数据稀疏性和泛化能力差。
- 词向量的泛化不是显式查同义词，而是通过相似语义表示自然迁移。
- 余弦相似度主要比较向量方向是否接近，不是简单比较词面距离。
- RNN 的隐藏状态是上下文摘要，不是每一步重新读完整前文。
- Transformer 可以在上下文窗口内直接建立 token 关系，但不是无限全局理解。
- Encoder 的“理解”是向量表示和模式计算，不是人类意识意义上的理解。
- Token 不一定等于一个词。中文短语可能被切成多个 token。
- 每个 token 都有 Q、K、V，不是不同 token 分别只承担一种身份。
- Q/K 匹配产生的是原始相关性分数，归一化后才是注意力权重。
- 权重乘以 V 的目的，是决定从对应 token 的 Value 中汇总多少信息。

## 18. 下次继续

下次从第三章 3.1.2 继续：

- Multi-Head Attention 多头注意力
- Add & Norm 残差连接与层归一化
- Feed Forward 前馈网络
- Encoder 和 Decoder 内部结构
- Decoder-Only 架构

