```
project/
├── api/                         # API接口相关代码
│   ├── handler/                 # API请求处理程序
│   ├── middleware/              # API中间件
│   └── router.go                # 路由定义
├── build/                       # 构建和部署相关文件
│   ├── Dockerfile               # Docker容器构建文件
│   ├── docker-compose.yml       # Docker编排配置文件
│   └── Makefile                 # 构建脚本和任务定义
├── cmd/                         # 应用程序启动入口
│   ├── app/                     # 主应用程序目录
│   │   └── main.go              # 主应用程序入口文件
│   └── cli/                     # 命令行工具目录
│       └── main.go              # 命令行工具入口文件
├── config/                      # 配置文件和配置相关代码
│   ├── config.go                # 配置结构体和加载逻辑
│   ├── local.yaml               # 本地开发配置文件
│   ├── dev.yaml                 # 开发环境配置文件
│   ├── prod.yaml                # 生产环境配置文件
│   └── test.yaml                # 测试环境配置文件
├── docs/                        # 项目文档目录
│   ├── requirements.md          # 需求文档（产品+用户需求）
│   ├── architecture.md          # 架构设计文档
│   ├── api.md                   # REST API接口文档
│   ├── database.md              # 数据库设计文档
│   ├── deployment.md            # 部署和运维文档
│   ├── development.md           # 开发指南和技术原理
│   └── README.md                # 文档概览和导航
├── internal/                    # 私有应用程序和库代码
│   ├── model/                   # 数据模型定义
│   ├── repository/              # 数据访问层代码
│   ├── service/                 # 业务逻辑层代码
│   └── util/                    # 内部工具函数
├── migrations/                  # 数据库迁移文件
├── pkg/                         # 可公共使用的库代码
├── scripts/                     # 构建、安装、生成代码等脚本
├── test/                        # 测试相关代码
├── web/                         # Web前端相关代码
├── .env.example                 # 环境变量示例文件
├── .gitignore                   # Git忽略文件配置
├── go.mod                       # Go模块依赖管理文件
├── go.sum                       # Go模块依赖校验和文件
├── LICENSE                      # 项目开源许可证文件
├── CHANGELOG.md                 # 版本变更记录文档
└── README.md                    # 项目简介和使用说明
```