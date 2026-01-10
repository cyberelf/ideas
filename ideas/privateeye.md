# PrivateEye - 本地化 AI 驱动的个人隐私泄露审计与溯源工具

## Idea Overview

PrivateEye 是一个完全本地化的个人隐私泄露监控 Agent，通过 CLI 输入脱敏个人信息后，自动在全球范围内的数据泄露通知（如 Have I Been Pwned）、暗网监控接口、GitHub 敏感信息泄露中进行巡检。其核心安全特性是使用本地小模型（Llama-3-8B/Phi-4，16GB 内存即可运行）对抓取到的数据进行模糊匹配和关联分析，用户敏感数据无需上传至任何云端服务。

## Background Research

**现有解决方案分析：**

- **Have I Been Pwned** ([链接](https://haveibeenpwned.com/)) - 最流行的数据泄露查询服务，需上传邮箱等信息到云端
- **商业监控服务**：Breachsense、1Password Dark Web Monitoring、NordStellar 等提供持续的暗网监控，但均为订阅制云服务
- **GitHub 敏感信息监控工具**：
  - [GSIL](https://github.com/FeeiCN/GSIL) - Python 开源工具，基于规则匹配
  - [GShark](https://github.com/0xbug/GShark) - Go + Vue 可视化工具
  - [VIPKID GitHub Monitor](https://github.com/vipkid/github-monitor) - 企业级方案

**现有方案的局限性：**
1. **隐私悖论**：为了检查信息是否泄露，必须把信息交给第三方服务
2. **被动通知**：大多仅告知"已泄露"，缺乏溯源分析
3. **规则局限**：基于关键词/正则的匹配容易漏检或误报
4. **数据孤岛**：各服务独立，缺乏统一关联分析

**PrivateEye 的差异化优势：**
1. **隐私优先**：所有敏感数据处理均在本地完成，零数据外传
2. **AI 增强匹配**：利用本地 LLM 进行语义理解和模糊匹配，降低误报
3. **多源聚合**：整合泄露数据库、暗网、GitHub 等多维度信息源
4. **溯源分析**：不仅告知"泄露了"，还分析"如何泄露"和"泄露源头"

## Detailed Description

**解决的核心问题：**
在数字化时代，个人信息泄露已成为电信诈骗、身份盗用等犯罪的主要温床。现有监控服务存在一个根本性矛盾——用户为了"保护隐私"必须先"交出隐私"。PrivateEye 打破这一悖论，提供真正隐私安全的泄露监控方案。

**解决方案：**
1. **本地 Agent 架构**：用户通过 CLI 输入脱敏信息（如部分邮箱、手机号片段、用户名等），Agent 在本地环境运行
2. **多源数据采集**：自动抓取 Have I Been Pwned 公开数据、暗网泄露情报、GitHub 敏感信息等公开渠道
3. **本地 AI 分析**：使用 Llama-3-8B 或 Phi-4 等小模型（16GB 内存可运行）在本地进行：
   - 模糊匹配：识别变形、部分遮挡的敏感信息
   - 关联分析：跨数据源发现关联泄露事件
   - 溯源推理：推断可能的泄露源头和时间线
4. **CLI 输出报告**：生成详细的泄露审计报告，包括泄露事件、风险评级、建议措施

**为什么这个方案有价值：**
- **零信任架构**：用户敏感信息永不离开本地设备
- **智能匹配**：AI 理解上下文，减少规则匹配的盲点
- **溯源能力**：帮助用户理解泄露路径，从根本上防范

## Expected Outcomes

**用户价值：**
- 个人用户可获得企业级隐私监控能力，无需向第三方暴露敏感信息
- 清晰了解自己的信息如何泄露，从源头加强防护
- 开源免费，相比商业服务节省每年数百元订阅费

**技术创新：**
- 探索本地小模型在隐私审计场景的应用边界
- 构建隐私优先的 Agent 系统设计模式
- 多源异构数据的本地化关联分析方法

**社会影响：**
- 降低个人隐私监控门槛，提升全民隐私保护意识
- 为开源社区贡献首个真正本地化的隐私审计工具
- 推动隐私计算技术在个人场景的应用落地

## Suggested Tech Stack

- **AI/ML**:
  - Llama-3-8B-Instruct 或 Phi-4 (本地推理)
  - Ollama / llama.cpp (模型运行时)
  - LangChain / CrewAI (Agent 编排)

- **Backend**:
  - Python 3.10+
  - FastAPI (CLI 服务接口)
  - aiohttp (异步数据采集)

- **数据源集成**:
  - Have I Been Pwned API (仅获取公开泄露事件列表)
  - GitHub Search API (公开仓库扫描)
  - 暗网情报源 (TOR + 公开泄露索引)

- **前端/交互**:
  - Rich / Typer (美观的 CLI 界面)
  - 可选：TUI (Textual) 提供交互式界面

- **其他**:
  - SQLite (本地缓存和索引)
  - 定时任务 (schedule/apscheduler)

## References

- [Have I Been Pwned API](https://haveibeenpwned.com/API/v3)
- [GSIL - GitHub Sensitive Information Leakage](https://github.com/FeeiCN/GSIL)
- [GShark - GitHub敏感信息搜集工具](https://github.com/0xbug/GShark)
- [Local AI Agents: A Privacy-First Alternative](https://gloriumtech.com/local-ai-agents-the-privacy-first-alternative-to-cloud-based-ai/)
- [AudAgent - Local Privacy Protection for AI](https://arxiv.org/html/2511.07441)
- [Privacy-First AI Agents in 2025](https://blog.shinkai.com/privacy-first-ai-agents-in-2025-why-it-matters-and-where-it-matters-most/)

## Contributors

- [@cyberelf] - Idea Author
