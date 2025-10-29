---
title: langchain
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - ai
  - ai-agent
  - framework
---

# LangChain

[LangChain](https://docs.langchain.com/oss/python/langchain/overview) 是一个应用框架，旨在简化使用大型语言模型的应用程序。

LangChain 的核心价值在于**模块化**，主要组件包括：

- **Models**：提供统一的接口，让你可以轻松切换不同的大模型（如OpenAI、本地模型）。
- **Prompts**：高效地管理提示词模板，使交互更可控。
- **Indexes**：包含文档加载器、文本分割器和向量数据库检索器，专门用于处理外部数据。
- **Chains**：允许你将多个步骤（如提示、模型调用、输出解析）连接成一个完整的“工作链”。
- **Agents**：让大模型具备使用外部工具（如计算器、搜索引擎）的能力，以完成更复杂的任务。
- **Memory**：管理对话历史，实现有上下文的多轮对话。

## 基本构建

- 在项目根目录创建 [Python 虚拟环境](python.md#虚拟环境)。

- 安装 LangChain Agent 核心库

  ```bash
  pip install -U langchain
  ```

- 安装 Google Gemini 集成库

  ```bash
  pip install langchain-google-genai
  ```

- 准备大模型 API，此处使用免费的 [Google AI Studio 的 API](https://aistudio.google.com/api-keys)。

- 设置环境变量

  ```bash
  # 设置环境变量
  export GOOGLE_API_KEY="替换为此前申请的 Google API"

  # 检查环境变量，如果返回 API，则代表设置成功。
  echo $GOOGLE_API_KEY
  ```

- 创建 `agent_example.py` 文件

  ```python
  from dataclasses import dataclass
  from langchain.agents import create_agent
  from langchain_google_genai import ChatGoogleGenerativeAI
  from langchain.tools import tool, ToolRuntime
  from langgraph.checkpoint.memory import InMemorySaver
  
  # ==================================================
  # 系统提示
  # ==================================================
  
  SYSTEM_PROMPT = """You are an expert weather forecaster, who speaks in puns.
  
  You have access to two tools:
  
  - get_weather_for_location: use this to get the weather for a specific location
  - get_user_location: use this to get the user's location
  
  If a user asks you for the weather, make sure you know the location. If you can tell from the question that they mean wherever they are, use the get_user_location tool to find their location."""
  
  # ==================================================
  # 运行时上下文的 Schema
  # ==================================================
  
  @dataclass
  class Context:
      """Custom runtime context schema."""
  
      user_id: str
  
  # ==================================================
  # 定义工具
  # ==================================================
  
  # 第一个工具：get_weather_for_location
  @tool
  def get_weather_for_location(city: str) -> str:
      """Get weather for a given city."""
      return f"It's always sunny in {city}!"
  
  # 第二个工具：get_user_location (依赖运行时上下文)
  @tool
  def get_user_location(runtime: ToolRuntime[Context]) -> str:
      """Retrieve user information based on user ID."""
      user_id = runtime.context.user_id
      return "Florida" if user_id == "1" else "SF"
  
  # ==================================================
  # 实例化模型 (依赖环境变量 GOOGLE_API_KEY)
  # ==================================================
  model_instance = ChatGoogleGenerativeAI(
      model="gemini-2.5-flash",
      # 对应文档中的参数:
      temperature=0.5,
      max_output_tokens=1000,
  )
  
  # ==================================================
  # 定义 Agent 响应格式
  # ==================================================
  
  @dataclass
  class ResponseFormat:
      """Response schema for the agent."""
  
      # A punny response (always required)
      punny_response: str
      # Any interesting information about the weather if available
      weather_conditions: str | None = None
  
  # ==================================================
  # 定义内存存储器：允许代理记住之前的对话和上下文。
  # ==================================================
  
  checkpointer = InMemorySaver()
  
  # ==================================================
  # 创建 Agent
  # ==================================================
  
  agent = create_agent(
      model=model_instance,
      system_prompt=SYSTEM_PROMPT,
      tools=[get_user_location, get_weather_for_location],
      # [输入结构] 定义 Agent 调用时可接收的额外上下文数据的结构（例如用户 ID）。
      context_schema=Context,
      # 传入响应格式类
      response_format=ResponseFormat,
      # 传入内存存储器
      checkpointer=checkpointer,
  )
  
  # ==================================================
  # 运行代理示例
  # ==================================================
  
  # `thread_id` 是一个唯一标识符，用于 Checkpointer 存储和检索特定的会话历史。
  config = {"configurable": {"thread_id": "1"}}
  
  # 运行 Agent，传入用户消息和配置
  response = agent.invoke(
      {"messages": [{"role": "user", "content": "what is the weather outside?"}]},
      config=config,  # 传入会话 ID，让 Agent 知道去哪里加载/存储记忆。
      context=Context(user_id="1"),  # 传入工具所需的运行时上下文数据（用户ID为 "1"）。
  )
  
  # 打印 Agent 最终的结构化回复
  print(response["structured_response"])
  # 预期输出示例：ResponseFormat(punny_response="...", weather_conditions="...")
  
  # 注意：我们使用相同的 `thread_id`，Agent 会自动加载第一次调用的历史记录。
  response = agent.invoke(
      {"messages": [{"role": "user", "content": "thank you!"}]},
      config=config,  # 相同 config，继续会话 ID "1" 的历史。
      context=Context(user_id="1"),  # 仍然传入上下文数据。
  )
  
  # 打印 Agent 最终的结构化回复
  print(response["structured_response"])
  # 预期输出示例：ResponseFormat(punny_response="You're 'thund-erfully' welcome!...", weather_conditions=None)
  ```
