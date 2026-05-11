RAG 智能问答系统

📖 项目简介

RAG 智能问答系统是一个完整的端到端检索增强生成（Retrieval-Augmented Generation）解决方案，基于 LangChain 和 LangGraph 构建。系统提供现代化的前端聊天界面和高性能的 FastAPI 后端，能够基于自定义知识库提供准确、可溯源的智能回答。

本项目适用于企业知识库、文档检索、客服对话、教育辅助等多种场景，具备完整的文档管理、智能检索、多轮对话和来源追溯功能。

✨ 核心功能

🎯 智能问答引擎
基于知识库的精准回答：严格基于检索到的文档内容生成回答，减少幻觉
多轮对话支持：自动维护对话历史，支持上下文理解
查询重写优化：基于对话历史智能重写用户查询，提升检索准确性
指代消解：理解代词和上下文引用，提升对话流畅度

📚 文档管理系统
批量文档索引：支持一次性索引多个文档
智能文本分割：使用 RecursiveCharacterTextSplitter 进行智能分块
元数据管理：支持文档来源、主题等元数据标注
向量化存储：使用 OpenAI Embeddings 进行文本向量化
内存向量存储：高效的相似度检索

🔍 检索增强功能
相似度检索：基于向量相似度的 Top-K 文档检索
可配置检索参数：支持调整检索数量和策略
实时检索：毫秒级响应速度
上下文构建：自动整合检索结果生成上下文

📊 来源追溯系统
引用文档展示：清晰显示每个回答引用的文档来源
内容预览：提供检索文档的内容预览
元数据可视化：展示文档的元信息（来源、主题等）
可信度标注：帮助用户判断信息可靠性

📈 置信度评估机制
自动生成置信度：基于上下文相关性评估回答质量（0-1分）
严格评分标准：
  1.0：完全基于上下文，信息准确完整
  0.8：主要基于上下文，少量合理补充
  0.6：部分基于上下文，包含外部知识
  0.4：少量基于上下文，主要依赖外部知识
  0.2：几乎不基于上下文
  0.0：与上下文无关或错误
可视化展示：高/中/低三档置信度颜色标识

💬 对话管理系统
自动历史维护：自动保存用户和助手的对话记录
历史查看：提供 API 查询对话历史
历史清除：支持清除对话历史开始新对话
上下文感知：仅使用最近4轮对话进行上下文理解

🔧 系统管理功能
健康检查：实时监控 API 状态
统计信息：查询次数、平均置信度、最后查询时间等
系统重置：一键重置整个系统状态
文档统计：已索引文档数量统计

🛠️ 技术栈

后端技术
FastAPI - 高性能 Web 框架
LangChain - LLM 应用开发框架
LangGraph - 状态化工作流引擎
Uvicorn - ASGI 服务器
Pydantic - 数据验证和序列化

核心组件
OpenAI Embeddings - 文本向量化（支持智谱AI）
InMemoryVectorStore - 内存向量存储
RecursiveCharacterTextSplitter - 智能文本分割
ChatOpenAI - 语言模型接口（支持 GLM-4-Flash）

前端技术
HTML5/CSS3 - 现代化界面
JavaScript (ES6+) - 交互逻辑
Font Awesome - 图标库
纯前端实现 - 无框架依赖，轻量级

开发工具
python-dotenv - 环境变量管理
CORS Middleware - 跨域资源共享

📦 项目结构

rag-qa-system/
├── main.py                    # FastAPI 主应用和 API 端点
├── rag_system.py              # RAG 核心引擎实现
├── frontend/
│   └── index.html            # 前端聊天界面
├── .env.example              # 环境变量示例
├── requirements.txt          # Python 依赖
├── Dockerfile                # Docker 配置
├── README.md                 # 项目文档
└── LICENSE                   # 许可证

🚀 快速开始

环境准备

克隆项目
git clone https://github.com/yourusername/rag-qa-system.git
cd rag-qa-system

创建虚拟环境
python -m venv venv
source venv/bin/activate  # Windows: venvScriptsactivate

安装依赖
pip install -r requirements.txt

配置环境变量

创建 .env 文件，配置 API 密钥：

智谱AI 配置（推荐）
ZHIPUAI_API_KEY=your_zhipu_api_key_here
ZHIPUAI_BASE_URL=https://open.bigmodel.cn/api/paas/v4/

或使用 OpenAI
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_BASE_URL=https://api.openai.com/v1

可选：Tavily 搜索 API（用于扩展检索）
TAVILY_API_KEY=your_tavily_api_key_here

启动后端服务

启动 FastAPI 服务器
python main.py

或使用 uvicorn 命令
uvicorn main:app --host 0.0.0.0 --port 8000 --reload

服务启动后，访问以下地址：
📄 API 文档: http://localhost:8000/docs
📖 ReDoc: http://localhost:8000/redoc
🔍 健康检查: http://localhost:8000/health

访问前端界面

打开 frontend/index.html 文件，或使用本地服务器：

使用 Python 内置服务器
python -m http.server 8080

