---
title: loguru
author: Jerry.Baijy
tags:
  - dev
  - dev-tools
  - python
  - log-tools
---

# Overview

[Loguru](https://loguru.readthedocs.io/en/stable/) 是一个功能强大的 Python 日志库，旨在替代 Python 标准库的 `logging`模块，提供更加直观和便捷的日志记录体验。

# Install

```bash
# pip 安装
pip install loguru

# pdm 安装
pdm add loguru
```

# Quickstart

```python
from loguru import logger

logger.debug("这是一条调试信息")
logger.info("这是一条普通信息")
logger.warning("这是一条警告信息")
logger.error("这是一条错误信息")
logger.critical("这是一条严重错误信息")
```

