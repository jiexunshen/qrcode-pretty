# QR Code Pretty

[English](./README.md)

这个分支保留了原来的 `qrcode-pretty` 命令行工具，并在它的基础上新增了一个浏览器里的可视化设计器。

## 改了什么

### 可视化设计器

新增 [`docs/qrcode-designer.html`](./docs/qrcode-designer.html)，用于在本地浏览器里可视化生成二维码。

它支持原 CLI 已有的样式控制项：

- 二维码模块样式
- 内定位点样式
- 外定位点样式
- 主体颜色
- 内定位点颜色
- 外定位点颜色
- 中心图片
- 透明背景
- 二维码版本
- 方块尺寸
- 边距
- 纠错等级

设计器可以导出 SVG 和 PNG。

### 预设

新增内置预设：

- Classic high contrast
- GitHub repository
- arXiv preprint
- Soft round accent

预设会让二维码点阵颜色和定位点颜色尽量贴近对应 logo，同时保留足够的扫描对比度。

页面也支持保存本地预设。保存的预设存放在浏览器 `localStorage` 中。

### Logo 处理

新增内置 logo 资源：

- [`assets/github-logo.svg`](./assets/github-logo.svg)
- [`assets/arxiv-logo.svg`](./assets/arxiv-logo.svg)

设计器会按照二维码模块网格清除 logo 后方的点阵，而不是按普通像素矩形裁剪。
这样调整 logo 尺寸、logo 留白、方块尺寸或边距时，logo 底板仍然能和二维码模块对齐。

导出的 SVG 和 PNG 会把 logo 图片以内嵌 data URL 的方式写入文件，因此导出后 logo 不会丢失。

### URL 校验

可视化设计器只会为合法的 `http` 或 `https` 网站地址生成二维码。
输入非法时会显示警告，并清空预览。

### 语言切换

新增 `EN` / `ZH` 分段式语言切换。

### 资源整理

把 logo 文件移动到 `assets/`，并重命名为稳定的项目资源名：

- `GitHub_Invertocat_Black.svg` -> `assets/github-logo.svg`
- `arxiv-logo.svg` -> `assets/arxiv-logo.svg`

## 启动设计器

在项目根目录运行：

```bash
python -m http.server 8000 --bind 127.0.0.1
```

然后打开：

```text
http://127.0.0.1:8000/docs/qrcode-designer.html
```

## 说明

原来的 Python 包和命令行工具仍然保留。
这份 README 只记录在原项目基础上做的改动。