然后访问 http://localhost:8080/frontend/index.html

📝 使用指南

基本操作流程

系统初始化
   后端启动时自动索引示例文档
   或手动调用 /index/sample 端点重新索引

开始问答
   在前端输入框输入问题
   点击发送按钮或按 Enter 键
   系统返回答案、来源引用和置信度

多轮对话
   系统自动维护对话历史
   后续问题可引用前文内容
   支持指代消解（如"它"、"这个"等）

管理对话
   查看对话历史：访问 /history 端点
   清除历史：点击前端清除按钮或调用 DELETE /history

API 使用示例

健康检查
curl http://localhost:8000/health

响应示例:
{
  "status": "healthy",
  "rag_initialized": true,
  "document_count": 4,
  "timestamp": "2026-05-11T17:17:00"
}

索引示例文档
curl -X POST http://localhost:8000/index/sample

响应示例:
{
  "success": true,
  "document_count": 4,
  "chunk_count": 12,
  "message": "成功索引 4 个示例文档"
}

发送查询
curl -X POST http://localhost:8000/query \
  -H "Content-Type: application/json" \
  -d '{
    "question": "什么是 LangChain？",
    "use_history": true
  }'

响应示例:
{
  "answer": "LangChain 是一个用于开发大型语言模型（LLM）应用的开源框架...",
  "sources": [
    {
      "index": 1,
      "source": "langchain_intro.txt",
      "content_preview": "LangChain 简介nnLangChain 是一个用于开发大型语言模型..."
    }
  ],
  "confidence": 0.92,
  "timestamp": "2026-05-11T17:17:30"
}

获取对话历史
curl http://localhost:8000/history

清除历史
curl -X DELETE http://localhost:8000/history

索引新文档
curl -X POST http://localhost:8000/index \
  -H "Content-Type: application/json" \
  -d '{
    "documents": [
      {
        "text": "这是文档内容...",
        "metadata": {
          "source": "custom_doc.txt",
          "topic": "custom"
        }
      }
    ]
  }'

获取系统统计
curl http://localhost:8000/stats

响应示例:
{
  "total_queries": 15,
  "average_confidence": 0.85,
  "last_query_time": "2026-05-11T17:17:30"
}

重置系统
curl -X POST http://localhost:8000/reset

🔧 配置说明

RAG 配置参数

在 rag_system.py 中的 RAGConfig 类定义了系统配置：

RAGConfig(
    # 生成参数
    temperature=0.2,        # 生成随机性（0-1），值越低越确定
    max_tokens=1000,        # 最大生成长度
    
    # 文档处理
    chunk_size=500,         # 文本分块大小（字符数）
    chunk_overlap=100,      # 分块重叠大小（字符数）
    
    # 检索参数
    top_k=3,                # 检索文档数量
    search_type="similarity" # 检索方式
)

可调优参数说明
参数   说明   建议值范围   默认值
temperature   生成随机性，控制输出多样性   0.1-0.7   0.2

max_tokens   单次生成的最大 token 数量   500-2000   1000

chunk_size   文档分块大小，影响检索精度   300-1000   500

chunk_overlap   分块重叠大小，保证上下文连贯   50-200   100

top_k   检索返回的文档数量   2-5   3

环境变量配置
变量名   说明   必填   示例
ZHIPUAI_API_KEY   智谱AI API 密钥   是（二选一）   1a7f60f0...

ZHIPUAI_BASE_URL   智谱AI API 地址   是（二选一）   https://open.bigmodel.cn/api/paas/v4/

OPENAI_API_KEY   OpenAI API 密钥   是（二选一）   sk-...

OPENAI_BASE_URL   OpenAI API 地址   否   https://api.openai.com/v1

TAVILY_API_KEY   Tavily 搜索 API 密钥   否   tvly-...

🎨 前端界面特性

界面设计
🎯 现代化聊天界面：渐变色主题，圆角设计，阴影效果
📱 响应式布局：完美适配移动端和桌面端
✨ 流畅动画：消息淡入、图标脉动、按钮悬停效果
🎨 配色方案：蓝色主题，符合科技感

交互功能
💬 实时消息显示：用户和 AI 消息区分显示
📊 置信度可视化：高（绿色）、中（橙色）、低（红色）三档
📚 来源引用展示：清晰展示引用文档和内容预览
⏳ 加载状态指示：AI 思考时显示加载动画
🔌 API 连接状态：实时显示后端连接状态
📝 自动高度调整：输入框根据内容自动调整高度

用户体验优化
⌨️ 快捷键支持：Enter 发送，Ctrl+Enter 换行
🎯 自动聚焦：页面加载后自动聚焦输入框
📈 平滑滚动：消息滚动流畅自然
❌ 错误提示：友好的错误信息展示

📊 工作流程

系统架构图

