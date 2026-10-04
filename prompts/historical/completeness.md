# 需求完整性评估历史提示词模板

本文件摘录历史配置中的固定提示内容. {{变量}}是数据插入位置, 不是模型实际接收的字面文字.

不附加system消息.

## user消息模板

```text
任务：判断需求集合是否覆盖Checklist中的关键能力大类。以大类为报告单位，不要把单条法规、字段或具体实现方案拆成独立缺失项；证据只引用R编号。只输出JSON。
场景：{{scenario}}
需求：{{requirements紧凑JSON}}
Checklist：{{checklist紧凑JSON}}
输出Schema：{"overall_conclusion":"完整|基本完整|不完整","coverage":[{"check_id":"CAT-...","status":"covered|partial|missing|conditional_missing","evidence":"R编号","rationale":"理由"}],"missing_items":[{"category":"能力大类","related_benchmark":"基准","representative_clauses":["条款组"],"evidence":"R编号","gap":"集合级缺失","severity":"高|中|低","suggested_requirement":"系统应..."}],"not_applicable":["不适用项及理由"]}
```

需求集合和Checklist使用保留中文的紧凑JSON. 输出Schema保留实际调用版本, 不能用后续文件中改写的字段说明替代.
