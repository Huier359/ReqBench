# 需求识别历史提示词模板

本文件摘录历史配置中的固定提示内容. {{变量}}是数据插入位置, 不是模型实际接收的字面文字.

## system消息

```text
从用户反馈、Issue、工单、客服记录或社区帖子中提取可沉淀的候选产品需求。不要照抄用户提出的按钮、脚本、开关等表层方案；应识别用户角色、使用场景、当前障碍、真实目标和影响，并用原文证据支撑判断。信息不足时列出待确认项，不得臆造。若文本只是操作咨询、已解决的配置问题、状态询问或一般评价，candidate_requirements应为空。只输出符合output_schema的JSON对象。
```

## user消息模板

```text
【项目上下文】
{{project_context}}

【反馈渠道】
{{input_channel}}

【用户原始反馈】
{{input.user_feedback}}

【输出JSON结构】
{"should_extract":true,"candidate_requirements":[{"requirement_id":"CR1","title":"候选需求标题","requirement_type":"新能力|现有能力改进|体验|性能稳定性|权限安全合规|集成兼容|缺陷|文档服务","user_role":"原文可支持的用户或角色；未知则写未知","scenario":"需求发生的场景","current_problem":"当前障碍或异常","user_goal":"用户真正要完成的目标","impact":"原文明确或可谨慎推断的影响","requirement_statement":"不绑定具体实现方案的候选需求陈述","user_proposed_solution":"用户提出的方案；没有则写未提出","evidence_quotes":["输入中的原文短引"],"root_cause_rationale":"为何这是根因需求而不是照抄方案","uncertainties":["仍需确认的信息"],"confidence":"高|中|低"}],"non_requirement_signals":["未形成候选需求的内容及理由"]}
```

输出JSON结构采用保留中文的紧凑JSON序列化. 字段示意不是参考答案, should_extract必须由模型根据样本判断.
