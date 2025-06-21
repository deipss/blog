---
layout: default
title: Idea到vscode
parent: Solution
last_modified_date: 2025-05-29
---

# 1. Idea 到 vscode 的常用快捷键

- 打开终端:ctrl + shift + ·（不是数字 1 左边的符号）
- 文件重命名:回车键
- 打开近期文件:command + p
- 命令面板:command + shift + p
- 当前文件搜索:command + f
- 在整个工作区（workspace）内进行全文搜索:command + shift + f
- 打开快捷键设置： Cmd+K Cmd+S（Mac）
- 文件 > 打开文件夹（或按 Ctrl+O Ctrl+K ）

# 2. Java 工程

在VSCode中打开Java工程需要安装必要的扩展并进行适当配置。以下是详细步骤：


### 2.1. **步骤1：安装Java开发工具扩展**
1. 打开VSCode，点击左侧扩展图标（或按 `Ctrl+Shift+X`）。
2. 安装以下扩展：
   - **Extension Pack for Java**：微软官方提供的Java开发工具包，包含语言支持、调试器等。
   - **Maven for Java**：如果项目使用Maven管理依赖。
   - **Gradle Extension Pack**：如果项目使用Gradle管理依赖。


### 2.2. **步骤2：打开Java项目文件夹**
1. 点击菜单 **文件 > 打开文件夹**（或按 `Ctrl+K Ctrl+O`）。
2. 选择Java项目的根目录（包含 `src`、`pom.xml` 或 `build.gradle` 的文件夹）。


### 2.3. **步骤3：配置JDK路径（如果需要）**
1. 打开命令面板（`Ctrl+Shift+P`），输入 **"Java: Configure Java Runtime"**。
2. 选择已安装的JDK路径（需先自行安装JDK 11+）。
3. 若没有检测到JDK，点击 **"Add JDK"** 并指定路径。

![alt text](<img/vs jdk.png>)

### 2.4. **步骤4：识别项目结构**
- **Maven项目**：VSCode会自动识别 `pom.xml` 文件并下载依赖。
- **Gradle项目**：会自动识别 `build.gradle` 文件。
- **普通Java项目**：确保源代码位于 `src/main/java` 目录下（默认结构）。


### 2.5. **步骤5：编译和运行Java文件**
1. 打开Java文件（`.java`）。
2. 点击编辑器右上角的 **运行** 按钮（绿色三角形），或：
   - 右键点击编辑器，选择 **Run Java**。
   - 使用快捷键 `Ctrl+F5`（Windows/Linux）或 `Cmd+F5`（Mac）。


### 2.6. **步骤6：调试Java代码**
1. 在代码行号旁边点击设置断点。
2. 打开命令面板，输入 **"Debug: Start Debugging"** 或按 `F5`。
3. 选择调试配置（如 **"Java: Launch Program"**）。


### 2.7. **常见问题与解决方法**
1. **项目依赖未加载**：
   - 右键点击 `pom.xml` 或 `build.gradle`，选择 **"刷新Maven项目"** 或 **"刷新Gradle项目"**。
2. **找不到主类**：
   - 确保 `main` 方法存在且包路径正确。
   - 在 `launch.json` 中手动配置主类路径。
3. **VSCode提示"无法解析类型"**：
   - 等待依赖下载完成，或重启VSCode。
   - 检查JDK版本是否兼容项目要求。


通过以上步骤，你可以在VSCode中高效地开发和调试Java项目。

> 很难一次性完全迁移到vscode，主是因为IDEA有许多的快捷方式可以生成代码，尤其是一个DAO、BO、TO的转换，在vscode中需要自己写代码。

## maven的一些配置
![alt text](<img/vs mvn.png>)
mavne 工程的一些配置
![alt text](<img/vs mvn2.png>)


# 3. Python 工程

