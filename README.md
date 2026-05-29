# 毕业设计：基于 SpringBoot + Vue + AI 大模型的智慧旅游推荐系统

> 🎓 广州应用科技学院 · 计算机科学与技术 · 彭信力（202210007077）
> 
> 2025-2026 学年

---

## 📋 项目概述

本系统是一个融合 **AI 大模型 + 传统旅游管理** 的智慧旅游平台。用户可以在前端浏览景点、酒店、旅游线路并进行预订，同时通过 **AI 旅游助手"小智"** 实现智能行程规划、语音/文字问答、景点酒店一键预订。

---

## 🏗️ 技术架构

| 层级 | 技术栈 |
|------|--------|
| **后端** | Spring Boot 3.4 + MyBatis-Plus + MySQL + Redis + MongoDB |
| **前端** | Vue 3 + Element Plus（管理端 + 用户端） |
| **AI** | LangChain4j + 阿里云通义千问 + Spring AI + OpenAI |
| **数据** | MySQL 8.0（业务数据）+ MongoDB（对话记忆）+ Redis（缓存/会话） |
| **其他** | JWT 认证、WebSocket 实时通信、流式输出 (SSE/WebFlux) |

---

## ✨ 核心功能

### 🎯 业务模块
- **景点管理**：景点列表、详情、搜索、分类浏览
- **酒店预订**：酒店查询、房型选择、下单预订
- **旅游线路**：线路推荐、行程查看
- **论坛社区**：用户发帖、评论互动、收藏点赞
- **轮播管理**：首页轮播图配置

### 🤖 AI 智能助手（亮点）
- **AI 旅游规划师"小智"**：基于通义千问大模型，支持多轮对话
- **智能行程规划**：根据用户偏好、预算、时长自动生成旅游路线
- **一键预订**：对话中直接完成景点/酒店预订和取消
- **流式输出**：基于 SSE 实现 ChatGPT 式逐字回复
- **RAG 增强**：结合本地知识库提供精准旅游信息
- **Tool Calling**：AI 可调用业务接口实现真实业务操作
- **多模型支持**：兼容 OpenAI / 通义千问 / Ollama 本地模型

---

## 📂 项目结构

```
毕业设计代码数据库/
├── tourism-backend/          # Spring Boot 后端
│   ├── src/main/java/com/shanzhu/tourism/
│   │   ├── controller/       # 接口层（ChatController、XiaoZhiController 等）
│   │   ├── service/          # 业务逻辑层
│   │   ├── mapper/           # 数据访问层（MyBatis-Plus）
│   │   ├── entity/           # 实体类
│   │   ├── config/           # 配置类（CORS、Redis、JWT、MyBatis）
│   │   ├── assistant/        # AI Agent（XiaozhiAgent、TourismTools 等）
│   │   └── common/           # 工具类（JWT、Redis、MongoDB 工具）
│   ├── src/main/resources/
│   │   └── zhaozhi-prompt-template.txt  # AI 系统提示词
│   └── pom.xml               # Maven 依赖
├── vue/
│   ├── tourism-admin-frontend/    # 管理后台（Vue 3 + Element Plus）
│   └── tourism-user-frontend/    # 用户前端（Vue 3 + Element Plus）
├── tourism.sql                    # 数据库初始化脚本
└── 5月20日.mp4                    # 答辩演示视频
```

---

## 🚀 快速启动

### 1. 环境要求
- JDK 17+
- Node.js 18+
- MySQL 8.0+
- Redis 7+
- MongoDB 6+

### 2. 后端启动
```bash
cd tourism-backend
# 修改 application.yml 中的数据库连接和 API Key
mvn clean package -DskipTests
java -jar target/tourism-backend-0.0.1-SNAPSHOT.jar
```

### 3. 前端启动
```bash
cd vue/tourism-user-frontend
npm install
npm run dev
```

### 4. 配置 AI 模型
在 `application.yml` 中配置：
```yaml
langchain4j:
  openai:
    api-key: ${OPENAI_API_KEY}
  community:
    dashscope:
      api-key: ${DASHSCOPE_API_KEY}
```

---

## 🧪 AI 助手对话示例

```
用户：我想去广州塔玩
小智：🎯 广州塔是广州的地标景点！我已为您查询到信息：
     - 开放时间：09:00-22:30
     - 门票：150元起
     - 地址：广州市海珠区阅江西路222号
     需要我帮您预订门票吗？

用户：好的，帮我预订明天下午2点的
小智：✅ 预订成功！订单编号：GZ20250520001
     日期：2025年5月21日 14:00
     人数：1人
     请按时前往～
```

---

## 📊 数据库设计（11 张表）

| 表名 | 说明 |
|------|------|
| `sys_attractions` | 景点信息表 |
| `sys_hotel` | 酒店信息表 |
| `sys_hotel_item` | 酒店房型表 |
| `sys_hotel_order` | 酒店订单表 |
| `sys_attraction_order` | 景点预约表 |
| `sys_line` | 旅游线路表 |
| `sys_forum` | 论坛帖子表 |
| `sys_comments` | 评论表 |
| `sys_favor` | 收藏表 |
| `sys_rotations` | 轮播图表 |
| `user` | 用户表 |

---

## 🏆 项目亮点

- ✅ 完整的前后端分离架构，涵盖 11 张数据表
- ✅ LangChain4j 集成 Tool Calling，AI 可直接操作业务系统
- ✅ 支持多个 AI 模型无缝切换（通义千问 / OpenAI / Ollama）
- ✅ 流式输出 + SSE，媲美 ChatGPT 交互体验
- ✅ RAG 增强检索，结合本地旅游知识库精准回答
- ✅ MongoDB 持久化对话记忆，多轮上下文不丢失
- ✅ JWT + TokenInterceptor 实现用户认证与鉴权
- ✅ Redis 缓存热点数据，提升系统响应速度

---

## 📸 系统截图

> 详见 `项目与数据库/基于SpringBoot+Vue+AI大模型的旅游信息推荐系统/图片/` 目录

---

## 📄 相关文件

- 🎥 答辩视频：`5月20日.mp4`
- 📝 答辩情况表：`附件9：广州应用科技学院毕业设计（论文）答辩情况表.docx`
- 📦 后端源代码：`tourism-backend.zip`
- 📦 前端源代码：`vue.zip`
- 🗄️ 数据库脚本：`tourism.sql`

---

## 📝 致谢

感谢指导老师在毕业设计期间的悉心指导，感谢广州应用科技学院提供的学习平台与资源支持。

---

**© 2026 彭信力 | 广州应用科技学院 计算机科学与技术**
