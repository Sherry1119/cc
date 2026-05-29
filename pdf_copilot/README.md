# PDF智能客服Agent

基于本地PDF材料的自动客服对话系统，支持PDF上传、文本提取、向量化存储和智能问答。

## 🎯 功能特性

- **PDF文档上传**: 支持拖拽上传或点击选择PDF文件
- **智能文本提取**: 使用pdfplumber和PyPDF2提取PDF文本
- **向量化存储**: 使用ChromaDB进行文本向量化存储和检索
- **智能问答**: 基于相似度匹配的问答系统
- **Web界面**: 美观的Bootstrap 5响应式界面
- **实时交互**: 实时显示对话状态和置信度
- **知识管理**: 支持PDF列表查看、删除和知识库重置

## 🛠️ 开发环境搭建

### 1. 环境要求

- Python 3.8+
- pip包管理器

### 2. 安装依赖

```bash
# 进入项目目录
cd pdf_copilot

# 安装Python依赖
pip install -r requirements.txt
```

### 3. 目录结构

```
pdf_copilot/
├── src/                    # 源代码目录
│   ├── app.py            # Flask应用主入口
│   ├── utils/            # 工具模块
│   │   ├── logger.py     # 日志配置
│   │   ├── pdf_processor.py  # PDF处理工具
│   │   ├── vector_db.py   # 向量数据库管理
│   │   ├── knowledge_base.py  # 知识库管理
│   │   └── requirements_check.py  # 依赖检查
├── templates/             # HTML模板
│   └── index.html        # 主页面
├── static/               # 静态资源目录
├── data/                 # 数据存储目录
│   ├── pdfs/             # 原始PDF文件
│   ├── pdf_processed/    # 处理后的PDF
│   └── embeddings/      # 向量数据库
├── config.py             # 配置文件
├── run.py                # 启动脚本
├── requirements.txt     # Python依赖
└── .env.example         # 环境变量示例
```

## 🚀 快速开始

### 1. 检查依赖

```bash
python src/utils/requirements_check.py
```

### 2. 配置环境

```bash
# 复制环境配置文件
cp .env.example .env

# 编辑配置文件（可选）
nano .env
```

### 3. 启动服务

```bash
# 启动开发服务器
python run.py

# 或者指定端口
python run.py --port 8080

# 启用调试模式
python run.py --debug

# 重置知识库
python run.py --reset
```

### 4. 访问应用

打开浏览器访问: http://localhost:5000

## 📋 详细使用教程

### 步骤1：上传PDF文档

1. 点击上传区域或拖拽PDF文件到上传区域
2. 系统自动提取PDF文本并处理
3. 处理完成后，PDF文档将显示在左侧列表中

### 步骤2：进行智能问答

1. 在底部输入框输入问题
2. 按回车键或点击发送按钮
3. 系统将在右侧聊天区域显示回答
4. 显示回答的置信度和参考来源

### 步骤3：管理文档

- **查看PDF列表**：在左侧面板查看所有上传的PDF
- **删除PDF**：点击PDF旁边的删除按钮
- **重置知识库**：点击"重置"按钮清除所有文档

## 🔧 核心功能实现

### 1. PDF处理 (`pdf_processor.py`)

```python
# 主要功能：
- PDF文件验证（格式、大小检查）
- 文本提取（pdfplumber为主，PyPDF2为备）
- 文本分块处理
- PDF信息提取
```

### 2. 向量数据库 (`vector_db.py`)

```python
# 主要功能：
- ChromaDB初始化和配置
- 文本向量化存储
- 相似度搜索
- PDF数据管理
```

### 3. 知识库管理 (`knowledge_base.py`)

```python
# 主要功能：
- PDF添加和移除
- 查询和回答生成
- 统计信息管理
- 数据持久化
```

### 4. Web应用 (`app.py`)

```python
# 主要功能：
- Flask RESTful API
- 文件上传处理
- 实时问答接口
- 状态查询接口
```

## 🔄 API接口说明

### 1. 健康检查

```
GET /api/health
```

### 2. 上传PDF

```
POST /api/upload
Content-Type: multipart/form-data

参数：file (PDF文件)
```

### 3. 询问问题

```
POST /api/query
Content-Type: application/json

{
    "question": "如何使用这个系统？"
}
```

### 4. 获取PDF列表

```
GET /api/pdfs
```

### 5. 删除PDF

```
DELETE /api/remove-pdf/{pdf_id}
```

### 6. 获取统计信息

```
GET /api/stats
```

### 7. 重置知识库

```
POST /api/reset
Content-Type: application/json

{
    "confirm": true
}
```

## 🎨 界面功能说明

### 统计面板
- **PDF文档数**：显示当前知识库中的PDF数量
- **知识块数**：显示向量化后的文本块数量
- **系统状态**：显示运行状态（正常/异常）

### 文件上传
- 支持拖拽上传
- 支持点击选择
- 上传进度显示
- 错误提示

### 聊天界面
- 用户和机器人消息区分
- 加载动画
- 打字效果
- 回答来源显示
- 置信度指示

## 🔍 故障排除

### 1. 依赖安装失败

```bash
# 更新pip
pip install --upgrade pip

# 国内用户使用镜像
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/
```

### 2. PDF提取失败

- 检查PDF文件是否损坏
- 尝试重新保存PDF文件
- 使用其他PDF查看器导出

### 3. 向量数据库错误

- 删除 `data/embeddings` 目录重新创建
- 检查磁盘空间
- 重启应用

### 4. 界面无法访问

- 检查端口是否被占用
- 确认防火墙设置
- 使用 `--host 0.0.0.0` 允许外部访问

## 📝 高级配置

### 1. 修改配置文件

编辑 `config.py` 修改以下设置：

```python
# PDF配置
MAX_PDF_SIZE = 50 * 1024 * 1024  # 50MB
EMBEDDING_MODEL = 'all-MiniLM-L6-v2'

# Web配置
HOST = '0.0.0.0'
PORT = 5000

# 对话配置
MAX_TOKENS = 1500
TEMPERATURE = 0.3
```

### 2. 自定义嵌入模型

在 `config.py` 中修改 `EMBEDDING_MODEL`：

```python
# 使用其他模型
EMBEDDING_MODEL = 'paraphrase-multilingual-MiniLM-L12-v2'  # 多语言模型
```

### 3. 日志配置

修改日志级别和输出位置：

```python
LOG_LEVEL = 'DEBUG'  # DEBUG, INFO, WARNING, ERROR
LOG_FILE = 'logs/app.log'
```

## 🚀 部署指南

### 1. 生产环境部署

```bash
# 安装生产依赖
pip install gunicorn

# 使用gunicorn启动
gunicorn -w 4 -b 0.0.0.0:5000 src.app:app
```

### 2. Docker部署

创建 `Dockerfile`：

```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
EXPOSE 5000

CMD ["python", "run.py"]
```

### 3. Nginx配置

```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## 🎯 后续扩展方向

1. **集成大语言模型**
   - 使用ChatGPT、Claude等API增强问答能力
   - 实现更复杂的推理和总结

2. **多模态支持**
   - 支持图片、视频等多媒体文档
   - OCR文字识别

3. **对话历史管理**
   - 保存对话历史
   - 支持多轮对话

4. **权限管理**
   - 用户认证
   - 文档访问控制

5. **性能优化**
   - 缓存机制
   - 异步处理
   - 负载均衡

## 📄 许可证

MIT License

## 🤝 贡献指南

欢迎提交Issue和Pull Request！

---

**祝您使用愉快！** 🎉