┌─────────────────────────────────────────────────────────────┐
│                         前端界面                             │
│                    (HTML/JavaScript)                        │
└──────────────────────────┬──────────────────────────────────┘
                           │ HTTP/JSON
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                      FastAPI 后端                            │
│                    (RESTful API)                            │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    RAG 核心引擎                              │
│              (LangChain + LangGraph)                        │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │  文档处理   │  │   检索器    │  │   生成器    │         │
│  │ Processor   │─▶│  Retriever  │─▶│  Generator  │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    向量存储                                  │
│              (InMemoryVectorStore)                          │
└─────────────────────────────────────────────────────────────┘

详细处理流程

用户提问
   前端接收用户输入
   发送 POST /query 请求

查询处理
   检查对话历史
   基于历史重写查询（如需要）
   优化检索关键词

文档检索
   向量相似度搜索
   返回 Top-K 相关文档
   构建上下文信息

回答生成
   结合上下文和对话历史
   调用 LLM 生成回答
   格式化输出

质量评估
   计算置信度分数
   验证回答准确性
   标注来源信息

返回结果
   返回答案、来源、置信度
   保存对话历史
   更新统计信息

🧪 示例对话

单轮问答示例

用户: 什么是 LangChain？

助手: LangChain 是一个用于开发大型语言模型（LLM）应用的开源框架。
它提供了一套标准化的接口和工具，帮助开发者快速构建基于 LLM 的应用程序。

主要特点：
模块化设计：所有组件都可以独立使用或组合使用
链式调用：支持将多个组件链接在一起形成复杂的工作流
记忆管理：内置多种记忆类型，支持对话历史管理
工具集成：可以轻松集成外部工具和 API

来源: langchain_intro.txt
置信度: 92% (高)

多轮对话示例

用户: LangGraph 是什么？

助手: LangGraph 是 LangChain 生态系统中的一个重要组件，专门用于构建
有状态的、多步骤的 AI 应用。它基于图结构来定义工作流，使得复杂的 AI 
流程变得清晰和可控。

来源: langgraph_intro.txt
置信度: 89% (高)

用户: 它的核心概念有哪些？

助手: LangGraph 的核心概念包括：
状态（State）：使用 TypedDict 定义应用状态，在节点间传递
节点（Node）：处理状态的函数，执行具体的业务逻辑
边（Edge）：定义节点之间的连接和流转规则
条件边：根据状态动态决定下一个节点

来源: langgraph_intro.txt
置信度: 91% (高)

用户: 在什么场景下使用它比较合适？

助手: LangGraph 的典型应用场景包括：
多步骤推理
多代理协作
复杂决策流程
带有循环的工作流

它的优势在于可视化流程、状态管理、检查点支持和人机协作模式。

来源: langgraph_intro.txt
置信度: 87% (高)

📈 性能优化建议

文档处理优化
选择合适的分块策略：按段落、句子或固定长度分块
调整 chunk_size：平衡检索精度和上下文完整性
使用元数据过滤：减少不必要的检索范围

检索优化
调整 top_k 参数：根据需求调整检索文档数量
尝试不同检索算法：similarity vs MMR（最大边际相关性）
实现结果重排序：对检索结果进行二次排序

生成优化
控制 temperature：降低值获得更确定的回答
设置合理的 max_tokens：避免过长响应
优化提示模板：设计更有效的系统提示

系统优化
对话历史截断：仅使用最近4轮对话
异步请求处理：提高并发能力
连接池管理：优化数据库连接

🐛 常见问题

Q: API 连接失败？
A: 检查后端服务是否启动，确认端口 8000 是否被占用，查看控制台错误信息。

Q: 回答质量不高？
A: 
检查文档质量是否足够
调整 temperature 参数（建议 0.1-0.5）
优化知识库文档内容
调整 chunk_size 参数

Q: 检索不到相关文档？
A:
检查文档是否正确索引
调整 chunk_size 或 chunk_overlap
增加 top_k 参数值
检查查询关键词是否准确

Q: 置信度分数偏低？
A:
确保回答严格基于上下文
检查文档内容是否与问题相关
优化提示模板，强调基于上下文回答
调整检索参数提高相关性

Q: 前端无法连接后端？
A:
检查 API_BASE_URL 配置是否正确
确认后端服务正在运行
检查浏览器控制台错误信息
确认 CORS 配置正确

🤝 贡献指南

欢迎贡献代码！请遵循以下步骤：

Fork 本项目
创建特性分支 (git checkout -b feature/AmazingFeature)
提交更改 (git commit -m 'Add some AmazingFeature')
推送到分支 (git push origin feature/AmazingFeature)
开启 Pull Request

📄 许可证

本项目采用 MIT 许可证 - 详见 LICENSE 文件

🙏 致谢

LangChain - LLM 应用开发框架
LangGraph - 状态化工作流引擎
FastAPI - 高性能 Web 框架
智谱AI - GLM 系列大模型
OpenAI - 语言模型和嵌入服务

📧 联系方式

📧 Email: your.email@example.com
🐙 GitHub: @yourusername
💼 LinkedIn: your-profile

⭐️ 如果这个项目对你有帮助，请给个 Star 支持一下！

Happy Coding! 🚀
