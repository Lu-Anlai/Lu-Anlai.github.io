---
title: Manim的安装指南（Windows）
date: 2019-02-13 14:16:44
categories: 教程
tags:
- 教程
- Manim
---

网上的教程都不够详细，并且早已过时。

[$\text{Manim}$项目地址](https://github.com/3b1b/manim/)。

<!-- more -->

# 前期准备

1. [$\text{Manim}$](https://github.com/3b1b/manim/)基于[$\text{Python}3.7$](https://www.python.org/)，请确保$\text{Windows}$下安装了[$\text{Python}3.7$](https://www.python.org/)；

2. [$\text{Manim}$](https://github.com/3b1b/manim/)托管于[$\text{GitHub}$](https://github.com/)，请确保$\text{Windows}$下安装了[$\text{GitHub}$](https://github.com/)；

3. 请确保$\text{pip}$的版本是最新的。

# [$\text{Manim}$](https://github.com/3b1b/manim/)及其环境的配置

随便找一个目录，按住`Shift`键并右键选择`在此处打开 PowerShell 窗口`（$\text{Windows}10$以下的系统显示的是`命令提示符`）。

输入命令：

```
git clone https://github.com/3b1b/manim.git
cd manim
```

完成后可以发现原目录下多了一个叫做`manim`的文件夹，这就是以后的工作目录。

继续在之前的窗口中输入命令（或者在`manim`文件夹中打开$\text{PowerShell}$窗口）：

```
python -m pip install -r requirements.txt
```

## 问题

常见问题：

1. 在这一步中如果看到类似于`Error`或者`Visual Build 14.0`的字样，请自行上网搜索解决办法，搜索引擎推荐使用[$\text{Google}$](https://www.google.com/)。

2. 如果看到形如`ModuleNotFoundError: No module named <pack name>`的错误提示，请运行命令：

    ```
    pip install <pack name>
    ```

    特别的，如果遇见`ModuleNotFoundError: No module named 'readline'`，请输入：

    ```
    pip install pyreadline
    ```

# 测试

输入命令：

```
python -m manim example_scenes.py SquareToCircle -pl
```

如果弹出了一段下面这样的视频（分辨率为$854 \times 480$，帧率为$15 \text{FPS}$），说明$\text{Manim}$配置成功。

<embed src="480p15/SquareToCircle.mp4" width="854" height="480"/>

常见问题：

如果看到形如`ModuleNotFoundError: No module named <pack name>`的错误提示，请运行命令：

```
pip install <pack name>
```

特别的，如果遇见`ModuleNotFoundError: No module named 'readline'`，请输入：

```
pip install pyreadline
```

## 欣赏影片

以下影片分辨率为$1280 \times 720$，帧率为$30 \text{FPS}$

<embed src="720p30/SquareToCircle.mp4" width="854" height="480"/>

<embed src="720p30/WarpSquare.mp4" width="854" height="480"/>

<embed src="720p30/WriteStuff.mp4" width="854" height="480"/>
