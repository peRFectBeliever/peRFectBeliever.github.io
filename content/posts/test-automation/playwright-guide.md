
+++
authors = ["Devendran Nehru"]
title = "Test Automation MasterClass - Playwright Introduction"
date = "2024-12-10"
description = "🎭 End-to-End Testing with Playwright: A Complete Guide"
tags = [
    "playwright",
    "automation",
    "web",
]
categories = [
    "QA",
    "Automation",
]
series = ["Test Automation Frameworks"]
+++

## 📌 Introduction

[Playwright](https://playwright.dev/) is a modern end-to-end testing library developed by Microsoft. It enables reliable testing for web applications across all modern rendering engines — Chromium, Firefox, and WebKit — with a single API.

Playwright is **fast**, **flexible**, and **developer-friendly**, supporting powerful features like:
- Headless browser testing
- Auto-waiting for elements
- Screenshots & video recording
- Built-in support for multiple browsers and devices
- Cross-platform test execution

## 🚀 Getting Started with Playwright

### 1. 📦 Installation

You can install Playwright using npm or yarn:

```bash
npm init playwright@latest
# or
npm install -D @playwright/test
```

To install browser binaries:

```bash
npx playwright install
```

## 📁 Project Structure

A typical Playwright project looks like:

```
playwright.config.ts
tests/
  └── example.spec.ts
tests-examples/
  └── login.spec.ts
```

## ✍️ Writing Your First Test

Let's create a basic test using Playwright's built-in test runner `@playwright/test`.

### 📄 `example.spec.ts`

```ts
import { test, expect } from '@playwright/test';

test('homepage has title and links to docs', async ({ page }) => {
  await page.goto('https://playwright.dev/');

  // Expect title to contain Playwright
  await expect(page).toHaveTitle(/Playwright/);

  // Click the "Get started" link.
  await page.getByRole('link', { name: 'Get started' }).click();

  // Expect the URL to contain intro
  await expect(page).toHaveURL(/.*intro/);
});
```

### 🧪 Run the Test

```bash
npx playwright test
```

## 🌍 Cross-Browser Testing

Playwright supports:
- **Chromium** (Chrome, Edge)
- **Firefox**
- **WebKit** (Safari)

Update `playwright.config.ts` to test on all browsers:

```ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  projects: [
    { name: 'Chromium', use: { browserName: 'chromium' } },
    { name: 'Firefox', use: { browserName: 'firefox' } },
    { name: 'WebKit', use: { browserName: 'webkit' } },
  ],
});
```

## 📱 Emulating Devices

You can emulate real-world devices using `devices` from Playwright.

```ts
import { devices } from '@playwright/test';

projects: [
  {
    name: 'Mobile Safari',
    use: devices['iPhone 13'],
  },
]
```

## 📸 Screenshots & Videos

Enable media capture in `playwright.config.ts`:

```ts
use: {
  screenshot: 'on',
  video: 'retain-on-failure',
}
```

Inside your test:

```ts
await page.screenshot({ path: 'screenshot.png' });
```

## 🔐 Authentication Testing

### Example: Login and Save Storage State

```ts
// login.spec.ts
import { test } from '@playwright/test';

test('login and save state', async ({ page }) => {
  await page.goto('https://example.com/login');
  await page.fill('#username', 'testuser');
  await page.fill('#password', 'password123');
  await page.click('button[type="submit"]');

  // Save state to file
  await page.context().storageState({ path: 'auth.json' });
});
```

Then reuse this state:

```ts
// playwright.config.ts
use: {
  storageState: 'auth.json'
}
```

## 🧱 Component Testing (React, Vue, etc.)

Playwright supports component testing with frameworks like React, Vue, and Angular via its component testing mode.

```bash
npx playwright test --project=react
```

Learn more: [Component Testing](https://playwright.dev/docs/component-testing/introduction)

## 🧰 Useful Utilities

- **Fixtures**: Custom test setup/teardown
- **Trace Viewer**: Visualize what happened in a test
- **Parallel Execution**: Speed up test runs

```bash
npx playwright show-trace trace.zip
```

## 📊 CI Integration

Playwright integrates seamlessly with CI tools like GitHub Actions, GitLab CI, CircleCI, etc.

### Example: GitHub Actions

```yaml
name: Playwright Tests

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v3
        with:
          node-version: 20
      - run: npm install
      - run: npx playwright install --with-deps
      - run: npx playwright test
```

## 🧠 Best Practices

- Use `data-testid` or `getByRole` for reliable selectors
- Isolate test state with `beforeEach` and `afterEach`
- Keep tests deterministic and idempotent
- Mock API responses when needed
- Use page.waitForURL or `expect` to ensure stability

## 📚 Resources

- Official Docs: [https://playwright.dev/](https://playwright.dev/)
- GitHub Repo: [https://github.com/microsoft/playwright](https://github.com/microsoft/playwright)
- Playwright Test Generator: `npx playwright codegen example.com`

## ✅ Conclusion

Playwright is a robust and modern tool for end-to-end testing. Whether you're testing across browsers, simulating mobile devices, or integrating into CI pipelines, Playwright offers everything needed to deliver high-quality web applications.