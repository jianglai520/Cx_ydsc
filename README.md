# Cx_ydsc - 超星学习通阅读时长自动刷取工具

> **无需 Python 环境，双击即用**。自动模拟鼠标滚轮上下滚动，模拟真人阅读行为，帮助在超星学习通（chaoxing.com）自动累积阅读时长。

---

## 📦 快速开始（推荐：直接用 exe）

### 下载方式
- **Releases 页面**：前往 [Releases](https://github.com/jianglai520/Cx_ydsc/releases) 下载最新的 `CxReadTime.exe`
- 或直接使用本仓库 `dist/` 目录下已打包好的 `CxReadTime.exe`

### 使用步骤
1. **双击运行** `CxReadTime.exe`
   - 首次运行若 Windows 提示“未知发行者”或“受 SmartScreen 保护”，点击 **“详细信息” → “仍要运行”**
   - 建议：**右键 → “以管理员身份运行”**（部分系统需要管理员权限才能模拟鼠标滚轮）
2. 打开 **超星学习通**（网页版 `chaoxing.com` 或客户端），进入任意**阅读页面**
3. **将鼠标悬停在阅读区域上方**（不要移开鼠标）
4. 保持 `CxReadTime` 窗口打开，脚本会自动开始随机上下滚动
   - 窗口会显示倒计时和执行日志，例如：
     ```
     8秒后,在12秒内上移 1850 个像素点
     已执行上移 1850 个像素点
     ```
5. 想停止时，**直接关闭 `CxReadTime` 窗口**即可

---

## 🛠️ 开发者：从源码运行

### 环境要求
- Python 3.8+
- 依赖：`pyautogui`、`pillow`（仅打包时需要）

### 安装依赖
```bash
pip install pyautogui pillow -i https://pypi.tuna.tsinghua.edu.cn/simple
```

### 运行脚本
```bash
python main.py
```

### 自行打包 exe
```bash
pip install pyinstaller -i https://pypi.tuna.tsinghua.edu.cn/simple
pyinstaller --onefile --noconsole --icon gui.ico --name CxReadTime main.py
```
生成的 exe 在 `dist/CxReadTime.exe`

---

## ⚙️ 工作原理

- **核心逻辑**：后台线程每 3–15 秒随机决定向上或向下滚动，滚动距离 500–3000 像素，持续 3–15 秒
- **模拟方式**：使用 `pyautogui.scroll()` 模拟鼠标滚轮事件，**不移动鼠标位置**，仅发送滚轮消息
- **触发条件**：**鼠标必须悬停在目标阅读区域上方**（脚本检测鼠标位置，仅在鼠标停留时发送滚动）
- **GUI 界面**：基于 `tkinter` 的灰色小窗口，实时显示倒计时与执行状态

---

## ❓ 常见问题

| 问题 | 解决方法 |
|------|----------|
| 双击 exe 没反应 / 闪退 | 右键 → “以管理员身份运行” |
| 滚动没效果 / 阅读时长没增加 | 确认鼠标**一直悬停在阅读区域**；尝试管理员运行；检查是否被杀毒软件拦截 |
| Windows 报毒 / SmartScreen 拦截 | 属于无签名程序的正常现象，点“详细信息 → 仍要运行”；或加入杀毒白名单 |
| 报错 `ModuleNotFoundError: pyautogui` | 源码运行需先 `pip install pyautogui`；exe 版无需安装 |
| 想修改滚动频率/距离 | 编辑 `main.py` 中 `random.randint` 的范围参数 |

---

## ⚠️ 免责声明

- 本工具**仅供学习交流使用**，请勿用于刷课作弊、刷时长造假等违反学校/平台规定的行为
- 使用本工具产生的一切后果由使用者自行承担，作者不承担任何法律责任
- 超星学习通等平台可能更新反作弊机制，导致本工具失效，请知悉

---

## 📄 许可证

本项目基于 **GPL-3.0** 协议开源，遵循原仓库 [SJYssr/Cx_ydsc](https://github.com/SJYssr/Cx_ydsc) 许可。

- 允许自由使用、修改、分发
- 修改后的代码必须同协议开源
- 不得用于闭源商业软件

---

## 🙏 致谢

- 原作者：[SJYssr](https://github.com/SJYssr) - 项目创建与核心逻辑
- 依赖库：`pyautogui`、`tkinter`（标准库）、`pillow`（打包用）