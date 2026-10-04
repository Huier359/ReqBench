# ReqBench提示词模板

本目录提供六类任务的历史提示词模板和独立存放的增强版草案. 仅发布固定指令和输入拼接位置, 不含未公开项目原文, 参考答案, 候选输出, 人工评分, API Key或本机绝对路径.


## 历史任务模板

| 任务 | 文件 | 消息角色 |
| --- | --- | --- |
| 需求补全 | [completion](historical/completion.md) | system + user |
| 需求分解 | [decomposition](historical/decomposition.md) | user |
| 需求完整性评估 | [completeness](historical/completeness.md) | user |
| 需求冲突识别 | [conflict](historical/conflict.md) | system + user |
| 需求识别 | [extraction](historical/extraction.md) | system + user |
| 需求追踪 | [trace](historical/trace.md) | user |

## 使用约定

1. 用对应数据字段替换{{变量}}, 不将占位符直接发送给模型. 保留原文本和数组顺序, 不擅自摘要或截断.
2. 按各模板规定构造system/user消息, 不为仅使用user消息的任务附加通用system指令.
3. 每个样本单轮独立运行. 模板不包含已解答示范, 不显式要求输出内部思考过程. JSON字段示意不是少样本答案.
4. requirements, checklist及output_schema的JSON插入采用保留中文的紧凑序列化. 使用实际发送的Schema版本.
5. 模型版本, 生成参数和数据版本另行冻结记录. 公开模板并不保证模型服务在不同时间返回逐字相同的输出.

## 已核对的历史生成配置

| 任务 | temperature | max_tokens | max_retries |
| --- | ---: | ---: | ---: |
| 需求补全 | 0 | 16000 | 2 |
| 需求分解 | 0 | 16000 | 2 |
| 需求完整性评估 | 0 | 16000 | 2 |
| 需求冲突识别 | 0 | 10000 | 0 |
| 需求识别 | 0 | 16000 | 0 |
| 需求追踪 | 0 | 16000 | 0 |

以上配置来自历史完成批次, 不含早期停止的试运行. 历史请求使用JSON对象响应模式和stream=false. API供应方是否支持参数及模型内部推理配置, 应以具体调用记录为准.
