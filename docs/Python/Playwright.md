---
layout: default
title: Playwright
parent: Python
last_modified_date: 2025-07-15
---

Playwright 是 Microsoft 开源的一个强大浏览器自动化工具，支持 Chromium、Firefox 和 WebKit，适合用于端到端测试、爬虫和自动化任务。

下面是 **Playwright 的常见使用场景和示例**（以 Python 和 Node.js 为主）：

---

## 1. 安装 Playwright

### Node.js：

```bash
npm install -D playwright
# 或选择特定浏览器版本
npm install -D playwright-chromium
npx playwright install
```

### Python：

```bash
pip install playwright
playwright install
```

---

##  2. 打开网页并截图

### Node.js (JavaScript / TypeScript)：

```js
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  await page.goto('https://example.com');
  await page.screenshot({ path: 'example.png' });
  await browser.close();
})();
```

### Python：

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page()
    page.goto("https://example.com")
    page.screenshot(path="example.png")
    browser.close()
```

---

## ✍️ 3. 表单交互（填写、点击、上传等）

```python
page.fill('#username', 'myuser')
page.fill('#password', 'mypassword')
page.click('button[type="submit"]')
```

---

## ⏱ 4. 等待元素出现

```python
page.wait_for_selector('.loading', state='hidden')  # 等待加载动画消失
```

---

## 📤 5. 文件上传

```python
page.set_input_files('input[type="file"]', 'myfile.pdf')
```

---

## 🔒 6. 登录并保持会话（保存 Cookie）

```python
context = browser.new_context(storage_state="state.json")
# ...
context.storage_state(path="state.json")
```

---

## 🧪 7. 使用测试框架（例如 `pytest`）

```python
# conftest.py
import pytest
from playwright.sync_api import sync_playwright


@pytest.fixture(scope="session")
def browser():
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=False)
        yield browser
        browser.close()
```

---

## 🧭 8. 导航与多标签页/多页面

```python
page1 = context.new_page()
page2 = context.new_page()
page1.goto("https://a.com")
page2.goto("https://b.com")
```

---

## 🔍 9. 元素定位（Selectors）

* `page.get_by_role("button", name="提交")`
* `page.locator('div >> text=Hello')`
* CSS: `page.locator(".my-class")`
* XPath: `page.locator('//button[@type="submit"]')`

---

## 🧱 10. 拦截网络请求 / 模拟响应

```python
def handle_route(route, request):
    if 'analytics' in request.url:
        route.abort()
    else:
        route.continue_()


page.route("**/*", handle_route)
```

---

## 📹 11. 录制视频 / 追踪

```python
context = browser.new_context(record_video_dir="videos/")
page = context.new_page()
page.goto("https://example.com")
context.close()
```

---

## 🧰 12. Headless 和 Devtools 模式

```python
browser = p.chromium.launch(headless=False, devtools=True)
```

---

## 🧪 13. 断言（结合测试）

```python
assert page.inner_text("h1") == "Welcome"
```

---

