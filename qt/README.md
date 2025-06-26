```
qt/
├── qt-widget-app/               # Qt Widgets桌面应用模板
│   ├── CMakeLists.txt           # CMake配置文件
│   ├── {{PROJECT_NAME}}.pro     # qmake项目文件（备选）
│   ├── src/                     # 源代码目录
│   │   ├── main.cpp             # 程序入口
│   │   ├── mainwindow.cpp       # 主窗口实现
│   │   ├── mainwindow.h         # 主窗口头文件
│   │   ├── mainwindow.ui        # UI界面文件
│   │   └── core/                # 核心业务逻辑
│   ├── resources/               # 资源文件
│   │   ├── icons/               # 图标资源
│   │   ├── images/              # 图片资源
│   │   ├── translations/        # 国际化翻译文件
│   │   └── resources.qrc        # Qt资源配置
│   ├── ui/                      # UI文件目录
│   ├── tests/                   # 测试代码
│   ├── docs/                    # 项目文档
│   ├── deploy/                  # 部署相关文件
│   │   ├── windows/             # Windows部署配置
│   │   ├── linux/               # Linux部署配置
│   │   └── macos/               # macOS部署配置
│   ├── .gitignore               # Git忽略文件
│   └── README.md                # 项目说明
├── qt-qml-app/                  # Qt QML移动/现代应用模板
│   ├── CMakeLists.txt           # CMake配置文件
│   ├── src/                     # C++源代码
│   │   ├── main.cpp             # 程序入口
│   │   ├── backend/             # 后端逻辑
│   │   └── models/              # 数据模型
│   ├── qml/                     # QML界面文件
│   │   ├── main.qml             # 主界面
│   │   ├── pages/               # 页面组件
│   │   ├── components/          # 可复用组件
│   │   └── styles/              # 样式文件
│   ├── resources/               # 资源文件
│   │   ├── fonts/               # 字体资源
│   │   ├── images/              # 图片资源
│   │   └── qml.qrc              # QML资源配置
│   ├── translations/            # 国际化文件
│   ├── tests/                   # 测试代码
│   └── android/                 # Android特定配置
├── qt-console-app/              # Qt控制台应用模板
│   ├── CMakeLists.txt           # CMake配置文件
│   ├── src/                     # 源代码目录
│   │   ├── main.cpp             # 程序入口
│   │   ├── application.cpp      # 应用程序类
│   │   └── application.h        # 应用程序头文件
│   ├── config/                  # 配置文件
│   ├── tests/                   # 测试代码
│   └── README.md                # 项目说明
└── qt-library/                  # Qt库项目模板
    ├── CMakeLists.txt           # CMake配置文件
    ├── src/                     # 源代码实现
    ├── include/                 # 公共头文件
    ├── examples/                # 使用示例
    ├── tests/                   # 单元测试
    ├── docs/                    # API文档
    └── CMakeLists.txt           # 库构建配置
```