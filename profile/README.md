<p align="center"><a href="README.en.md">English</a> · <b>简体中文</b></p>

<p align="center">
  <a href="https://axongui.github.io/Axon/"><img src="https://img.shields.io/badge/%E6%96%87%E6%A1%A3-%E5%9C%A8%E7%BA%BF%E9%98%85%E8%AF%BB-3451b2" alt="文档"></a>
  <a href="https://axongui.github.io/Axon/en/"><img src="https://img.shields.io/badge/docs-English-2ea44f" alt="docs"></a>
  <img src="https://img.shields.io/badge/python-3.12%2B-3451b2" alt="python">
  <img src="https://img.shields.io/badge/license-MIT-3451b2" alt="license">
</p>

---

Python 和 JavaScript 各写一行，就是一次跨进程调用：

```python
from axon import AxonController

@AxonController("MainView")          # 窗口名
class Calc:
    def add(self, a, b):
        return a + b
```

```javascript
import { Axon, AxonInit } from "axon-gui";

await AxonInit();                     // 有 Python 后端就握手，没有就静默返回
await Axon.Calc.add(2, 3);            // → 5，参数和返回值走 JSON
```

调用会走 QWebChannel，Python 侧的同步方法进线程池、`async def` 进事件循环，
JS 侧可以 `await`；反方向也一样：`Axon("MainView").DocsJS.someFunc(...)`、
双向事件、跨窗口共享的 key-value Store。

外观层是单独的包，因为「窗口长什么样」不属于「通道怎么走」——只要能力就不要多一个依赖。

## 这里有什么

| 入口 | 是什么 |
| --- | --- |
| [**Axon**](https://github.com/AxonGUI/Axon) | 框架本体：Python 运行时、JS 运行时、模板、文档站、打包脚本 |
| [**AxonShell**](https://github.com/AxonGUI/AxonShell) | 可选的窗口外观层：无边框窗口、自定义标题栏、菜单、右键菜单、缩放手柄 |
| [**文档站**](https://axongui.github.io/Axon/) | 每个示例都有「Python 侧怎么写 / JS 侧怎么写」，在客户端里打开时可以逐个点着跑 |
| [**在线示例**](https://axongui.github.io/Axon/examples/call) | 普通浏览器里是说明书；用客户端打开，按钮变成真的调用，能看到两端传了什么 |
| [**Releases**](https://github.com/AxonGUI/Axon/releases) | 文档客户端（Windows / Linux）、`axon-gui` 的 wheel/sdist、npm 包 |

## 三分钟跑起来

```bash
uv tool install axon-gui          # PyPI 未上架时用 Release 里的 wheel
axon-gui init myapp
cd myapp && uv sync
cd web/web-vue && npm install && npm run build && cd ../..
python main.py
```

详细步骤与另一种（不要模板、直接装包）写法见[快速开始](https://axongui.github.io/Axon/guide/quickstart)。

## 状态

个人项目，接口还在动，**不建议直接压在生产的核心链路上**。接口层有一套真 WebEngine 上的
断言（`core-py/tests/run_web_tests.py`），文档站有一套可点示例的自检，改动都要求先跑绿。



---
