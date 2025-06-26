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