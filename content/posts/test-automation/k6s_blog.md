+++
authors = ["Devendran Nehru"]
title = "K6s Introduction"
date = "2025-07-10"
description = "Grafana K6s basic guide"
tags = [
    "k6",
    "automation",
    "web",
    "load",
]
categories = [
    "QA",
    "Automation",
]
series = ["Test Automation Frameworks"]
+++


# 🧪 Performance Testing with K6: A Complete Guide with Examples

## 📌 Introduction

When building modern web applications, ensuring they can handle a high load of users is essential. **K6** is a developer-centric open-source load testing tool built for making performance testing simple, efficient, and fun.

K6 enables developers and QA engineers to write load tests using JavaScript, execute them locally or in the cloud, and gain insights into performance bottlenecks before they impact real users.

---

## 🚀 Why Use K6?

- 📜 Written in JavaScript
- 🧪 Load, stress, and soak testing
- 🧰 CLI-based tool, easy to integrate in CI/CD pipelines
- 📊 Rich output for metrics
- ☁️ Cloud execution with [k6 Cloud](https://k6.io/cloud/)

---

## 🔍 How K6 Differs from Other Tools

K6 offers a unique approach to performance testing compared to traditional tools like **JMeter**, **Gatling**, or **Locust**. Here's a breakdown:

| Feature            | K6                         | JMeter                      | Gatling                    | Locust                      |
|--------------------|-----------------------------|-----------------------------|----------------------------|-----------------------------|
| Scripting Language | JavaScript                 | XML-based UI or Groovy      | Scala                      | Python                      |
| Ease of Use        | Simple JS scripts           | GUI-based, can be complex   | Requires Scala knowledge   | Python is beginner-friendly |
| CLI Support        | ✅ Strong                   | ✅ Moderate                  | ✅ Strong                  | ✅ Strong                   |
| CI/CD Integration  | ✅ Native support            | ⚠️ Possible with config      | ✅ Supported                | ✅ Supported                |
| Performance        | High, event-loop based      | Lower due to Java threads   | High (Scala, async)        | Moderate (Python threads)   |
| Visual Results     | Basic CLI + k6 Cloud        | GUI, Plugins                 | Web-based dashboard        | Web UI                      |
| Distributed Tests  | ✅ with k6 Cloud or OSS tools| ✅ via plugins                | ✅                          | ✅                          |

**Summary**:
- **K6** is ideal for developers who prefer coding tests directly.
- **JMeter** is better suited for testers who prefer a GUI.
- **Gatling** and **Locust** are also code-based but require Scala or Python, respectively.

K6 is especially strong for:
- Modern DevOps practices
- Script versioning in Git
- Integrations with Grafana for dashboards

---

## 🛠️ Installation

Install using Homebrew (macOS):
```bash
brew install k6
```

Or using Chocolatey (Windows):
```bash
choco install k6
```

Or via Docker:
```bash
docker run -i loadimpact/k6 run - <script.js
```

---

## 📄 Basic Example

### Simple Load Test Script (`script.js`)
```js
import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  vus: 10, // virtual users
  duration: '30s', // test duration
};

export default function () {
  http.get('https://test.k6.io');
  sleep(1);
}
```

### Run the test
```bash
k6 run script.js
```

---

## 📦 Project Structure Example

A typical K6 test project might look like this:

```
k6-load-tests/
├── tests/
│   ├── homepage.test.js
│   └── login.test.js
├── data/
│   └── users.csv
├── utils/
│   └── auth.js
└── k6.config.js
```

---

## 👨‍💻 Sample Advanced Script

### Login Simulation with Data

`data/users.csv`
```
username,password
testuser1,pass1
testuser2,pass2
```

`tests/login.test.js`
```js
import http from 'k6/http';
import { check, sleep } from 'k6';
import { SharedArray } from 'k6/data';

const users = new SharedArray('users', function () {
  return open('../data/users.csv').split('\n').slice(1).map(row => {
    const [username, password] = row.split(',');
    return { username, password };
  });
});

export const options = {
  vus: 5,
  duration: '20s',
};

export default function () {
  const user = users[Math.floor(Math.random() * users.length)];

  const payload = JSON.stringify({
    username: user.username,
    password: user.password,
  });

  const headers = { 'Content-Type': 'application/json' };

  const res = http.post('https://test-api.k6.io/auth/token/', payload, { headers });

  check(res, {
    'login success': (r) => r.status === 200,
  });

  sleep(1);
}
```

---

## 🧪 Test Types

- **Smoke Test**: Run with 1–2 users to validate script
- **Load Test**: Simulate normal traffic
- **Stress Test**: Increase load until the system fails
- **Spike Test**: Sudden increase in users
- **Soak Test**: Long-duration test

---

## 🔗 Integration with CI/CD

K6 can be easily integrated with tools like GitHub Actions:

```yaml
jobs:
  load-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Install k6
        run: sudo apt install k6 -y
      - name: Run Load Test
        run: k6 run tests/homepage.test.js
```

---

## 📈 Viewing Results

- CLI metrics summary
- JSON or CSV output: `k6 run --out json=output.json script.js`
- Use [k6 Cloud](https://k6.io/cloud/) for dashboard

---

## 📚 Resources

- [Official Docs](https://k6.io/docs/)
- [GitHub Repo](https://github.com/grafana/k6)
- [Awesome k6](https://github.com/grafana/awesome-k6)

---

## 🎯 Conclusion

K6 provides a fast, powerful, and developer-friendly way to ensure your system's performance and resilience. With JavaScript scripting and seamless integrations, it becomes a must-have tool in your performance testing toolkit.

Happy Testing! 🚀
