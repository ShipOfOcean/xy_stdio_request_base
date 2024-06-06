# xy_stdio_request_base

- zh_CN [简体中文](README_zh_CN.md)
- zh_TW [繁体中文](README_zh_TW.md)
- en [English](README_en.md)


## Description
Singleton Tools.

<a href="https://github.com/ShipOfOcean/xy_stdio_request_base.git" target="_blank">Github</a>

## 安装

```bash
pip install xy_stdio_request_base
```

## How to use

###### python script

```python
from xy_stdio_request_base.Decorators import singleton, Singleton

@singleton
class Cls_0(object):
    count = 0
    def __init__(self):
        pass

@Singleton
class Cls_1(object):
    count = 0
    def __init__(self):
        pass

Cls_0().count = 10
Cls_0().count
# 10
Cls_0().count = 11
# 11
Cls_1().count = 10
# 10
Cls_1().count = 11
Cls_1().count
# 11

from xy_stdio_request_base.Singleton import CallSingleton, NewSingleton

class Foo_0(metaclass=CallSingleton):
    count = 0

Foo_0().count = 10
Foo_0().count
# 10
Foo_0().count = 11
Foo_0().count
# 11

class Foo_1(Singleton):
    count = 0
Foo_1().count = 10
Foo_1().count
# 10
Foo_1().count = 11
Foo_1().count
# 11

```

## Donate

If you think these tools are pretty good, Can you please have a cup of coffee?
<br/>
![WeChat](WeChat.png)
![Alipay](Alipay.png)

## Contact


```
Wechat: yuyangitt
Mail: 845262968@qq.com
```