<p align="center">
  <img src="https://raw.githubusercontent.com/AxonGUI/Axon/main/assets/axon-mark.svg" width="96" alt="Axon" />
</p>

<h1 align="center">Axon</h1>

<p align="center"><b>Write the backend in Python, the interface in HTML/CSS/JS.</b><br/>
PySide6 opens the window, any frontend framework draws the UI, both sides expose the same
API to each other, and it packages into a desktop client you can double-click.</p>

<p align="center"><a href="README.md">简体中文</a> · <b>English</b></p>

<p align="center">
  <a href="https://axongui.github.io/Axon/en/"><img src="https://img.shields.io/badge/docs-English-2ea44f" alt="docs"></a>
  <a href="https://axongui.github.io/Axon/"><img src="https://img.shields.io/badge/%E6%96%87%E6%A1%A3-%E4%B8%AD%E6%96%87-3451b2" alt="中文文档"></a>
  <img src="https://img.shields.io/badge/python-3.12%2B-3451b2" alt="python">
  <img src="https://img.shields.io/badge/license-MIT-3451b2" alt="license">
</p>

---

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
