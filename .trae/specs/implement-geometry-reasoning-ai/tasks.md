# Tasks

- [x] Task 1: 创建项目基础结构和配置文件
  - [x] SubTask 1.1: 创建项目目录结构
  - [x] SubTask 1.2: 创建requirements.txt依赖文件
  - [x] SubTask 1.3: 创建主模块入口文件
  - [x] 确保测试通过

- [x] Task 2: 实现事件系统（Event System）
  - [x] SubTask 2.1: 实现Event类，包含事件向量（24维）和成功标志
  - [x] SubTask 2.2: 实现EventSequence类，管理事件序列（最大长度64）
  - [x] SubTask 2.3: 实现位置编码
  - [x] 确保测试通过

- [x] Task 3: 实现分词器（Tokenizer）
  - [x] SubTask 3.1: 实现按空格和符号分词的逻辑
  - [x] SubTask 3.2: 实现词汇表（大小300）
  - [x] SubTask 3.3: 实现encode和decode方法
  - [x] 确保测试通过

- [x] Task 4: 实现编码器（Encoder）
  - [x] SubTask 4.1: 实现Transformer编码器结构（2头、1层、24维、FFN 48）
  - [x] SubTask 4.2: 实现输入嵌入层
  - [x] SubTask 4.3: 实现输出层（24维事件向量）
  - [x] 确保测试通过

- [x] Task 5: 实现解码器（Decoder）
  - [x] SubTask 5.1: 实现Decoder-only Transformer结构（2头、1层、24维、FFN 48）
  - [x] SubTask 5.2: 实现自回归生成逻辑
  - [x] SubTask 5.3: 实现输出投影到词汇表
  - [x] 确保测试通过

- [x] Task 6: 实现推理AI（Reasoning AI）
  - [x] SubTask 6.1: 实现Decoder-only Transformer结构（1层、2头、24维、FFN 48）
  - [x] SubTask 6.2: 实现输入构建（历史事件向量序列 + 位置编码）
  - [x] SubTask 6.3: 实现输出层（24维事件向量 + 2维控制信号）
  - [x] 确保测试通过

- [x] Task 7: 实现渲染引擎（Render Engine）
  - [x] SubTask 7.1: 参考numericals.py实现几何图形表示
  - [x] SubTask 7.2: 实现几何图形绘制
  - [x] SubTask 7.3: 实现命题验证逻辑
  - [x] 确保测试通过

- [x] Task 8: 实现符号引擎（Symbolic Engine）
  - [x] SubTask 8.1: 参考dd.py实现演绎数据库
  - [x] SubTask 8.2: 实现命题验证规则
  - [x] SubTask 8.3: 实现枚举验证逻辑
  - [x] 确保测试通过

- [x] Task 9: 实现命题列表管理
  - [x] SubTask 9.1: 实现符号命题列表
  - [x] SubTask 9.2: 实现渲染命题列表
  - [x] SubTask 9.3: 实现命题查询和更新接口
  - [x] 确保测试通过

- [x] Task 10: 实现工作流程
  - [x] SubTask 10.1: 实现主推理循环
  - [x] SubTask 10.2: 实现控制信号处理逻辑
  - [x] SubTask 10.3: 实现终止条件判断
  - [x] 确保测试通过

- [x] Task 11: 实现训练策略
  - [x] 训练时将总参数量调整至0.05M以内（实际44,966参数）
  - [x] SubTask 11.1: 实现编码器-解码器联合训练
  - [x] SubTask 11.2: 实现监督训练流程
  - [x] SubTask 11.3: 实现RL训练流程和奖励计算

- [x] Task 12: 编写测试和文档
  - [x] SubTask 12.1: 编写单元测试
  - [x] SubTask 12.2: 编写集成测试
  - [x] SubTask 12.3: 编写使用示例

# Task Dependencies
- Task 2 依赖于 Task 1
- Task 3 依赖于 Task 1
- Task 4 依赖于 Task 2, Task 3
- Task 5 依赖于 Task 2, Task 3
- Task 6 依赖于 Task 2
- Task 7 依赖于 Task 1
- Task 8 依赖于 Task 1
- Task 9 依赖于 Task 1
- Task 10 依赖于 Task 4, Task 5, Task 6, Task 7, Task 8, Task 9
- Task 11 依赖于 Task 4, Task 5, Task 6, Task 10
- Task 12 依赖于 Task 10, Task 11
