# 什么是推理大语言模型？

推理大语言模型是一类在回答问题前会进行自主思考的模型，例如 deepseek-r1、gpt-o1 和 gemini-thinking。其思考过程通常用 `<think> {thinking_process} </think>` 包裹。

# 推理大语言模型的使用技巧

- **在 deepseek-r1 中避免使用 system prompt**：deepseek 在官方使用建议[^1]中明确指出：“Avoid adding a system prompt; all instructions should be contained within the user prompt.” 相比之下，OpenAI[^2] 使用了 “developer message” 来代替 “system message”，但依然支持系统提示词。
  
- **将 deepseek-r1 的 temperature 设置为 0.6**：官方建议将 temperature 设置在 0.5 到 0.7 之间（推荐值为 0.6），以防止出现无休止的重复或不连贯的输出。

- **找到适合当前 prompt 的输出格式**：已有多篇研究探讨了输出格式对非推理大语言模型表现的影响。可以确定的是，固定某种输出格式（如 JSON 或 YAML）会在一定程度上降低模型的智能。deepseek 在其官方文档中建议：“For mathematical problems, it is advisable to include a directive in your prompt such as: 'Please reason step by step, and put your final answer within \boxed{}.'” 同样，OpenAI 也提到：“Starting with `o1-2024-12-17`, reasoning models in the API will avoid generating responses with markdown formatting.”

- **避免在提示词中使用“思维链”（CoT）类似的词汇**：因为思维链是推理大语言模型的内在能力，在用户提示中提及是没有必要的。

- **先使用 zero-shot，再尝试 few-shot**：推理模型在理解问题和指令时具有较强的能力，通常 zero-shot 会取得较好的效果。如果确实需要使用 few-shot，确保示例与指令高度相关。

- **提示词结构要清晰**：使用如 markdown 标题或 XML 标签等方式来结构化提示词，有助于提高模型的理解和响应质量。比如 # persona, # background information, # task description, # shots, # objective。

- **用清晰的语句表达任务目标**：先用常规大语言模型完善提示词，再将其输入推理大语言模型，以确保任务目标明确。

# Footnotes

[^1]: https://github.com/deepseek-ai/DeepSeek-R1?tab=readme-ov-file#usage-recommendations
[^2]: https://platform.openai.com/docs/guides/reasoning-best-practices