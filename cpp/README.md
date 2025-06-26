```
cpp/
├── cmake-library/               # CMake库项目模板
│   ├── CMakeLists.txt           # 根CMake配置文件
│   ├── cmake/                   # CMake模块和脚本
│   │   ├── modules/             # 自定义CMake模块
│   │   └── toolchains/          # 交叉编译工具链
│   ├── include/                 # 公共头文件目录
│   │   └── {{PROJECT_NAME}}/    # 项目命名空间头文件
│   ├── src/                     # 源代码目录
│   ├── tests/                   # 单元测试
│   │   ├── unit/                # 单元测试用例
│   │   ├── integration/         # 集成测试用例
│   │   └── CMakeLists.txt       # 测试CMake配置
│   ├── examples/                # 使用示例
│   ├── docs/                    # 项目文档
│   │   ├── api/                 # API文档
│   │   ├── tutorials/           # 教程文档
│   │   └── README.md            # 详细说明
│   ├── third_party/             # 第三方依赖
│   ├── scripts/                 # 构建和部署脚本
│   │   ├── build.sh             # 构建脚本
│   │   ├── install.sh           # 安装脚本
│   │   └── format.sh            # 代码格式化脚本
│   ├── .clang-format            # 代码格式化配置
│   ├── .clang-tidy              # 静态分析配置
│   ├── .gitignore               # Git忽略文件
│   ├── LICENSE                  # 开源许可证
│   ├── README.md                # 项目说明
│   └── CHANGELOG.md             # 变更日志
├── cmake-application/           # CMake应用程序模板
│   ├── CMakeLists.txt           # 根CMake配置文件
│   ├── src/                     # 源代码目录
│   │   ├── main.cpp             # 主程序入口
│   │   ├── core/                # 核心逻辑模块
│   │   ├── utils/               # 工具函数模块
│   │   └── CMakeLists.txt       # 源码CMake配置
│   ├── include/                 # 头文件目录
│   ├── resources/               # 资源文件
│   ├── config/                  # 配置文件
│   ├── tests/                   # 测试代码
│   ├── docs/                    # 项目文档
│   ├── .clang-format            # 代码格式化配置
│   ├── .gitignore               # Git忽略文件
│   └── BUILD.md                 # 构建说明
└── modern-cpp/                  # 现代C++项目模板
    ├── CMakeLists.txt           # 根CMake配置（C++20/23）
    ├── conanfile.txt            # Conan依赖管理
    ├── vcpkg.json               # vcpkg依赖管理
    ├── src/                     # 源代码
    ├── include/                 # 头文件
    ├── tests/                   # 测试（使用Catch2/GoogleTest）
    ├── benchmarks/              # 性能测试（使用Google Benchmark）
    ├── .github/                 # GitHub Actions CI/CD
    │   └── workflows/           # 工作流配置
    ├── Dockerfile               # Docker容器化
    └── docker-compose.yml       # Docker编排
```