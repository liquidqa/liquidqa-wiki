## 🔍 DOM-Based Locators

| Locator Type                   | Syntax Example                                 | Description                             |
|-------------------------------|-----------------------------------------------|---------------------------------------|
| By Tag name                   | `page.locator('tag')`                          | Select by HTML tag                     |
| By ID                         | `page.locator('#id')`                          | Select by element ID                   |
| By Class name              | `page.locator('.className')`                   | Select elements containing class      |
| By full Class name           | `page.locator('[class="exactClassName"]')`    | Select elements with exact class attr |
| By Attribute                  | `page.locator('[attr="value"]')`               | Select elements by attribute           |
| By combining selectors        | `page.locator('tag[attr="value"][attr2]')`     | Combine multiple attribute selectors   |
| By XPath (not recommended)   | `page.locator('//*[@id="value"]')`             | Select by XPath (avoid if possible)    |

---

## 🕵️‍♂️ User-Facing Locators

| Locator Type                 | Syntax Example                                   | Description                            |
|-----------------------------|-------------------------------------------------|--------------------------------------|
| By partial text match        | `page.locator(':text("partialText")')`          | Match elements containing text       |
| By exact text match          | `page.locator(':text-is("exactText")')`         | Match elements with exact text        |
| By visible text             | `page.getByText('visibleText')`                    | Match element by visible text         |
| By role                     | `page.getByRole('roleName', { name: 'accessibleName' })` | Match by ARIA role and accessible name |
| By label                   | `page.getByLabel('labelText')`                    | Match input by associated label       |
| By placeholder             | `page.getByPlaceholder('placeholderText')`        | Match input by placeholder text       |
| By test ID (data-testid)    | `page.getByTestId('testIdValue')`                  | Match by `data-testid` attribute       |
| By title                   | `page.getByTitle('pageTitle')`                      | Match element by title attribute       |

<br>

## ✅ Good Practices for Playwright Locators

<details>
<summary><strong> 💬 Read more </strong></summary>

### [Playwright Locators Documentation](https://playwright.dev/docs/locators)
---

### 1. Prioritize User-Facing Locators

- **Official Docs**:  
  Playwright recommends using locators that reflect how users perceive the page, such as roles, labels, and accessible names. This approach leads to more resilient tests.

- **Community Insight**:  
  Experts emphasize that user-facing locators are less likely to break with UI changes compared to DOM-based locators.  

---

### 2. Avoid XPath and Complex CSS Selectors

- **Official Docs**:  
  XPath and overly complex CSS selectors can be brittle and are discouraged unless absolutely necessary.

- **Community Insight**:  
  Discussions highlight that XPath locators often lead to flaky tests and should be avoided when possible.

---

### 3. Use `data-testid` for Stability

- **Official Docs**:  
  While not explicitly required, using `data-testid` attributes provides stable and intention-driven hooks for testing.

- **Community Insight**:  
  Many developers advocate for `data-testid` to ensure selectors remain reliable despite UI changes.  
 
---

### 4. Keep Selectors Simple and Readable

- **Official Docs**:  
  Simple, readable locators are easier to maintain and less prone to breaking.

- **Community Insight**:  
  Avoid overly complex or chained selectors when not needed. Favor clarity.  

---

### 5. Chain Locators for Precision

- **Official Docs**:  
  You can chain locators to scope your selection and narrow it down precisely.

- **Community Insight**:  
  Chaining and filtering locators helps reduce ambiguity and better target deeply nested elements.  

---

### 6. Utilize Playwright's Auto-Waiting

- **Official Docs**:  
  Playwright automatically waits for elements to be ready before performing actions — no need for manual `waitFor`.

- **Community Insight**:  
  Relying on built-in auto-waiting improves test reliability and reduces flakiness.  

---

### 7. Handle Multiple Matching Elements Carefully

- **Official Docs**:  
  If multiple elements match a locator, Playwright throws unless you explicitly select one.

- **Community Insight**:  
  Use `.first()`, `.nth(index)`, or `.last()` to specify which match to use when multiple exist.

---

</details>




