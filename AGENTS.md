# linxira-plymouth-theme · Agent 开发规范

> **档位:B 内容仓** · 本仓是 **Linxira OS 的开机/关机 Plymouth 启动主题**(Jimmac spinner + ACPI BGRT 背景 + Linxira 品牌)。
> 通用条款见工作区总纲 `f:\Linxira-OS\AGENTS.md`,发布与测试口径见
> `linxira-os/docs/RELEASE_STANDARD.md`,本文件只写本仓特有事项,不复述通用条款。

## 职责

- 提供系统启动/关机动画主题资源;本仓**是少数已接入 ISO 构建的内容仓**。

## 目录布局

- `src/linxira.plymouth` —— 主题描述(`Name=Linxira`、`ImageDir=/usr/share/plymouth/themes/linxira`、`ModuleName=two-step`)。
- `src/animation-0001..0036.png` —— 启动动画帧序列。
- `src/throbber-0001..0030.png` —— 转圈帧序列。
- `src/watermark.png`、`src/watermark.svg` —— 水印。
- `src/lock.png`、`entry.png`、`capslock.png`、`bullet.png`、`keyboard.png`、`keymap-render.png` —— 交互态素材。
- `.mimosa/hook-state/` —— 工具运行时态(见 `.gitignore`,**非源码**)。

## 是否随 ISO 发布

- **已接入 ISO 构建**。`README.md` 明确:`linxira-iso-direct` 需要本主题 —— 构建时以
  `build-direct-iso.sh --plymouth-theme-directory <path>/src` 传入本仓的 `src/`。
  即 ISO 构建**直接引用 `src/` 目录**,本仓改动会进入构建链路。

## 上游来源与去品牌化

- 上游:`CachyOS/cachyos-plymouth-theme`(GPL-3.0,见 `README.md`)。
- 名称/路径**已迁移**:主题文件已重命名为 `linxira.plymouth`,`Name=Linxira`,`ImageDir` 指向 `themes/linxira`。
- 全仓**未发现 `cachyos` 硬编码**(已 grep,仅 `README.md` 保留上游出处链接)。

## 禁区

- `src/` 被 ISO 构建直接引用:**勿随意重命名/删除素材**;`animation-*`、`throbber-*` 帧序列命名须保持连续。
- 改 `Name` / `ImageDir` 须**同步 ISO 端的安装路径**,否则主题装载失败。
- 不要改 `.mimosa/` 运行时态;大体积 PNG 素材提交时注意仓库体积。