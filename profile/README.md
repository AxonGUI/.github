<p align="center">
  <img src="https://raw.githubusercontent.com/AxonGUI/Axon/main/assets/axon-mark.svg" width="96" alt="Axon" />
</p>

<h1 align="center">Axon</h1>

<p align="center"><b>用 Python 写后端，用 Web 写界面。</b><br/>
PySide6 开窗口，任意前端框架写界面，两侧同名 API 互调，可打包成双击即用的桌面客户端。</p>

<p align="center"><a href="#user-content-english">English</a> · <b>简体中文</b></p>

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

## 这里有什么

| 入口 | 是什么 |
| --- | --- |
| [**Axon**](https://github.com/AxonGUI/Axon) | 唯一的仓库：Python 运行时、JS 运行时、模板、文档站、打包脚本都在里面 |
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

## English

<p align="center"><b>Write the backend in Python, the interface in HTML/CSS/JS.</b><br/>
PySide6 opens the window, any frontend framework draws the UI, both sides expose the same
API to each other, and it packages into a desktop client you can double-click.</p>

Python and JavaScript, one line each, and you have a cross-process call:

```python
from axon import AxonController

@AxonController("MainView")          # the window name
class Calc:
    def add(self, a, b):
        return a + b
```

```javascript
import { Axon, AxonInit } from "axon-gui";

await AxonInit();                     // handshake if a Python backend exists, silent otherwise
await Axon.Calc.add(2, 3);            // -> 5, arguments and results travel as JSON
```

Calls go over QWebChannel: sync Python methods run on a thread pool, `async def` runs on the event
loop, and JS can `await`. The other direction works the same way —
`Axon("MainView").DocsJS.someFunc(...)`, plus events in both directions and a key-value store
shared across windows.

### What is here

| Entry | What it is |
| --- | --- |
| [**Axon**](https://github.com/AxonGUI/Axon) | the only repository: Python runtime, JS runtime, template, docs site and packaging scripts |
| [**Docs**](https://axongui.github.io/Axon/en/) | every example shows "how to write the Python side" and "how to write the JS side"; open it in the client and you can run each one |
| [**Live examples**](https://axongui.github.io/Axon/en/examples/call) | a manual in a normal browser; in the client the buttons become real calls and you can see what crossed the channel |
| [**Releases**](https://github.com/AxonGUI/Axon/releases) | the docs client (Windows / Linux), `axon-gui` wheel/sdist, npm package |

### Up and running in three minutes

```bash
uv tool install axon-gui          # use the release wheel while PyPI upload is in progress
axon-gui init myapp
cd myapp && uv sync
cd web/web-vue && npm install && npm run build && cd ../..
python main.py
```

Step-by-step details, and the other route (install the packages, no template) are in the
[Quickstart](https://axongui.github.io/Axon/en/guide/quickstart).
