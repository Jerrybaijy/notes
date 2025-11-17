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

> [LangChain 文档](https://docs.langchain.com/oss/python/langchain/overview)
>
> [LangChain 参考](https://reference.langchain.com/python/langchain/)

LangChain 的核心价值在于**模块化**，主要组件包括：

- **Models**：提供统一的接口，让你可以轻松切换不同的大模型（如OpenAI、本地模型）。
- **Prompts**：高效地管理提示词模板，使交互更可控。
- **Indexes**：包含文档加载器、文本分割器和向量数据库检索器，专门用于处理外部数据。
- **Chains**：允许你将多个步骤（如提示、模型调用、输出解析）连接成一个完整的“工作链”。
- **Agents**：让大模型具备使用外部工具（如计算器、搜索引擎）的能力，以完成更复杂的任务。
- **Memory**：管理对话历史，实现有上下文的多轮对话。

## 基本实现

- 在项目根目录创建 [Python 虚拟环境](python.md#虚拟环境)并激活。

- 安装必要库

  ```bash
  pip install langchain
  pip install langchain-google-genai
  pip install python-dotenv
  ```

- `.env`

  ```
  # 将 YOUR_API_KEY_HERE 替换为您真实的 Gemini API 密钥
  GEMINI_API_KEY="YOUR_API_KEY_HERE"
  ```

- `app.py`

  ```python
  from langchain.agents import create_agent
  import os
  from dotenv import load_dotenv
  from langchain_google_genai import ChatGoogleGenerativeAI
  
  # ---------------指定模型---------------------
  # 读取 .env 文件并将 GEMINI_API_KEY 加载到环境中
  load_dotenv()
  
  # 读取 API 密钥
  GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")
  
  # 检查 API 密钥是否已加载
  if not GEMINI_API_KEY:
      raise ValueError("GEMINI_API_KEY 未在环境变量中设置。请检查您的 .env 文件。")
  
  # 实例化模型
  model = ChatGoogleGenerativeAI(model="gemini-2.5-flash", google_api_key=GEMINI_API_KEY)
  
  # ----------------定义工具-------------------------
  def get_weather(city: str) -> str:
      """Get weather for a given city."""
      return f"It's always sunny in {city}!"
  
  # ----------------创建代理-------------------------
  agent = create_agent(
      model=model,
      tools=[get_weather],
      system_prompt="You are a helpful assistant",
  )
  
  # ----------------调用代理-------------------------
  result = agent.invoke(
      {"messages": [{"role": "user", "content": "what is the weather in sf"}]}
  )
  
  print(result)
  ```

## 标准实现

- 在项目根目录创建 [Python 虚拟环境](python.md#虚拟环境) 并激活。

- 安装必要库

  ```bash
  pip install -U langchain
  pip install -U langchain-google-genai
  pip install python-dotenv
  ```

- `.env`

  ```
  # 将 YOUR_API_KEY_HERE 替换为您真实的 Gemini API 密钥
  GEMINI_API_KEY="YOUR_API_KEY_HERE"
  ```

- `app.py`

  ```python
  from langchain.agents import create_agent
  import os
  from dotenv import load_dotenv
  from langchain_google_genai import ChatGoogleGenerativeAI
  from langchain.tools import tool, ToolRuntime
  from dataclasses import dataclass
  from langgraph.checkpoint.memory import InMemorySaver
  
  # ---------------定义系统提示语---------------------
  SYSTEM_PROMPT = """你是一位精通双关语的专业天气预报员，请始终使用**中文**回答。
  
  你拥有以下两个工具：
  
  - get_weather_for_location: 用于获取特定地点的天气
  - get_user_location: 用于获取用户当前所在地点
  
  如果用户询问天气，请确保你知道地点。如果用户的问题暗示的是他们当前所在的位置，则使用 get_user_location 工具来查找他们的位置。
  **请注意：你的所有回复都必须是中文的，并且应包含中文的双关语或有趣的谐音梗。**"""
  
  # ---------------指定模型---------------------
  # 读取 .env 文件并将 GEMINI_API_KEY 加载到环境中
  load_dotenv()
  
  # 读取 API 密钥
  GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")
  
  # 检查 API 密钥是否已加载
  if not GEMINI_API_KEY:
      raise ValueError("GEMINI_API_KEY 未在环境变量中设置。请检查您的 .env 文件。")
  
  # 实例化模型
  llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash", google_api_key=GEMINI_API_KEY)
  
  # ---------------定义上下文模式 context_schema---------------------
  @dataclass
  class Context:
      """Custom runtime context schema."""
  
      user_id: str
  
  # ---------------定义响应格式 response_format---------------------
  @dataclass
  class ResponseFormat:
      """Response schema for the agent."""
  
      punny_response: str
      weather_conditions: str | None = None
  
  # ---------------定义内存存储器---------------------
  checkpointer = InMemorySaver()
  
  # 会话标识符
  config = {"configurable": {"thread_id": "1"}}
  
  # ----------------定义工具-------------------------
  @tool
  def get_weather_for_location(city: str) -> str:
      """Get weather for a given city."""
      return f"It's always sunny in {city}!"
  
  @tool
  def get_user_location(runtime: ToolRuntime[Context]) -> str:
      """Retrieve user information based on user ID."""
      user_id = runtime.context.user_id
      return "Florida" if user_id == "1" else "SF"
  
  # ----------------创建代理-------------------------
  agent = create_agent(
      model=llm,
      system_prompt=SYSTEM_PROMPT,
      tools=[get_user_location, get_weather_for_location],
      context_schema=Context,
      response_format=ResponseFormat,
      checkpointer=checkpointer,
  )
  
  # ----------------运行代理-------------------------
  
  # 运行 Agent，传入用户消息和配置
  response = agent.invoke(
      {"messages": [{"role": "user", "content": "今天天气怎么样？"}]},
      config=config,  # 传入会话 ID，让 Agent 知道去哪里加载/存储记忆。
      context=Context(user_id="1"),  # 传入工具所需的运行时上下文数据（用户ID为 "1"）。
  )
  
  # 打印 Agent 最终的结构化回复
  print(response["structured_response"])
  # 预期输出示例：ResponseFormat(punny_response="...", weather_conditions="...")
  
  # 再次运行 Agent，使用相同的 `thread_id`，Agent 会自动加载第一次调用的历史记录。
  response = agent.invoke(
      {"messages": [{"role": "user", "content": "谢谢！"}]},
      config=config,  # 相同 config，继续会话 ID "1" 的历史。
      context=Context(user_id="1"),  # 仍然传入上下文数据。
  )
  
  # 打印 Agent 最终的结构化回复
  print(response["structured_response"])
  # 预期输出示例：ResponseFormat(punny_response="You're 'thund-erfully' welcome!...", weather_conditions=None)
  ```

# Models

[Models](https://docs.langchain.com/oss/python/langchain/models) 是 Agent 的推理引擎。它们驱动智能体的决策过程。LangChain 提供了[上千种模型集成包](https://docs.langchain.com/oss/python/integrations/providers/all_providers)。

模型可以通过两种方式加以利用：

- **独立运行**：可以直接调用模型（在代理循环之外）来执行文本生成、分类或提取等任务，而无需代理框架。
- **使用代理**：通过 Agent 引入。

## 基本实现

下面是一个实现多轮循环问答的模型（无记忆）

```
# 将 YOUR_API_KEY_HERE 替换为您真实的 Gemini API 密钥
GEMINI_API_KEY="YOUR_API_KEY_HERE"
```

```bash
pip install python-dotenv
pip install langchain
pip install langchain-google-genai
```

```python
import os
from dotenv import load_dotenv
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain.agents import create_agent

# 设置 API
load_dotenv()
GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")

# 实例化模型
model = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    api_key=GEMINI_API_KEY
)

# 调用模型 & 多轮问答
while True:
    question = input("用户：")
    response = model.invoke(question)
    print("AI：" + response.content)
    print("=" * 60)
```

## 设置 API

LLM 的 API，此处使用[免费的 Google AI Studio 的 API](https://aistudio.google.com/api-keys)，有两种设置方法：

- 在 `.env` 文件中设置
- 在本地当前环境的终端中设置

### `.env`

```
# 将 YOUR_API_KEY_HERE 替换为您真实的 Gemini API 密钥
GEMINI_API_KEY="YOUR_API_KEY_HERE"
```

```bash
pip install python-dotenv
```

```python
import os
from dotenv import load_dotenv

# 读取 .env 文件并将 GEMINI_API_KEY 加载到环境中
load_dotenv()

# 读取 API 密钥
GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")

# 检查 API 密钥是否已加载，可选。
if not GEMINI_API_KEY:
    raise ValueError("GEMINI_API_KEY 未在环境变量中设置。请检查您的 .env 文件。")
```

**在以上代码中：**

- `GEMINI_API_KEY` 为从 `.env` 文件读取到的 API。
- 不要使用 `gemini-2.5-pro` 模型，以防配额超限。

### 终端加载

```bash
# 设置环境变量
export GOOGLE_API_KEY="YOUR_API_KEY_HERE"

# 检查环境变量，如果返回 API，则代表设置成功。
echo $GOOGLE_API_KEY
```

## 指定模型

指定 Model 有两种方法：

- 初始化模型
- 模型类

### 初始化模型

[**初始化模型**](https://docs.langchain.com/oss/python/langchain/models#initialize-a-model)，即使用 [`init_chat_model`](https://reference.langchain.com/python/langchain/models/?_gl=1*1gysoxw*_gcl_au*NDczNTIxMDkyLjE3NjEzODI3OTI.*_ga*MjE5MjYzNzI5LjE3NjE1NTY1MzU.*_ga_47WX3HKKY2*czE3NjIxMDUzMjYkbzMwJGcxJHQxNzYyMTA1NzA1JGo1NSRsMCRoMA..#langchain.chat_models.init_chat_model) 初始化一个 Model。通常用于 Model 的独立运行，而不是借助 Agent。

```bash
pip install langchain
pip install langchain-google-genai
```

```python
from langchain.chat_models import init_chat_model

# ======================
# 还应该设定 API 密钥等环境变量
# ======================

# 初始化模型
model = init_chat_model(
    model="gemini-2.5-flash",
    api_key=GEMINI_API_KEY,
)

# 调用模型
response = model.invoke("你是谁？")
print(response.content)
```

### 模型类

通过 `ChatGoogleGenerativeAI()` 类实例化一个 Model。

```bash
pip install langchain
pip install langchain-google-genai
```

```python
from langchain.agents import create_agent
from langchain_google_genai import ChatGoogleGenerativeAI

# ======================
# 还应该设定 API 密钥等环境变量
# ======================

# 实例化模型
model = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    api_key=GEMINI_API_KEY
)

# 调用模型
response = model.invoke("你是谁？")
print(response.content) # 我是一个大型语言模型，由 Google 训练。
```

### 本地模型

[Ollama](https://docs.langchain.com/oss/python/integrations/chat/ollama) 允许您在本地运行开源的大型语言模型。

## 调用模型

有三种主要的调用方法，每种方法都适用于不同的使用场景。

- `invoke`
- `stream`
- `batch`

### `invoke`

[`invoke`](https://docs.langchain.com/oss/python/langchain/models#invoke) 是最直接的调用方法。

```python
response = model.invoke("Why do parrots have colorful feathers?")
print(response)
```

### `stream`

[`stream`](https://docs.langchain.com/oss/python/langchain/models#stream) 可以逐步显示输出。

```python
for chunk in model.stream("Why do parrots have colorful feathers?"):
    print(chunk.text, end="|", flush=True)
```

### `batch`

[`batch`](https://docs.langchain.com/oss/python/langchain/models#batch) 将一系列独立的模型请求批量处理，可以显著提高性能并降低成本，因为可以并行处理这些请求：

```python
responses = model.batch([
    "Why do parrots have colorful feathers?",
    "How do airplanes fly?",
    "What is quantum computing?"
])
for response in responses:
    print(response)
```

## 多轮问答

```python
# ======================
# 设定 API，指定模型
# ======================

# 多轮问答
while True:
    question = input("用户：")
    response = model.invoke(question)
    print("AI：" + response.content)
    print("=" * 60)
```

## 多模态

[多模态](https://docs.langchain.com/oss/python/langchain/models#multimodal)，某些模型可以处理并返回**非文本数据**，例如图像、音频和视频。您可以通过提供内容块将非文本数据传递给模型。

```python
response = model.invoke("Create a picture of a cat")
print(response.content_blocks)
# [
#     {"type": "text", "text": "Here's a picture of a cat"},
#     {"type": "image", "base64": "...", "mime_type": "image/jpeg"},
# ]
```

## 模型其它

- [调用 Tools](https://docs.langchain.com/oss/python/langchain/models#tool-calling)
- [结构化输出](https://docs.langchain.com/oss/python/langchain/models#structured-outputs)
- 更多...

# Agents

[Agents](https://docs.langchain.com/oss/python/langchain/agents) 组件用于创建 Agent。让大模型具备使用外部工具（如计算器、搜索引擎）的能力，以完成更复杂的任务。

```mermaid
flowchart TD
    %% 节点
    input([input])
    model{model}
    tools(tools)
    output([output])

    %% 结构
    input --> model
    model -- action --> tools
    tools -- observation --> model
    model -- finish --> output
```

## 基本实现

下面是一个实现多轮循环问答的代理（有记忆）

```
# 将 YOUR_API_KEY_HERE 替换为您真实的 Gemini API 密钥
GEMINI_API_KEY="YOUR_API_KEY_HERE"
```

```
pip install python-dotenv
pip install langchain
pip install langchain-google-genai
```

```python
import os
from dotenv import load_dotenv
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain.agents import create_agent
from langgraph.checkpoint.memory import InMemorySaver

# ---------------指定模型---------------------
# 设置 API
load_dotenv()
GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")

# 实例化模型
model = ChatGoogleGenerativeAI(model="gemini-2.5-flash", api_key=GEMINI_API_KEY)

# ----------------创建代理-------------------------
agent = create_agent(
    model=model,
    checkpointer=InMemorySaver() # 实现记忆
)

# ----------------调用代理 & 多轮问答----------------
while True:
    question = input("用户：")
    response = agent.invoke(
        {"messages": [{"role": "user", "content": question}]},
        {"configurable": {"thread_id": "1"}}, # 实现记忆
    )
    print("AI：" + response["messages"][-1].content)
    print("=" * 60)
```

**在以上代码中：**

- [`create_agent()`](https://reference.langchain.com/python/langchain/agents/?_gl=1*z2ejvz*_gcl_au*NDczNTIxMDkyLjE3NjEzODI3OTI.*_ga*MjE5MjYzNzI5LjE3NjE1NTY1MzU.*_ga_47WX3HKKY2*czE3NjIwODQyMDAkbzI4JGcxJHQxNzYyMDg0MzczJGo2MCRsMCRoMA..#langchain.agents.create_agent)：用于创建 Agent。
- `model=model` ：`model` 为之前创建的实例化模型。

## 静态和动态模型

### 静态模型

[**静态模型**](https://docs.langchain.com/oss/python/langchain/agents#static-model)在创建代理时配置一次，并在整个执行过程中保持不变。详见 Agent 的基本实现。

### 动态模型

[**动态模型**](https://docs.langchain.com/oss/python/langchain/agents#dynamic-model)是基于当前状态以及上下文信息，选择不同的模型。这使得复杂的路由逻辑和成本优化成为可能。

要使用动态模型，使用 [`@wrap_model_call`](https://reference.langchain.com/python/langchain/middleware/#langchain.agents.middleware.wrap_model_call) 装饰器创建中间件，该装饰器会在请求中修改模型：

```python
from langchain_openai import ChatOpenAI
from langchain.agents import create_agent
from langchain.agents.middleware import wrap_model_call, ModelRequest, ModelResponse

basic_model = ChatOpenAI(model="gpt-4o-mini")
advanced_model = ChatOpenAI(model="gpt-4o")

@wrap_model_call
def dynamic_model_selection(request: ModelRequest, handler) -> ModelResponse:
    """Choose model based on conversation complexity."""
    message_count = len(request.state["messages"])

    if message_count > 10:
        # Use an advanced model for longer conversations
        model = advanced_model
    else:
        model = basic_model

    request.model = model
    return handler(request)

agent = create_agent(
    model=basic_model,  # Default model
    tools=tools,
    middleware=[dynamic_model_selection]
)
```

## `context_schema`

`context_schema` 上下文模式，用于定义用户的**元数据**，Agent 在运行时可以识别用户。

```python
from dataclasses import dataclass

# 定义 schema
@dataclass
class Context:
    """Custom runtime context schema.""" 

    user_id: str

# 在定义工具时，传入 schema
@tool
def get_user_location(runtime: ToolRuntime[Context]) -> str:
    """Retrieve user information based on user ID."""
    user_id = runtime.context.user_id
    return "Florida" if user_id == "1" else "SF"

# 传入 Agent
agent = create_agent(
    # ... 其他参数
    context_schema=Context
)

# 在回应时，传入 schema
response = agent.invoke(
    # ... 其它消息和配置
    
    context=Context(user_id="1")
)
```

## `response_format`

`response_format` 响应格式，

```python
# 定义响应格式
@dataclass
class ResponseFormat:
    """Response schema for the agent."""

    punny_response: str
    weather_conditions: str | None = None

# 传入 Agent
agent = create_agent(
    # ... 其他参数
    response_format=ResponseFormat
)
```

# Memory

**记忆系统**能够记住以往交互的信息。

## Short-term Memory

[**Short-term Memory**](https://docs.langchain.com/oss/python/langchain/short-term-memory)（短期记忆）：关注于**单个对话会话**（或“线程”）中的**即时上下文**。它的主要目标是让 LLM 能够记住最近的互动，从而实现流畅、多轮次的对话。

### 基本用法

在创建 Agent 时指定 [`checkpointer`](https://reference.langchain.com/python/langchain/agents/?h=checkpointer#langchain.agents.create_agent(checkpointer)) 属性，在调用 Agent 时使用 `thread_id`。

数据存储在内存中，它只在当前程序运行期间有效。一旦程序结束或重启，这些记忆就会丢失。

```python
from langchain.agents import create_agent
from langgraph.checkpoint.memory import InMemorySaver

# ======================
# 设定 API，指定模型
# ======================

# ----------------创建代理-------------------------
agent = create_agent(
    model=model,
    # 指定 checkpointer 参数
    checkpointer=InMemorySaver()
)

# 调用代理 & 多轮问答
while True:
    question = input("用户：")
    response = agent.invoke(
        {"messages": [{"role": "user", "content": question}]},
        # 指定线程
        {"configurable": {"thread_id": "1"}},
    )
    print("AI：" + response["messages"][-1].content)
    print("=" * 60)
```

**在以上示例中：**

- `checkpointer=InMemorySaver()`：`InMemorySaver` 充当了 Agent 的**记忆存储介质**。它将 Agent 的整个执行历史保存在**内存**中。
- `thread_id`：用于区分会话，告诉 `InMemorySaver` 将当前这次 `invoke` 调用的状态和历史，保存到 ID 为 "1" 的这个特定会话（或线程）中。

### 生产用法

在生产环境中，使用由数据库支持的检查点。

数据存储在数据库中，即使程序崩溃、重启或部署到不同的环境中，记忆也不会丢失。

```bash
pip install langgraph-checkpoint-postgres
```

```python
from langchain.agents import create_agent
from langgraph.checkpoint.postgres import PostgresSaver  

DB_URI = "postgresql://postgres:postgres@localhost:5442/postgres?sslmode=disable"
with PostgresSaver.from_conn_string(DB_URI) as checkpointer:
    checkpointer.setup() # auto create tables in PostgresSql
    agent = create_agent(
        "gpt-5",
        [get_user_info],
        checkpointer=checkpointer,  
    )
```

**在以上示例中：**

- `with 语句`：建立与数据库的连接

### 防止超限

长时间的对话可能会超出 LLM 的上下文窗口。常见的解决方案包括：

- [修剪消息](https://docs.langchain.com/oss/python/langchain/short-term-memory#trim-messages)
- [删除消息](https://docs.langchain.com/oss/python/langchain/short-term-memory#delete-messages)
- [消息摘要](https://docs.langchain.com/oss/python/langchain/short-term-memory#summarize-messages)

### 访问存储器

[**访问存储器**](https://docs.langchain.com/oss/python/langchain/short-term-memory#access-memory)：可以通过多种方式访问和修改智能体的短期记忆（状态）。

## Long-term Memory

[**Long-term Memory**](https://docs.langchain.com/oss/python/langchain/long-term-memory)（长期记忆）：关注**跨会话**和**跨时间**保留信息，让系统能够学习用户偏好、维护用户档案或访问广泛的领域知识。

LangChain 使用 [LangGraph 持久化](https://docs.langchain.com/oss/python/langgraph/persistence#memory-store)来实现长期记忆。

# Messages

[**Messages**](https://docs.langchain.com/oss/python/langchain/messages) 是模型的基本上下文单元。它们代表模型的输入和输出，携带与 LLM 交互时表示对话状态所需的内容和元数据。

## 基本用法

### 文本提示

[**文本提示**](https://docs.langchain.com/oss/python/langchain/messages#text-prompts)是字符串——非常适合简单的生成任务，无需保留对话历史记录。

```python
response = model.invoke("Write a haiku about spring")
```

### 消息提示

[**消息提示**](https://docs.langchain.com/oss/python/langchain/messages#message-prompts)通过提供消息对象列表，将消息列表传递给模型。

```python
from langchain.messages import SystemMessage, HumanMessage, AIMessage

messages = [
    SystemMessage("You are a poetry expert"),
    HumanMessage("Write a haiku about spring"),
    AIMessage("Cherry blossoms bloom...")
]
response = model.invoke(messages)
```

### 字典格式

[**字典格式**](https://docs.langchain.com/oss/python/langchain/messages#dictionary-format)以自动补全格式指定消息。

```python
messages = [
    {"role": "system", "content": "You are a poetry expert"},
    {"role": "user", "content": "Write a haiku about spring"},
    {"role": "assistant", "content": "Cherry blossoms bloom..."}
]
response = model.invoke(messages)
```

## 消息类型

[**消息类型**](https://docs.langchain.com/oss/python/langchain/messages#message-types)：

-  [SystemMessage()](https://docs.langchain.com/oss/python/langchain/messages#system-message)：系统消息，告诉模型如何运行，并为交互提供上下文。
-  [HumanMessage()](https://docs.langchain.com/oss/python/langchain/messages#human-message)：人类消息，代表用户输入以及与模型的交互。
-  [AIMessage()](https://docs.langchain.com/oss/python/langchain/messages#ai-message)：AI 消息，模型生成的响应，包括文本内容、工具调用和元数据。
-  [ToolMessage()](https://docs.langchain.com/oss/python/langchain/messages#tool-message)：工具消息，工具调用的输出。

# Middleware

[**Middleware**](https://docs.langchain.com/oss/python/langchain/middleware)，中间件，提供了一种更严格地控制代理内部运行方式的方法。

> [中间件指南](https://docs.langchain.com/oss/python/langchain/middleware)
>
> [中间件 API 参考](https://reference.langchain.com/python/langchain/middleware/?_gl=1*7nl9a8*_gcl_au*NDczNTIxMDkyLjE3NjEzODI3OTI.*_ga*MjE5MjYzNzI5LjE3NjE1NTY1MzU.*_ga_47WX3HKKY2*czE3NjIxNjg1MDEkbzM2JGcxJHQxNzYyMTcwOTc5JGo0JGwwJGgw)

中间件有以下类型：

- [内置中间件](https://docs.langchain.com/oss/python/langchain/middleware#built-in-middleware)
- [自定义中间件](https://docs.langchain.com/oss/python/langchain/middleware#custom-middleware)
  - [基于装饰器的中间件](https://docs.langchain.com/oss/python/langchain/middleware#decorator-based-middleware)
  - [基于类的中间件](https://docs.langchain.com/oss/python/langchain/middleware#class-based-middleware)

## 基本实现

```python
from langchain.agents import create_agent
from langchain.agents.middleware import SummarizationMiddleware, HumanInTheLoopMiddleware

agent = create_agent(
    model="gpt-4o",
    tools=[...],
    middleware=[SummarizationMiddleware(), HumanInTheLoopMiddleware()],
)
```

**在以上示例中：**

- [`middleware`](https://reference.langchain.com/python/langchain/agents/?_gl=1*z2ejvz*_gcl_au*NDczNTIxMDkyLjE3NjEzODI3OTI.*_ga*MjE5MjYzNzI5LjE3NjE1NTY1MzU.*_ga_47WX3HKKY2*czE3NjIwODQyMDAkbzI4JGcxJHQxNzYyMDg0MzczJGo2MCRsMCRoMA..#langchain.agents.create_agent(middleware))：中间件

## 基于装饰器的中间件

[**基于装饰器的中间件**](https://docs.langchain.com/oss/python/langchain/middleware#decorator-based-middleware)是一种自定义中间件。

```python
from langchain.agents.middleware import before_model, after_model, wrap_model_call
from langchain.agents.middleware import AgentState, ModelRequest, ModelResponse, dynamic_prompt
from langchain.messages import AIMessage
from langchain.agents import create_agent
from langgraph.runtime import Runtime
from typing import Any, Callable

# Node-style: logging before model calls
@before_model
def log_before_model(state: AgentState, runtime: Runtime) -> dict[str, Any] | None:
    print(f"About to call model with {len(state['messages'])} messages")
    return None

# Node-style: validation after model calls
@after_model(can_jump_to=["end"])
def validate_output(state: AgentState, runtime: Runtime) -> dict[str, Any] | None:
    last_message = state["messages"][-1]
    if "BLOCKED" in last_message.content:
        return {
            "messages": [AIMessage("I cannot respond to that request.")],
            "jump_to": "end"
        }
    return None

# Wrap-style: retry logic
@wrap_model_call
def retry_model(
    request: ModelRequest,
    handler: Callable[[ModelRequest], ModelResponse],
) -> ModelResponse:
    for attempt in range(3):
        try:
            return handler(request)
        except Exception as e:
            if attempt == 2:
                raise
            print(f"Retry {attempt + 1}/3 after error: {e}")

# Wrap-style: dynamic prompts
@dynamic_prompt
def personalized_prompt(request: ModelRequest) -> str:
    user_id = request.runtime.context.get("user_id", "guest")
    return f"You are a helpful assistant for user {user_id}. Be concise and friendly."

# Use decorators in agent
agent = create_agent(
    model="gpt-4o",
    middleware=[log_before_model, validate_output, retry_model, personalized_prompt],
    tools=[...],
)
```

## 基于类的中间件

[**基于类的中间件**](https://docs.langchain.com/oss/python/langchain/middleware#class-based-middleware)是一种自定义中间件。

```python
from langchain.agents.middleware import AgentMiddleware, AgentState
from langgraph.runtime import Runtime
from langchain.agents import create_agent
from typing import Any

# 定义基于类的中间件 (LoggingMiddleware)
class LoggingMiddleware(AgentMiddleware):
    """
    这个类实现了两个钩子：before_model 和 after_model。
    它负责在模型调用前后打印日志信息。
    """
    
    # 钩子 1: 在模型调用之前触发
    def before_model(self, state: AgentState, runtime: Runtime) -> dict[str, Any] | None:
        print(f"状态中包含 {len(state['messages'])} 条消息。")
        return None

    # 钩子 2: 在模型调用之后触发
    def after_model(self, state: AgentState, runtime: Runtime) -> dict[str, Any] | None:
        last_message_content = state['messages'][-1].content
        print(f"模型已返回（部分内容）: {last_message_content[:30]}...")
        return None

# 实例化基于类的中间件
logging_instance = LoggingMiddleware() 

agent = create_agent(
    model="gpt-4o",
    middleware=[logging_instance],
)

# 提示：实际运行时，这两个钩子会在 Agent 内部调用 LLM 时自动执行。
print("\nAgent 创建完成。")
print("当 Agent 运行时，LoggingMiddleware 中的 before_model 和 after_model 将自动被调用。")
```

# Prompts

Prompts 用于管理提示词模板，使交互更可控。

```python
SYSTEM_PROMPT = """You are an expert weather forecaster, who speaks in puns.

You have access to two tools:

- get_weather_for_location: use this to get the weather for a specific location
- get_user_location: use this to get the user's location

If a user asks you for the weather, make sure you know the location. If you can tell from the question that they mean wherever they are, use the get_user_location tool to find their location."""

agent = create_agent(
    model=llm,
    # 传入 SYSTEM_PROMPT 组件
    system_prompt=SYSTEM_PROMPT,
    
    # 传入其它组件
)
```

# Tools

[Tools](https://docs.langchain.com/oss/python/langchain/tools) 组件为 Agent 提供各种工具。

```python
from langchain.tools import tool, ToolRuntime

@tool
def get_weather_for_location(city: str) -> str:
    """Get weather for a given city."""
    return f"It's always sunny in {city}!"

SYSTEM_PROMPT = """You are an expert weather forecaster, who speaks in puns.

You have access to two tools:

- get_weather_for_location: use this to get the weather for a specific location
- get_user_location: use this to get the user's location

If a user asks you for the weather, make sure you know the location. If you can tell from the question that they mean wherever they are, use the get_user_location tool to find their location."""
```

**在以上示例中：**

- 使用 [`@tool`](https://reference.langchain.com/python/langchain/tools/#langchain.tools.tool) 装饰器
- `"""Get weather for a given city."""`：默认情况下，函数的文档字符串会成为工具的描述，帮助模型理解何时使用该工具。
- 在提示词中告诉模型，用这个工具干什么。

# Streaming

[Streaming](https://docs.langchain.com/oss/python/langchain/streaming)，流式传输，用于显示各个节点的实时更新，而不是单纯显示最终结果。

# Structured Output

[**Structured output**](https://docs.langchain.com/oss/python/langchain/structured-output)（结构化输出）允许代理以特定且可预测的格式返回数据。

## 基本实现

```python
def create_agent(
    # ...
    response_format: Union[
        ToolStrategy[StructuredResponseT],
        ProviderStrategy[StructuredResponseT],
        type[StructuredResponseT],
    ]
```

# 多轮对话

## 只使用模型的脚本

```bash
pip install langchain
pip install langchain-google-genai
pip install python-dotenv
```

```python
import os
from dotenv import load_dotenv
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.messages import HumanMessage, AIMessage, BaseMessage
from typing import List

# ---------------指定模型---------------------
# 设置 API
load_dotenv()
GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")

# 实例化模型
model = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    api_key=GEMINI_API_KEY
)

# ----------------初始化对话历史-------------------------
# 用于存储完整的对话历史
chat_history: List[BaseMessage] = []

# ----------------运行多轮对话循环-------------------------
def chat_loop():
    """
    运行一个命令行交互循环，实现持续的多轮对话。
    """
    global chat_history
    
    print("--- 🤖 Gemini 命令行聊天助手已启动 ---")
    print("输入您的提问。输入 '退出' 或 'q' 结束会话。")
    
    # 将一个系统指令添加到历史记录的开头，设置 AI 的角色
    system_instruction = "你是一个友好且乐于助人的 AI 助手。请记住用户的上下文和之前的对话。"
    
    # 循环等待用户输入
    while True:
        try:
            # 获取用户输入
            user_input = input("👤 您: ").strip()
            
            # 检查退出命令
            if user_input.lower() in ["退出", "q", "exit", "quit", "exit()"]:
                print("\n👋 谢谢使用，再见！")
                break
                
            if not user_input:
                continue

            # 1. 创建代表当前用户输入的消息
            current_human_message = HumanMessage(content=user_input)
            
            # 2. 构建完整的输入消息列表：历史记录 + 当前输入
            full_messages = chat_history + [current_human_message]
            
            # 3. 调用模型
            # 注意：模型调用是阻塞的，可能需要一些时间
            ai_response_message = model.invoke(full_messages)
            
            # 获取 AI 的文本回复
            ai_response_text = ai_response_message.content
            
            # 4. 打印回复并更新对话历史
            print(f"🤖 AI: {ai_response_text}")
            
            # 将用户的输入添加到历史记录
            chat_history.append(current_human_message)
            # 将 AI 的回复消息添加到历史记录
            chat_history.append(ai_response_message)
            
        except Exception as e:
            print(f"\n❌ 发生了一个错误: {e}")
            print("会话结束。")
            break

# 启动聊天循环
if __name__ == "__main__":
    chat_loop()
```

## 模型+Flask

详见项目：Build a Chatbot in Web Page with Flask & Langchain

<img src="assets/image-20251106230113201.png" alt="image-20251106230113201" style="zoom:50%;" />
