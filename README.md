# xy_stdio_request_base

- zh_CN [简体中文](readme/README_zh_CN.md)
- zh_TW [繁体中文](readme/README_zh_TW.md)
- en [English](readme/README_en.md)

## 说明
标准输入输出封装

<a href="https://github.com/ShipOfOcean/xy_stdio_request_base.git" target="_blank">Github地址</a>

## 安装

```bash
pip install xy_stdio_request_base
```

## 使用

###### python脚本

```python
# main.py
import asyncio
from xy_stdio_request_base.Base import Base
from xy_string.utils import is_empty_string
from datetime import datetime


def printf(text):
    print(
        text,
        file=open(
            "./logs/server.log",
            "a+",
        ),
    )


class ServerBase(Base):
    input_text = None
    output_text = None
    error_text = None

    def on_output(self, output_text: str):
        self.output_text = output_text
        self.print_text(
            "output",
            self.output_text,
        )
        return super().on_output(self.output_text)

    def on_input(self, input_text: str):
        self.input_text = input_text
        self.print_text(
            "input",
            self.input_text,
        )
        return super().on_input(self.input_text)

    def on_error(self, error_text: str):
        self.error_text = error_text
        self.print_text(
            "error",
            self.error_text,
        )
        return super().on_error(self.error_text)

    def print_text(self, title: str, text: str):
        if not is_empty_string(text):
            printf(
                f"server post {datetime.now().isoformat()} {title} => {text} {self.identifier}",
            )


async def main():
    server = ServerBase()
    server.start()

    while not server.closed:
        server.write_input(
            f"server input => {datetime.now().isoformat()} {server.identifier}"
        )
        server.write_output(
            f"server output => {datetime.now().isoformat()} {server.identifier}"
        )
        server.write_error(
            f"server error => {datetime.now().isoformat()} {server.identifier}"
        )
        print_sep = server.input_text or server.output_text or server.error_text
        if not is_empty_string(server.input_text):
            printf(
                f"{datetime.now().isoformat()} input_text => {server.input_text}",
            )
            server.input_text = None
        if not is_empty_string(server.output_text):
            printf(
                f"{datetime.now().isoformat()} output_text => {server.output_text}",
            )
            server.output_text = None
        if not is_empty_string(server.error_text):
            printf(
                f"{datetime.now().isoformat()} error_text => {server.error_text}",
            )
            server.error_text = None
        if print_sep:
            printf(
                "=========================================================================",
            )
        await asyncio.sleep(3)


if __name__ == "__main__":
    asyncio.run(main())


```

```bash
> python main.py
```

## 捐赠

如果小伙伴们觉得这些工具还不错的话，能否请咱喝一杯咖啡呢
<br />
![微信](readme/WeChat.png)
![支付宝](readme/Alipay.png)

## 联系方式


```
微信: yuyangitt
邮箱: 845262968@qq.com
```