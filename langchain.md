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
  from langchain.agents import create_agent
  from langchain_google_genai import ChatGoogleGenerativeAI
  
  # 1. 定义一个工具（Tool）
  def get_weather(city: str) -> str:
      """Get weather for a given city."""
      # 这是一个工具（Tool），Agent 会判断何时调用它。
      # Agent 看到这个工具的 docstring (文档字符串) 后，
      # 知道可以用它来获取天气信息，并把 'sf' 作为 city 参数传入。
      return f"It's always sunny in {city}!"
  
  # 2. 实例化模型，明确指定模型名称
  # LangChain 会自动从环境变量 GOOGLE_API_KEY 中获取密钥
  model_instance = ChatGoogleGenerativeAI(
      model="gemini-2.5-flash"  
  )
  
  # 3. 创建 Agent
  agent = create_agent(
      model=model_instance,  
      tools=[get_weather],
      system_prompt="You are a helpful assistant",
  )
  
  # 4. 运行 Agent
  result = agent.invoke(
      {"messages": [{"role": "user", "content": "what is the weather in sf"}]}
  )
  
  print("Agent 运行结果:")
  print(result)
  ```

- 此时运行 `agent_example.py`，可返回一个非交互的结果。

- 定义系统提示词

  ```python
  # 定义 SYSTEM_PROMPT 环境变量
  SYSTEM_PROMPT = """You are an expert weather forecaster, who speaks in puns.
  
  You have access to two tools:
  
  - get_weather_for_location: use this to get the weather for a specific location
  - get_user_location: use this to get the user's location
  
  If a user asks you for the weather, make sure you know the location. If you can tell from the question that they mean wherever they are, use the get_user_location tool to find their location."""
  
  agent = create_agent(
      model=model_instance,  
      tools=[get_weather],
      # 传入 SYSTEM_PROMPT 环境变量
      system_prompt="SYSTEM_PROMPT",
  )
  ```

- 创建工具

  ```python
  # 导入工具相关的库
  from dataclasses import dataclass
  from langchain.tools import tool, ToolRuntime
  
  # 第一个工具：get_weather_for_location
  @tool
  def get_weather_for_location(city: str) -> str:
      """Get weather for a given city."""
      return f"It's always sunny in {city}!"
  
  # 自定义运行时上下文的 Schema
  @dataclass
  class Context:
      """Custom runtime context schema."""
      user_id: str
  
  # 第二个工具：get_user_location (依赖运行时上下文)
  @tool
  def get_user_location(runtime: ToolRuntime[Context]) -> str:
      """Retrieve user information based on user ID."""
      user_id = runtime.context.user_id
      return "Florida" if user_id == "1" else "SF"
  
  agent = create_agent(
      model=model_instance,
      # 将两个新工具传入
      tools=[get_weather_for_location, get_user_location], 
      system_prompt=SYSTEM_PROMPT, 
  )
  ```

- 配置模型

  ```python
  model_instance = ChatGoogleGenerativeAI(
      model="gemini-2.5-flash",
      # 对应文档中的参数:
      temperature=0.5,  # 控制回复的随机性
      max_output_tokens=1000 # 对应 max_tokens，但 Gemini 使用的参数名是 max_output_tokens
  )
  ```

- **定义响应格式**：可以定义结构化响应格式。

  ```python
  from dataclasses import dataclass
  
  # 定义 Agent 响应格式
  @dataclass
  class ResponseFormat:
      """Response schema for the agent."""
      # A punny response (always required)
      punny_response: str
      # Any interesting information about the weather if available
      weather_conditions: str | None = None
  
  agent = create_agent(
      model=model_instance,
      tools=[get_weather_for_location, get_user_location], 
      system_prompt=SYSTEM_PROMPT, 
      # 传入响应格式定义
      response_format=ResponseFormat,
  )
  ```

- **添加内存**：允许代理记住之前的对话和上下文。

  ```python
  # 导入 checkpointer 库
  from langgraph.checkpoint.memory import InMemorySaver
  
  # 实例化 checkpointer
  checkpointer = InMemorySaver()
  ```

- 创建并运行代理

  ```python
  agent = create_agent(
      model=model_instance,                          
      system_prompt=SYSTEM_PROMPT,
      tools=[get_user_location, get_weather_for_location],
       # [输入结构] 定义 Agent 调用时可接收的额外上下文数据的结构（例如用户 ID）。
      context_schema=Context,
      response_format=ResponseFormat,
      checkpointer=checkpointer
  )
  
  # =================================================================
  # 第一次运行：询问天气 (会触发工具调用)
  # =================================================================
  
  # `thread_id` 是一个唯一标识符，用于 Checkpointer 存储和检索特定的会话历史。
  config = {"configurable": {"thread_id": "1"}}
  
  # 运行 Agent，传入用户消息和配置
  response = agent.invoke(
      {"messages": [{"role": "user", "content": "what is the weather outside?"}]},
      config=config,                                   # 传入会话 ID，让 Agent 知道去哪里加载/存储记忆。
      context=Context(user_id="1")                     # 传入工具所需的运行时上下文数据（用户ID为 "1"）。
  )
  
  # 打印 Agent 最终的结构化回复
  print(response['structured_response']) 
  # 预期输出示例：ResponseFormat(punny_response="...", weather_conditions="...")
  
  # =================================================================
  # 第二次运行：继续会话 (会利用记忆)
  # =================================================================
  
  # 注意：我们使用相同的 `thread_id`，Agent 会自动加载第一次调用的历史记录。
  response = agent.invoke(
      {"messages": [{"role": "user", "content": "thank you!"}]},
      config=config,                                   # 相同 config，继续会话 ID "1" 的历史。
      context=Context(user_id="1")                     # 仍然传入上下文数据。
  )
  
  # 打印 Agent 最终的结构化回复
  print(response['structured_response']) 
  # 预期输出示例：ResponseFormat(punny_response="You're 'thund-erfully' welcome!...", weather_conditions=None)
  ```

- 完整代码

  ```python
  from dataclasses import dataclass
  from langchain.agents import create_agent
  from langchain_google_genai import ChatGoogleGenerativeAI
  from langchain.tools import tool, ToolRuntime
  from langgraph.checkpoint.memory import InMemorySaver
  
  # 系统提示 (System Prompt)
  SYSTEM_PROMPT = """You are an expert weather forecaster, who speaks in puns.
  
  You have access to two tools:
  
  - get_weather_for_location: use this to get the weather for a specific location
  - get_user_location: use this to get the user's location
  
  If a user asks you for the weather, make sure you know the location. If you can tell from the question that they mean wherever they are, use the get_user_location tool to find their location."""
  
  # 运行时上下文的 Schema
  @dataclass
  class Context:
      """Custom runtime context schema."""
      user_id: str
  
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
  
  # 实例化模型 (依赖环境变量 GOOGLE_API_KEY)
  model_instance = ChatGoogleGenerativeAI(
      model="gemini-2.5-flash",
      # 对应文档中的参数:
      temperature=0.5,
      max_output_tokens=1000,
  )
  
  # 定义 Agent 响应格式
  @dataclass
  class ResponseFormat:
      """Response schema for the agent."""
  
      # A punny response (always required)
      punny_response: str
      # Any interesting information about the weather if available
      weather_conditions: str | None = None
  
  # 定义内存存储器：允许代理记住之前的对话和上下文。
  checkpointer = InMemorySaver()
  
  # 创建 Agent
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
  
  # 运行代理示例
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

  