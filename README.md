# Ref for Windows

一张图，说清楚。Ref for Windows 是驻留系统托盘的截图标注工具：给界面上的控件、文件和区域加上编号与修改要求，再把截图和说明合成为一张 PNG，交给 AI 或同事。

本仓库仅用于发布 **Windows 可执行文件、版本更新说明与校验文件**。源码维护在 [GHOSTLaycoo/Ref-w](https://github.com/GHOSTLaycoo/Ref-w)。

## 下载

- [下载最新 Windows 版 EXE](https://github.com/GHOSTLaycoo/ref-win-releases/releases/latest)
- [查看所有版本与更新说明](https://github.com/GHOSTLaycoo/ref-win-releases/releases)
- [下载最新版本的 SHA-256 校验文件](https://github.com/GHOSTLaycoo/ref-win-releases/releases/latest/download/SHA256SUMS.txt)

目前为预览版本。支持 Windows 10 / Windows 11，需要 .NET Framework 4.8。v0.6.15 在 x64 Windows 上内置简体中文和英语 OCR。

## 运行

1. 从 Releases 下载 `RefWindows-<版本>.exe`。
2. 双击 EXE 运行。关闭主窗口后，Ref 会留在任务栏右下角的系统托盘。
3. 从旧版切换时，先在系统托盘选择「退出 Ref」，再启动新版。

## 快速上手

1. 按 **Ctrl + Alt + R** 开始标注，多显示器时先选择屏幕。
2. 鼠标移到目标上单击添加编号；滚轮切换候选层级。也可按 **F / A / T** 使用框选、箭头与文字。
3. 在面板中填写逐条要求和整体要求。
4. 按 **Ctrl + Enter** 保存并复制合成 PNG，然后粘贴或上传到支持图片的 AI 客户端。

截图、OCR 和图片合成在本机完成。自动保存目录为 `%LOCALAPPDATA%\RefWindows\Captures`。

更多操作见[完整操作手册](https://github.com/GHOSTLaycoo/Ref-w/blob/main/docs/操作手册.md)。

## 其他 OCR 语言

Ref for Windows v0.6.15 在 x64 Windows 上内置简体中文和英语 OCR，可以离线识别中英混排的截图。其他语言使用 Windows 提供的 OCR 组件。若内置识别引擎无法启动，Ref 会尝试系统 OCR。

1. Windows 11 打开 **设置 → 时间和语言 → 语言和区域**。Windows 10 打开 **设置 → 时间和语言 → 语言**。
2. 在「首选语言」中选择「添加语言」，安装要识别的语言。可以保留原来的 Windows 显示语言。
3. 从系统托盘退出并重新打开 Ref，然后在主窗口「开始标注」旁的「OCR 语言」下拉框中，选择带「Windows」字样的目标语言。

如果添加后仍未出现在 Ref 中，可以在管理员 Windows PowerShell 中运行 `Get-WindowsCapability -Online -Name 'Language.OCR*'` 查看可用语言。以法语（法国）为例，依次安装基础语言和 OCR 组件。

```powershell
Add-WindowsCapability -Online -Name 'Language.Basic~~~fr-FR~0.0.1.0'
Add-WindowsCapability -Online -Name 'Language.OCR~~~fr-FR~0.0.1.0'
```

组件安装完成后再次重启 Ref。并非所有语言都有 Windows OCR 组件。[微软语言安装说明](https://support.microsoft.com/zh-cn/windows/hardware/input-devices/manage-the-language-and-keyboard-input-layout-settings-in-windows) · [Windows OCR 组件说明](https://learn.microsoft.com/zh-cn/windows-hardware/manufacture/desktop/features-on-demand-language-fod?view=windows-11#ocr)

内置 OCR 基于 Tesseract，随发布版提供[第三方许可证](https://github.com/GHOSTLaycoo/ref-win-releases/releases/latest/download/THIRD-PARTY-NOTICES.txt)。

## 校验下载文件

每个版本附带 `SHA256SUMS.txt`。在 PowerShell 中运行以下命令，将结果与校验文件比对：

```powershell
Get-FileHash -Algorithm SHA256 .\RefWindows-0.6.15.exe
```

## 更新与反馈

当前采用手动更新：下载新版本，退出旧版后运行新 EXE。

使用问题可以在本仓库 [Issues](https://github.com/GHOSTLaycoo/ref-win-releases/issues) 中反馈；开发与源码相关内容请前往[源码仓库](https://github.com/GHOSTLaycoo/Ref-w)。

Ref for Windows 是独立的 Windows 实现，交互灵感来自 [Ref for macOS](https://github.com/ddhjy/ref-releases)。
