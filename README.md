# ReqBench Public Inputs

ReqBench是一个面向需求工程的大语言模型多任务评测基准。本仓库公开6类任务的270条匿名化模型输入，每类任务包含45条样本，其中L1（低）、L2（中）、L3（高）各15条。

## 任务与文件

| 任务 | 文件 | 样本数 | L1/L2/L3 |
|---|---|---:|---:|
| 需求补全 | [`json/requirements_completion.json`](json/requirements_completion.json) | 45 | 15/15/15 |
| 需求分解 | [`json/requirements_decomposition.json`](json/requirements_decomposition.json) | 45 | 15/15/15 |
| 需求冲突识别 | [`json/requirements_conflict_identification.json`](json/requirements_conflict_identification.json) | 45 | 15/15/15 |
| 需求完整性评估 | [`json/requirements_completeness_assessment.json`](json/requirements_completeness_assessment.json) | 45 | 15/15/15 |
| 需求抽取 | [`json/requirements_extraction.json`](json/requirements_extraction.json) | 45 | 15/15/15 |
| 需求追踪 | [`json/requirements_traceability.json`](json/requirements_traceability.json) | 45 | 15/15/15 |

完整数据见[`json/reqbench_public_270.json`](json/reqbench_public_270.json)。

## 提示词模板

六类任务的完整历史提示词模板、消息角色、输入拼接约定及历史调用参数见[`prompts/README.md`](prompts/README.md)。模板保留历史实验中的固定指令，样本内容通过占位符插入。

另提供独立的[增强版提示词草案](prompts/experimental/v2-draft.md)，明确标注其未用于既有实验且尚未验证效果。历史模板与增强版不能混用来解释已有分数。历史配置与本次投稿最终样本的对应关系仍需核对，详见提示词目录的版本边界说明。

## JSON结构

每个文件都是标准JSON数组。单条样本包含以下字段：

- `sample_id`：公开版独立样本编号；
- `task`、`task_name_zh`：任务标识及中文名称；
- `difficulty`、`difficulty_zh`：L1/L2/L3及对应中文难度；
- `model_input`：模型实际可见的匿名化任务输入。

```python
import json

with open("json/reqbench_public_270.json", encoding="utf-8") as f:
    samples = json.load(f)

print(len(samples))  # 270
```

## 隐私与评价边界

公开数据不包含项目名称、项目编号、项目对应关系、原样本编号、金标准、参考答案、评分结果、模型输出、内部证据定位和源文件路径。输入中原有的项目名称已统一替换为“目标系统”。详见[`DATA_CARD.md`](DATA_CARD.md)和[`EVALUATION.md`](EVALUATION.md)。

## 许可证

本仓库暂未附加开源许可证；许可证由仓库维护者在正式发布时确定。
