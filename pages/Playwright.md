### Защо Playwright + TypeScript е „правилният“ избор 🔥

* **Type safety** → по-малко runtime простотии
* **Autocomplete / IntelliSense** → по-бързо писане, по-малко грешки
* **Enums, interfaces, types** → стабилен и четим framework
* **По-enterprise** → това се очаква на интервю и в сериозни проекти

### 1️⃣ Какво реално трябва да владееш 

> Фокус: **реално владеене**, не copy–paste automation.

#### 🧱 Core Playwright Fundamentals

* `test`, `expect`, `Page`, `BrowserContext`
* Разлика между **page-level** и **context-level** state
* Auto-waiting механизма на Playwright (и защо НЕ ти трябват implicit waits)

#### 🧩 Fixtures (custom test context)

* Built-in fixtures (`page`, `context`, `request`)
* **Custom fixtures** чрез `base.extend()`
* Fixture lifecycle (`scope: test | worker`)
* Dependency injection между fixtures

> 👉 Това е „DI контейнерът“ на Playwright

#### 🏗️ POM + Composition (НЕ inheritance като в C#)

* Page Object = **thin abstraction**, не business logic dump
* **Composition**: Page използва други Page-и / Components
* Component-based POM (Card, Modal, Header)
* Без `new Page()` в test → идва от fixture

> ❌ Anti-pattern: огромни Page класове

#### 🎯 Locators & Assertions

* `locator()` vs `getByRole` / `getByTestId`
* **Web-first assertions**
* `expect.poll()` за async state
* **Soft assertions** (`expect.soft`) → multiple failures

#### 🔌 API Testing (`request`)

* `APIRequestContext`
* API setup / teardown за UI tests
* Hybrid tests: **API arrange → UI assert**
* Auth/token bootstrapping през API

#### 🔐 StorageState (Auth без login)

* `storageState.json`
* Multi-user auth states
* Auth като fixture
* Кога НЕ е добра идея

#### 🧭 test.step() (репорти & дебъг)

* Семантични стъпки
* По-добри HTML / Allure репорти
* Четими CI логове

#### ⚙️ Parallelism & Sharding

* `fullyParallel`
* Worker-и vs tests
* Sharding за големи test suites
* Flaky test isolation

#### 📊 Custom Reporters

* HTML
* Allure
* Custom JSON reporters
* Reporters за CI
---
## 2️⃣  Разширен Playwright Roadmap (TypeScript-first)

> Цел: **от beginner → confident senior-level automation engineer**

---

### 🟢 Фаза 0 – TypeScript & JS Fundamentals (задължително)

> ⚠️ Това е критично, ако идваш от C#

#### TypeScript специфики (MUST KNOW)

* `type` vs `interface`
* Union / Literal types (`'admin' | 'user'`)
* Optional chaining (`?.`)
* Nullish coalescing (`??`)
* Enums (и кога да НЕ ги ползваш)
* Generics (`<T>`)
* Async / Await (Promise mental model)

#### JavaScript поведение (често чупи тестове)

* Truthy / Falsy
* `undefined` vs `null`
* Reference vs Value
* Closures (callbacks в retries)

---

### 🟢 Фаза 1 – Playwright Core & Clean Tests

* Playwright config (`playwright.config.ts`)
* Projects (multi-browser, mobile)
* Auto-waits & retries
* Screenshots / video / traces
* Stable locators стратегия

#### Архитектура

* Tests = **business flow**
* Pages = **UI abstraction**
* Fixtures = **context & setup**

---

### 🟡 Фаза 2 – POM, Components & E2E

#### POM Best Practices

* Малки Page класове
* Component Objects (Button, Modal, Table)
* Reusable assertions

#### E2E стратегия

* Happy paths
* Critical paths
* NO over-mocking
* API preconditions

---

### 🟡 Фаза 3 – API + UI Hybrid Testing

* Auth през API
* Data seeding
* Backend validation
* Contract-level asserts

---

### 🟠 Фаза 4 – Debugging & Stability

* Traces (local + CI)
* Flaky test analysis
* Test isolation
* Deterministic data

---

### 🟠 Фаза 5 – Reporting & CI/CD

* HTML / Allure reports
* GitHub Actions / GitLab CI
* Artifacts (screenshots, traces)
* Parallel execution в CI

---

### 🔴 Фаза 6 – Advanced / Senior Level

* Custom fixtures architecture
* Multi-repo test strategy
* Cross-env execution
* Performance smoke tests
* AI-assisted testing (MCP-ready)

---

### 🧠 Mental Model (най-важното)

* Tests описват **какво**, не **как**
* Page Objects скриват UI детайли
* Fixtures контролират state
* Playwright чака вместо теб – ако му позволиш

👉 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣
