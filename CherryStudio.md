[TOC]

# CherryStudio

CherryStudio是一个AI智能体，可以通过配置API实现使用不同的语言模型进行思考



## CherryStudio的mcp配置

https://docs.cherry-ai.com/advanced-basic/mcp

MCP 是一种开源协议，旨在以标准化的方式向大型语言模型（LLM）提供上下文信息。

- **类比理解：** 可以把 MCP 想象成 AI 领域的“U盘”。我们知道，U盘可以存储各种文件，插入电脑后就能直接使用。类似地，MCP Server 上可以“插”上各种提供上下文的“插件”，LLM 可以根据需要向 MCP Server 请求这些插件，从而获取更丰富的上下文信息，增强自身能力。

**mcp配置过程**

* 下载后在右下角`设置`，选择`MCP设置`
* 右上角红色警告三角符，点击后安装UV与Bun
* 添加系统内置服务器`@cherry/mcp-auto-install`，`@cherry/fetch`，`@cherry/filesystem`，`@cherry/fetch`和`@cherry/filesystem`能覆盖大多数日常使用场景
* 如有需要可以通过`@cherry/mcp-auto-install`自动添加自定义服务器，或者手动添加



## 针对云雾API配置Claude

[CherryStudio调用cluade MCP - 云雾API 接口对接](https://yunwu.apifox.cn/doc-6458685)

* 打开Cherry Studio，选择`设置 -> 模型服务 -> +添加`
* 名称随意，提供商类型选择Anthropic

| 提供商类型 (provider) | 核心提供商 | 一句话解释                                                   | 关键区别与使用场景                                           | 典型模型                               |
| --------------------- | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------------- |
| **OpenAI**            | OpenAI     | **标准直连**：直接连接到 OpenAI 官方的 API 服务。            | 最常见、最标准的用法。你需要一个 OpenAI 官网的 API Key。适用于绝大多数个人开发者和中小型项目。 | gpt-4-turbo, gpt-3.5-turbo             |
| **Azure OpenAI**      | Microsoft  | **企业级渠道**：通过微软 Azure 云平台使用 OpenAI 的模型。    | 专为企业设计，提供更高的安全性、数据隐私保障和稳定的服务。配置更复杂，需要 Azure 的 Endpoint、Key 和部署名。 | (部署在Azure上的) gpt-4, gpt-3.5-turbo |
| **Gemini**            | Google     | **谷歌的选择**：连接到 Google 的 AI 模型服务。               | Google 的旗舰模型，在多模态（图像、视频理解）和与 Google 生态集成方面有优势。你需要一个 Google Cloud 的 API Key。 | gemini-1.5-pro, gemini-1.0-pro         |
| **Anthropic**         | Anthropic  | **安全与长文本专家**：连接到 Anthropic 公司的 Claude 模型服务。 | 以“宪法AI”带来的安全性著称，并且在处理超长文本（高达200K上下文）方面表现卓越。你需要 Anthropic 官网的 API Key。 | claude-3-opus, claude-3-sonnet         |
| **OpenAI-Response**   | OpenAI     | **特殊用途的 OpenAI**：一个为特定响应格式或API设计的**定制**接口。 | **这不是一个标准名称**。它很可能是 **CherryStudio 为实现特定功能而封装的**。可能用于强制JSON输出、或调用 Assistants API 等。 | gpt-4-turbo 等                         |

* 添加API密钥和API地址（https://yunwu.ai）

* 点击`添加模型`，输入模型ID，模型名称，分组名称即可

* 除此以外在模型服务列表中选择已有模型，如OpenAI，Anthropic等，在更换API密钥和地址以后按需添加模型，也可正常使用



## 模型使用

* 打开会话，选择刚添加的模型
* 下方MCP设置中选中`@cherry/fetch`和`@cherry/filesystem`，即可使用

