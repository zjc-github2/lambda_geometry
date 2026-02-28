# 几何题推理AI

## 本项目所有代码均由AI生成

## 项目简介

几何题推理AI是一个基于Transformer架构的几何推理系统，能够理解几何命题并执行推理步骤，验证几何结论的正确性。

## 核心功能

- 几何命题解析与编码
- 基于事件序列的推理过程
- 符号验证与渲染验证双重验证机制
- 完整的推理工作流程
- 可训练的神经网络模型

## 项目结构

```
geometry_reasoning_ai/
├── __init__.py          # 包初始化文件，导出核心组件
├── config.py            # 配置文件，定义模型参数
├── models.py            # 核心模型实现（编码器、解码器、推理AI）
├── workflow.py          # 几何推理系统工作流程
├── geometry_parser.py   # 几何命题解析器
├── symbolic_engine.py   # 符号验证引擎
├── render_engine.py     # 渲染验证引擎
├── proposition_manager.py # 命题管理器
├── event_system.py      # 事件系统
├── tokenizer.py         # 几何语言分词器
├── training.py          # 训练相关代码
├── data_generator.py    # 数据生成器
├── generate_training_data.py # 生成训练数据的脚本
├── generated_training_data.json # 生成的训练数据
└── requirements.txt     # 依赖包列表
```

## 工作原理

几何题推理AI的工作流程如下：

1. **命题输入与编码**：
   - 将几何命题输入系统
   - 使用`Encoder`将命题编码为事件向量
   - 创建初始事件并添加到事件序列中

2. **推理过程**：
   - `ReasoningAI`根据事件序列生成新的事件向量和控制信号
   - 控制信号决定推理策略（是否使用解码器、是否进行渲染验证）
   - `Decoder`将事件向量解码为几何命题

3. **验证机制**：
   - **符号验证**：使用`SymbolicEngine`验证命题的逻辑正确性
   - **渲染验证**：使用`RenderEngine`验证命题的几何正确性
   - 验证结果被记录并影响后续推理

4. **推理终止条件**：
   - 达到目标命题
   - 推理步数达到上限
   - 推理过程出现循环（连续三步产生相同命题）

## 核心组件详解

### 1. 神经网络模型

- **Encoder**：将几何命题编码为向量表示
- **Decoder**：将向量解码为几何命题
- **ReasoningAI**：基于事件序列执行推理，生成新的事件向量和控制信号

### 2. 验证引擎

- **SymbolicEngine**：通过符号逻辑验证命题的正确性
- **RenderEngine**：通过几何渲染验证命题的正确性

### 3. 辅助系统

- **GeometryParser**：解析几何命题，构建命题结构
- **PropositionManager**：管理推理过程中的命题，维护证明状态
- **EventSystem**：管理事件序列，记录推理过程
- **GeometryTokenizer**：将几何命题转换为标记序列

## 技术特点

1. **Transformer架构**：使用Transformer模型处理几何命题的编码和解码
2. **可学习位置编码**：采用可学习的位置编码替代传统的正弦余弦位置编码
3. **控制信号机制**：通过控制信号动态调整推理策略
4. **双重验证**：结合符号验证和渲染验证，提高推理准确性
5. **事件序列管理**：通过事件序列记录推理过程，支持复杂推理

## 模型配置

模型参数经过精心调整，确保总参数量在0.05M以下，适合在普通设备上运行：

- 嵌入维度：24
- 注意力头数：2
- 前馈网络维度：48
- 词汇表大小：300
- 最大序列长度：64
- 编码器/解码器层数：1

## 安装与使用

### 安装依赖

```bash
pip install -r geometry_reasoning_ai/requirements.txt
```

### 基本使用

```python
from geometry_reasoning_ai import GeometryReasoningSystem

# 创建推理系统实例
system = GeometryReasoningSystem()

# 定义初始命题和目标命题
initial_proposition = "在三角形ABC中，AB=AC，D是BC的中点"
target = "AD垂直于BC"

# 运行推理
success, steps = system.run_reasoning(initial_proposition, target)

# 输出推理结果
print(f"推理成功: {success}")
print(f"推理步数: {len(steps)}")

# 打印推理过程
for i, step in enumerate(steps):
    print(f"步骤 {i+1}:")
    print(f"  解码命题: {step.decoded_statement}")
    print(f"  符号验证: {step.symbolic_valid}")
    print(f"  渲染验证: {step.render_valid}")
```

## 训练模型

### 生成训练数据

```bash
python geometry_reasoning_ai/generate_training_data.py
```

### 训练模型

```python
from geometry_reasoning_ai import TrainingPipeline

# 创建训练管道
pipeline = TrainingPipeline()

# 加载训练数据
training_data = pipeline.load_data("geometry_reasoning_ai/generated_training_data.json")

# 开始训练
pipeline.train(training_data, epochs=100)

# 保存模型
pipeline.save_models("models/geometry_reasoning_ai.pth")
```

## 贡献

欢迎通过GitHub提交Issue和Pull Request，共同改进几何题推理AI。
