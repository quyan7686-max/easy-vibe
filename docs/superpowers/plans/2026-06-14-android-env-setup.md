# Android 开发环境配置与首个项目搭建实施计划

> **目标：** 在用户的电脑上完成 Android Studio、Trae 的安装，创建第一个基于 Kotlin + Jetpack Compose 的 Empty Activity 项目，配置国内镜像源，并成功运行到模拟器上。

**架构：** 采用 Easy-Vibe 教程推荐的 Vibe Coding 模式，以原生 Android (Kotlin + Compose) 为技术栈，Trae 作为 AI 编程助手，Android Studio 作为构建工厂。

**技术栈：** Kotlin, Jetpack Compose, Android Studio, Gradle, Trae

---

## Task 1: 安装 Trae (AI 编程助手)

**说明：** Trae 是进行 Vibe Coding 的主战场，内置 AI 辅助编程能力。

**步骤：**

- [ ] **Step 1: 下载 Trae**
  - 访问官网 [https://www.trae.cn](https://www.trae.cn)
  - 根据你的操作系统（Windows 或 Mac）下载对应版本
  - 双击安装包，按提示点击“下一步”完成安装

- [ ] **Step 2: 注册/登录 Trae**
  - 打开 Trae，使用手机号或邮箱注册账号并登录
  - 熟悉界面：左侧文件树、中间代码区、右侧 Chat 对话框

---

## Task 2: 安装 Android Studio (App 构建工厂)

**说明：** Android Studio 是 Google 官方 IDE，提供安卓 SDK、模拟器和编译环境。

**步骤：**

- [ ] **Step 1: 下载 Android Studio**
  - 访问官方下载页面 [https://developer.android.com/studio?hl=zh-cn](https://developer.android.com/studio?hl=zh-cn)
  - 下载适用于你系统的安装包（教程基于 2025.2.3 版本）

- [ ] **Step 2: 运行安装程序**
  - 双击安装包，保持默认选项一路点击 "Next"
  - 安装完成后首次启动，选择 "Do not import settings"

- [ ] **Step 3: 处理 JDK 环境（如遇到报错）**
  - 现代 Android Studio 通常自带 JDK，但如果遇到 "环境变量" 或 "SDK 配置" 报错
  - 参考详细避坑指南：[Android Studio 安装环境配置](https://blog.csdn.net/keiraee/article/details/142321644)

---

## Task 3: 创建第一个 Android 项目

**说明：** 使用 Empty Activity 模板创建项目，这是 Jetpack Compose 的标准入口。

**步骤：**

- [ ] **Step 1: 新建项目**
  - 打开 Android Studio，点击欢迎页面的 **"New Project"**
  - 在模板列表中选择 **"Empty Activity"**（图标上有 Jetpack Compose 标志）

- [ ] **Step 2: 填写项目配置**

| 字段 | 推荐值 | 说明 |
|------|--------|------|
| **Name** | My Application 1 | 应用名称，显示在手机桌面 |
| **Package name** | com.example.myapplication1 | 应用唯一标识符 |
| **Save location** | 自定义路径（如 E:\AndroidProjects\MyApplication1）| 不推荐放 C 盘 |
| **Minimum SDK** | API 30 | 覆盖超 90% 现役设备 |
| **Language** | Kotlin | Google 官方推荐语言 |

- [ ] **Step 3: 等待首次构建**
  - 点击 "Finish"，Android Studio 开始自动下载依赖
  - 第一次创建项目可能需要几分钟，请耐心等待
  - 直到底部进度条走完，左侧项目文件目录加载出来，才算成功

---

## Task 4: 配置国内镜像源（关键步骤）

**说明：** Android Studio 默认连接国外服务器，下载可能耗时极长或失败。配置国内镜像是一次性工作，受益终身。

**步骤：**

- [ ] **Step 1: 暂停当前下载**
  - 如果 Android Studio 右下角正在显示 "Gradle Building..."
  - 点击进度条旁边的暂停按钮，避免文件冲突

- [ ] **Step 2: 修改 Gradle 构建工具下载源**
  - 在左侧项目目录中，展开 `gradle` -> `wrapper`
  - 双击打开 `gradle-wrapper.properties`
  - 找到 `distributionUrl` 行，将其替换为：
    ```
    distributionUrl=https\://mirrors.cloud.tencent.com/gradle/gradle-8.7-bin.zip
    ```
  - **注意：** 只替换域名部分，其余不要动

- [ ] **Step 3: 修改依赖库下载源**
  - 在左侧目录根节点下找到并打开 `settings.gradle.kts`
  - 找到 `repositories { ... }` 代码块
  - 将其中的内容替换为以下国内镜像：
    ```kotlin
    // 阿里云镜像
    maven { setUrl("https://maven.aliyun.com/repository/public/") }
    maven { setUrl("https://maven.aliyun.com/repository/google/") }
    maven { setUrl("https://maven.aliyun.com/repository/jcenter/") }
    maven { setUrl("https://maven.aliyun.com/repository/gradle-plugin/") }
    // 华为云镜像
    maven { setUrl("https://repo.huaweicloud.com/repository/maven/") }
    // 腾讯云镜像
    maven { setUrl("https://mirrors.cloud.tencent.com/nexus/repository/maven-public/") }
    // 网易镜像
    maven { setUrl("https://mirrors.163.com/maven/repository/maven-public/") }
    ```

- [ ] **Step 4: 重新同步项目**
  - 保存文件修改
  - 点击 Android Studio 右上角的 **"Try Again"** 或 **"Sync Now"**
  - 等待几分钟，当底部控制台出现 **BUILD SUCCESSFUL** 时，环境搭建彻底成功

---

## Task 5: 理解项目结构

**说明：** 初学者只需关注三个核心文件，其他暂时不用管。

**步骤：**

- [ ] **Step 1: 切换 Android 视图**
  - 确保左侧 Project 面板处于 **Android** 视图（默认）

- [ ] **Step 2: 认识关键目录和文件**

```
app/
├── manifests/
│   └── AndroidManifest.xml     ← 应用"身份证"，声明应用名、入口 Activity
├── java/
│   └── com.example.myapplication1/
│       ├── MainActivity.kt       ← 应用入口，使用 Jetpack Compose 构建界面
│       └── ui/theme/
│           ├── Theme.kt          ← 定义界面外观（颜色、字体）
│           └── Color.kt          ← 定义颜色变量
├── res/
│   ├── drawable/                 ← 图片资源
│   ├── mipmap/                   ← App 图标
│   └── values/                   ← 文字、颜色、主题样式
└── build.gradle.kts (Module: app) ← App 构建配置
```

**核心关注：**
- `MainActivity.kt`：控制程序行为、决定屏幕上显示什么
- `AndroidManifest.xml`：注册组件、决定应用从哪里启动
- `Theme.kt`：定义界面外观

---

## Task 6: 创建模拟器并运行项目

**说明：** 验证环境是否搭建成功，看到第一个可运行的 App。

**步骤：**

- [ ] **Step 1: 打开设备管理器**
  - 点击 Android Studio 右侧工具栏的 **"Device Manager"**
  - 或通过顶部菜单 `View` -> `Tool Windows` -> `Device Manager`

- [ ] **Step 2: 创建虚拟设备**
  - 点击 "Add a new device" -> "Create Virtual device"
  - 选择 "Phone" 分类下的 "Smart Phone" 或 "Pixel" 系列
  - 点击 "Next"

- [ ] **Step 3: 选择系统镜像**
  - 在 "System Image" 列表中选中 "API 36.1"
  - 如果未下载，点击右侧 "Download" 按钮下载
  - 下载完成后选中，点击 "Finish"

- [ ] **Step 4: 启动模拟器**
  - 在设备管理器列表中，点击刚添加设备右侧的 **三角形播放按钮**
  - 稍等片刻，弹出模拟器窗口

- [ ] **Step 5: 运行 App**
  - 确保模拟器已启动并显示桌面
  - 点击 Android Studio 顶部工具栏的 **绿色三角形运行按钮**（或按 `Shift + F10`）
  - 等待编译完成，App 自动安装到模拟器
  - **成功标志：** 模拟器屏幕上显示 "Hello Android!" 或类似文字

---

## Task 7: 在 Trae 中打开项目（为 Vibe Coding 做准备）

**说明：** 将项目导入 Trae，后续通过自然语言与 AI 协作开发。

**步骤：**

- [ ] **Step 1: 打开项目**
  - 打开 Trae
  - 点击 "Open Folder"，选择刚才创建的 Android 项目文件夹（如 `E:\AndroidProjects\MyApplication1`）

- [ ] **Step 2: 验证文件浏览**
  - 在左侧文件树中，确认能看到 `app/src/main/java/.../MainActivity.kt`
  - 点击打开 `MainActivity.kt`，查看右侧是否有 Chat 对话框

- [ ] **Step 3: 发送第一条测试指令**
  - 在右侧 Chat 中输入：
    ```
    请帮我分析一下这个 MainActivity.kt 文件的作用是什么？
    ```
  - 验证 AI 能正确理解项目结构和代码含义

---

## 总结与下一步

完成以上所有步骤后，你的环境就已准备就绪。接下来将进入实战开发阶段：

1. 在 Trae 中通过自然语言描述需求
2. AI 生成 Kotlin + Compose 代码
3. 在 Android Studio 中运行到模拟器/真机查看效果
4. 反复迭代优化

**下一步预告：** 我们将按照 Easy-Vibe 教程，从零打造一款 "电子木鱼" App，涵盖 UI 交互、动画、音效、震动反馈等核心功能。
