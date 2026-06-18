# QwenPaw iOS APP

<p align="center">
  <img src="https://img.shields.io/badge/Swift-5.9-F05138?logo=swift" alt="Swift"/>
  <img src="https://img.shields.io/badge/iOS-16.0%2B-000000?logo=apple" alt="iOS"/>
  <img src="https://img.shields.io/badge/SwiftUI-5-0D96F6?logo=swift" alt="SwiftUI"/>
  <img src="https://img.shields.io/badge/Xcode-15-147EFB?logo=xcode" alt="Xcode"/>
  <img src="https://img.shields.io/github/license/R3lyW1nd/QwenPaw-iOS-APP" alt="License"/>
</p>

<p align="center">
  <b>让你的 QwenPaw Agent 随身而行</b> —— 原生 iOS 客户端，通过 REST API 实现与 AI 助手的实时对话。
</p>

---

> ⚠️ **APP 目前正在开发中，尽请期待！**

---

## 目录

- [功能特性](#-功能特性)
- [技术栈](#-技术栈)
- [项目架构](#-项目架构)
- [使用说明](#-使用说明)
- [API 对接说明](#-api-对接说明)
- [注意事项](#-注意事项)
- [许可证](#-许可证)

---

## 功能特性

| 功能 | 说明 |
|------|------|
| 实时对话 | SSE 流式响应，打字机效果实时显示 AI 回复 |
| 多 Agent 切换 | 支持切换不同智能体角色 |
| 文件管理 | 查看 / 下载工作空间文件 |
| 数据统计 | Token 消耗统计、API 调用次数追踪 |
| 主题系统 | 浅色 / 深色 / 跟随系统 + 多强调色，完美融合 iOS 设计语言 |
| Widget 小组件 | 桌面 Widget 快速查看对话状态 |
| Live Activity | 实时活动展示 AI 回复进度 |
| Spotlight 搜索 | 系统级搜索历史消息 |
| iCloud 同步 | 多设备间同步对话记录 |
| Shortcuts 快捷指令 | 支持 Siri 快捷指令唤起 |
| 离线缓存 | 消息本地持久化（CoreData），断网可查看 |


## 截图预览

<div align="center">

| | | | |
|---|---|---|---|
<img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_1.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_2.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_3.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_4.jpg' width='170'/> |
<img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_5.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_6.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_7.jpg' width='170'/> | |

</div>


## 技术栈

| 类别 | 技术 |
|------|------|
| 语言 | Swift 5.9 |
| UI 框架 | SwiftUI 5（iOS 16+） |
| 架构 | MVVM + Coordinator |
| 网络层 | URLSession + async/await |
| SSE 流式解析 | AsyncSequence + AsyncStream |
| 状态管理 | @Observable / @Published / Combine |
| 本地持久化 | SwiftData / CoreData |
| 主题引擎 | @AppStorage + dynamic color assets |
| 系统集成 | WidgetKit / Live Activities / Intents |
| 最低 SDK | iOS 16.0 |
| 构建工具 | Xcode 15 + Swift Package Manager |

## 项目架构

```
QwenPaw-iOS/
├── QwenPaw/
│   ├── App/
│   │   ├── QwenPawApp.swift                  # 应用入口
│   │   ├── ContentView.swift                 # 根视图
│   │   └── AppDelegate.swift                 # App 生命周期
│   ├── Models/
│   │   ├── AgentInfo.swift                   # Agent 信息模型
│   │   ├── Message.swift                     # 消息模型
│   │   ├── TokenStats.swift                  # Token 统计
│   │   ├── WorkspaceFile.swift               # 文件模型
│   │   └── CronJob.swift                     # 定时任务模型
│   ├── Views/
│   │   ├── Chat/
│   │   │   ├── ChatView.swift                # 聊天主视图
│   │   │   ├── MessageBubbleView.swift       # 消息气泡
│   │   │   └── InputBarView.swift            # 输入栏
│   │   ├── Agent/
│   │   │   └── AgentListView.swift           # Agent 列表
│   │   ├── Stats/
│   │   │   └── StatsView.swift               # 数据统计
│   │   ├── Settings/
│   │   │   ├── SettingsView.swift            # 设置页
│   │   │   ├── ThemePickerView.swift         # 主题选择
│   │   │   └── ServerConfigView.swift        # 服务器配置
│   │   ├── Manage/
│   │   │   ├── FileListView.swift            # 文件管理
│   │   │   └── CronListView.swift            # 定时任务
│   │   └── Components/
│   │       ├── ShimmerView.swift             # 骨架屏
│   │       ├── EmptyStateView.swift          # 空状态
│   │       └── LoadingIndicator.swift        # 加载指示器
│   ├── ViewModels/
│   │   ├── ChatViewModel.swift               # 聊天状态管理
│   │   ├── AgentViewModel.swift              # Agent 管理
│   │   ├── SettingsViewModel.swift           # 设置状态
│   │   └── StatsViewModel.swift              # 统计管理
│   ├── Services/
│   │   ├── APIService.swift                  # API 层
│   │   ├── SSEStream.swift                   # SSE 流式解析
│   │   ├── AuthService.swift                 # 认证管理
│   │   ├── CacheService.swift                # 缓存服务
│   │   └── KeychainManager.swift             # 安全存储
│   ├── Utilities/
│   │   ├── Logger.swift                      # 日志
│   │   ├── Formatters.swift                  # 格式化工具
│   │   └── Extensions.swift                  # 扩展方法
│   └── Resources/
│       ├── Assets.xcassets/                  # 资源文件
│       └── Colors.xcassets/                  # 主题色
├── QwenPawWidget/                            # Widget 扩展
│   └── QwenPawWidget.swift
├── QwenPawIntents/                           # Siri Intents 扩展
│   └── IntentHandler.swift
├── QwenPaw.xcodeproj/
├── Package.swift
└── README.md
```

## 使用说明

### 下载安装

> 待 App Store 上线后可通过 TestFlight 或 App Store 下载。

### 首次使用

1. 安装后打开应用
2. 在设置页填写 QwenPaw 服务器地址
3. 输入用户名和密码完成登录
4. 开始与 AI 对话

### 聊天

1. 在底部输入框输入消息，点击发送
2. AI 回复以 SSE 流式实时展示
3. 支持工具调用结果自动展示

### iOS 特色功能

- **Widget 小组件**：在主屏幕添加 Widget，快速查看最近消息
- **Live Activity**：锁屏/灵动岛实时显示 AI 回复进度
- **Spotlight 搜索**：下拉搜索可直接检索历史消息
- **Siri 快捷指令**：通过 Siri 唤醒发送消息
- **iCloud 同步**：多设备间对话记录自动同步



## API 对接说明

应用对接 QwenPaw RESTful API，完整文档请参考 [QwenPaw RESTful API 文档](https://qwenpaw.agentscope.io/docs/api-tutorial)。

### 主要接口

| 接口 | 方法 | 说明 |
|------|------|------|
| /api/auth/login | POST | 用户登录认证 |
| /api/console/chat | POST | SSE 流式聊天消息 |
| /api/agents | GET | 获取 Agent 列表 |
| /api/sessions | GET | 获取会话列表 |
| /api/skills | GET | 获取可用技能 |
| /api/tools | GET | 获取可用工具 |
| /api/token/stats | GET | Token 使用统计 |
| /api/workspace/files | GET | 工作空间文件列表 |

### 认证方式

```
Authorization: Bearer <JWT_TOKEN>
```

### SSE 流式响应

聊天接口采用 SSE 协议，通过 Swift 的 `AsyncStream` 实现流畅的流式展示。

## 注意事项

1. 应用使用 HTTP 明文传输，请仅在可信网络环境中使用
2. Token 通过 Keychain 安全存储
3. SSE 连接超时设置为 5 分钟
4. iCloud 同步需登录同一 Apple ID
5. Widget 和 Live Activity 需要 iOS 16.1+

## 许可证

MIT License © 2026 R3lyW1nd

---

<p align="center">
  Made with ❤️ by R3lyW1nd &amp; GeoS4C
</p>
