# 几何题推理AI项目 Spec
**训练时把总参数量调整至0.05M以内**

## Why

构建一个能够解几何题的AI系统，通过事件表示和自回归推理生成证明过程。系统以形式化几何命题为输入，利用事件向量表示和自回归推理进行推理，最终由大语言模型整理出完整的证明。

## What Changes

* 实现事件系统：事件向量（1280维）+ 是否成功标志

* 实现分词器：按空格和符号分词，词汇表大小2000

* 实现编码器：Transformer（20头、5层、1280维、FFN 5120）

* 实现推理AI：Decoder-only Transformer（15层、20头、1280维、FFN 5120），输出1282维

* 实现解码器：Decoder-only Transformer（20头、5层、1280维、FFN 5120）

* 实现渲染引擎：类似GeoGebra的图形验证

* 实现符号引擎：类似AlphaGeometry的符号验证

* 实现命题列表管理

* 实现完整的工作流程

* 实现训练策略：编码器-解码器联合训练、监督训练、RL训练(训练时把总参数量调整至0.05M以内)

## Impact

* 参考代码：`d:\代码\入geometry_simple\alphageometry-main\` 目录下的AlphaGeometry实现

* 主要参考文件：

  * `geometry.py` - 几何对象定义

  * `graph.py` - 证明状态图表示

  * `numericals.py` - 数值几何表示和验证

  * `dd.py` - Deductive Database实现

  * `ddar.py` - DD+AR组合实现

  * `lm_inference.py` - 语言模型推理

  * `beam_search.py` - beam search实现

## ADDED Requirements

### Requirement: 事件系统

系统应提供事件表示机制，用于表示推理过程中的每一步。

#### Scenario: 创建事件

* **WHEN** 系统需要表示一个推理步骤

* **THEN** 创建一个包含1280维事件向量和是否成功标志的事件对象

#### Scenario: 事件序列管理

* **WHEN** 推理过程产生多个事件

* **THEN** 系统能够按顺序管理事件序列，支持最大长度512

### Requirement: 分词器

系统应提供针对几何命题的分词功能。

#### Scenario: 分词处理

* **WHEN** 输入几何命题字符串

* **THEN** 按空格和符号（如 `=`、`;`）分词，词汇表大小为2000

### Requirement: 编码器

系统应提供将输入命题转换为事件向量的编码器。

#### Scenario: 命题编码

* **WHEN** 输入几何命题

* **THEN** 输出1280维事件向量

### Requirement: 推理AI

系统应提供自回归的Decoder-only Transformer进行推理。

#### Scenario: 推理步骤生成

* **WHEN** 输入历史事件向量序列M

* **THEN** 输出新的事件向量（1280维）和控制信号（2维）

#### Scenario: 控制信号处理

* **WHEN** 推理AI输出控制信号

* **THEN** 根据信号决定是否使用渲染引擎检查或调用解码器

### Requirement: 解码器

系统应提供将事件向量还原为可读命题的解码器。

#### Scenario: 事件解码

* **WHEN** 输入事件向量

* **THEN** 输出AlphaGeometry格式的几何命题

### Requirement: 渲染引擎

系统应提供类似GeoGebra的图形验证功能。

#### Scenario: 命题验证

* **WHEN** 输入AlphaGeometry格式的命题

* **THEN** 通过几何图形渲染验证命题正确性

### Requirement: 符号引擎

系统应提供类似AlphaGeometry的符号验证功能。

#### Scenario: 符号验证

* **WHEN** 输入命题

* **THEN** 通过枚举方式验证命题可由条件得到

### Requirement: 工作流程

系统应实现完整的推理工作流程。

#### Scenario: 完整推理流程

* **WHEN** 用户输入命题

* **THEN** 系统执行编码、推理、验证、解码等步骤直到得出结论或达到最大步数

### Requirement: 训练策略

系统应支持多种训练策略。

#### Scenario: 编码器-解码器联合训练

* **WHEN** 训练编码器和解码器

* **THEN** 冻结编码器，更新解码器参数

#### Scenario: 监督训练

* **WHEN** 进行监督训练

* **THEN** 根据标准答案计算损失并更新参数

#### Scenario: RL训练

* **WHEN** 进行强化学习训练

* **THEN** 根据推理步骤、验证结果、证明成功等给予奖励

