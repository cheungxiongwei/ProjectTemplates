# 目录结构
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

# 数据库定义
```
-- =========================================
--  Lottery Demo – SQLite 全字段注释
--  (SQLite 仅保存行内注释，不写入元数据)
-- =========================================

/* ---------- configs ---------- */
CREATE TABLE configs (
                         id          INTEGER PRIMARY KEY AUTOINCREMENT, -- 主键
                         key         TEXT    NOT NULL UNIQUE,           -- 配置项唯一键
                         value       TEXT    NOT NULL,                  -- 配置内容(JSON 字符串)
                         updated_at  TEXT    NOT NULL                   -- 最后更新时间 (ISO8601)
);  -- 系统配置表

/* ---------- users ---------- */
CREATE TABLE users (
                       id            INTEGER PRIMARY KEY AUTOINCREMENT, -- 主键
                       username      TEXT    NOT NULL UNIQUE,           -- 用户名(唯一)
                       password_hash TEXT    NOT NULL,                  -- 密码哈希(SHA-256+salt)
                       balance       REAL    NOT NULL DEFAULT 0,        -- 账户余额
                       status        INTEGER NOT NULL DEFAULT 1,        -- 账户状态:1=正常 0=禁用
                       role          INTEGER NOT NULL DEFAULT 0,        -- 用户角色:0=普通用户 1=管理员 2=客服 3=财务...
                       created_at    TEXT    NOT NULL,                  -- 创建时间
                       updated_at    TEXT    NOT NULL,                  -- 更新时间
                       last_login_at TEXT                               -- 最后登录时间
);  -- 用户表

/* ---------- bets ---------- */
CREATE TABLE bets (
                      id              INTEGER PRIMARY KEY AUTOINCREMENT, -- 主键
                      user_id         INTEGER NOT NULL,                  -- 关联 users.id
                      period_number   TEXT    NOT NULL,                  -- 期号
                      numbers         TEXT    NOT NULL,                  -- 投注号码(JSON)
                      amount          REAL    NOT NULL,                  -- 投注总额
                      bet_type        INTEGER NOT NULL DEFAULT 1,        -- 投注类型:1=单式 2=复式
                      order_status    INTEGER NOT NULL DEFAULT 1,        -- 订单状态:1=有效 0=取消
                      winning_status  INTEGER NOT NULL DEFAULT 0,        -- 开奖状态:0=未开奖 1=中奖 2=未中奖
                      winning_amount  REAL    NOT NULL DEFAULT 0,        -- 中奖金额
                      created_at      TEXT    NOT NULL,                  -- 创建时间
                      updated_at      TEXT    NOT NULL,                  -- 更新时间
                      deleted_at      TEXT,                              -- 软删除时间
                      FOREIGN KEY(user_id) REFERENCES users(id)
);  -- 投注记录表

CREATE INDEX idx_bets_user_period ON bets(user_id, period_number); -- 复合索引

/* ---------- draws ---------- */
CREATE TABLE draws (
                       id            INTEGER PRIMARY KEY AUTOINCREMENT, -- 主键
                       period_number TEXT    NOT NULL UNIQUE,           -- 期号(唯一)
                       numbers       TEXT    NOT NULL,                  -- 开奖号码(JSON)
                       status        INTEGER NOT NULL DEFAULT 0,        -- 期状态:0=销售中 1=已开奖
                       created_at    TEXT    NOT NULL,                  -- 创建时间
                       updated_at    TEXT    NOT NULL,                  -- 更新时间
                       deleted_at    TEXT                               -- 软删除时间
);  -- 开奖信息表

/* ---------- transactions ---------- */
CREATE TABLE transactions (
                              id            INTEGER PRIMARY KEY AUTOINCREMENT, -- 主键
                              user_id       INTEGER NOT NULL,                  -- 关联 users.id
                              change        REAL    NOT NULL,                  -- 金额变动(正负)
                              balance_after REAL    NOT NULL,                  -- 变动后余额
                              type          INTEGER NOT NULL,                  -- 1=扣款 2=派奖 3=充值 4=提现
                              ref_id        INTEGER,                           -- 关联 bets.id 或第三方流水号
                              memo          TEXT,                              -- 备注
                              created_at    TEXT    NOT NULL,                  -- 创建时间 (ISO8601)
                              FOREIGN KEY(user_id) REFERENCES users(id)
);  -- 流水/资金变动表

CREATE INDEX idx_tx_user_time ON transactions(user_id, created_at); -- 复合索引
```

# API 定义
```

```

技术栈：
- Go + Chi
- 内存存储
- 未来加 SQLite
- JSON 接口，无前端

功能需求：
- 用户下注 6 个红球、1 个蓝球（或机选）
- 模拟开奖
- 查看历史记录
- 不需要用户系统
- 返回中奖等级（一等奖到六等奖）

我希望 AI 帮我做这些：
- 严格按照这个目录结构生成项目，并用这种分层思维来写代码。
- docs 是用户自己编辑的，不允许做任何修改。
- 生成 main.go、controller、service、model 结构
- 实现下注接口、开奖接口
- 模拟随机生成号码逻辑