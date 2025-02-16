# 📚 E2E-tests: WebdriverIO + Testomat.io Integration

This project contains end-to-end tests written in **TypeScript** using **WebdriverIO**. The tests demonstrate advanced usage of the Allure reporter (steps, logs, attachments, custom tags, etc.) and integrate with **Testomat.io** for enhanced reporting, categorization, and CI/CD analytics.

---

## 🚀 Project Description

This project is designed to:

- Validate web applications using the Page Object Model (POM) for maintainability.
- Provide detailed and categorized test reports with custom steps, logs, screenshots, artifacts, and tags.
- Demonstrate integration with Testomat.io for advanced test analytics.
- Ensure fast test execution with minimal timeouts (e.g., under 1 minute) while simulating random test failures to improve error reporting robustness.

---

## 🛠️ Features

- **Page Object Model (POM):** Separates page interactions from test logic.
- **Advanced Reporting:** Utilizes Allure steps, custom labels (e.g., `@Smoke`, `@Regression`, `@Critical`, `@UI`, `@API`), and attachments (screenshots, logs) for detailed test documentation.
- **Random Failure Simulation:** Uses helper functions to inject random failures, allowing you to test the robustness of error reporting.
- **Testomat.io Integration:** Automatically uploads test results via CI/CD pipelines.
- **Fast Execution:** Minimal timeouts (e.g., 5000 ms) ensure all tests complete quickly.

---

## 📋 Installation

### Prerequisites

- **Node.js:** Version 20 or higher (LTS version recommended)
  - We recommend using the latest LTS (Long Term Support) version of Node.js
  - Earlier versions are not supported and may cause compatibility issues
  - You can check your Node version by running: `node --version`
  - Download Node.js LTS from: https://nodejs.org/

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-username/your-project.git
   cd your-project
   ```

2. **Install dependencies:**

   ```bash
   npm ci
   ```

---

## ⚙️ Configuration

1. **Configure WebdriverIO:**\
   Edit the `wdio.conf.ts` file to adjust WebdriverIO settings (base URL, timeouts, reporters, etc.). Ensure the Allure reporter is enabled.

2. **Integrate Testomat.io:**\
   The CI/CD pipeline is configured to use the Testomat.io uploader. Set the following secrets in your CI environment:

   - `TESTOMATIO` - API key for test reporting
   - `TESTOMATIO_CREATE` - Set to 1 to enable test creation
   - `TESTOMATIO_ENV` - Environment details (e.g. "Chrome, Windows")


   After tests run, the CI pipeline automatically uploads the results to Testomat.io.

3. **Adjust Execution Parameters:**\
   Ensure that your test timeouts and retry settings in `wdio.conf.ts` allow all tests to complete within the desired timeframe (ideally under 1 minute).

4. **Artefacts Testomat.io:**\
   Set the following secrets in your testomat.io account:

   - `ACCESS_KEY_ID` - Access key id
   - `SECRET_ACCESS_KEY` - Secret access key
   - `BUCKET` - Bucket name
   - `ENDPOINT` - Endpoint
   - `REGION` - Region

   In the .env file, set the following, also on the dashboard you can set the following:
   - `TESTOMATIO_PRIVATE_ARTIFACTS` - Set to 1 to enable private artifacts

---

## 📄 Project Structure

```plaintext
├── test
│   ├── helpers
│   │      └── RandomFailureHelper.ts   # Helper to simulate random test failures
│   ├── pageobjects
│   │      ├── CheckoutPage.ts           # POM for the checkout page
│   │      └── TodoPage.ts               # POM for the TodoMVC page
│   └── tests
│          ├── checkout
│          │      ├── form.spec.ts       # Checkout form tests
│          │      └── ui.spec.ts         # Checkout UI tests
│          ├── todo
│          │      ├── add_remove.spec.ts # TodoMVC add/remove tests
│          └── randomFailures.spec.ts     # Tests with random failure simulation
├── wdio.conf.ts                         # WebdriverIO configuration file
├── package.json                         # Project metadata and dependencies
└── README.md                            # Project documentation
```

---

## ✍️ Writing Tests

Tests are written in TypeScript using WebdriverIO. Each test includes:

- **Steps and Logging:** Uses `allure.addStep` and `console.log` to record key actions.
- **Artifacts:** Screenshots are captured after each test and attached to the report.
- **Custom Tags and Parameters:** Tests are tagged (e.g., `@Smoke`, `@Regression`, `@Critical`, `@UI`, `@API`) and include additional information such as Priority, Risk, and Business Requirement.

**Example snippet from a test:**

```typescript
it('should fill the form with valid data @Smoke @UI', () => {
  if (typeof allure !== 'undefined') {
    allure.addLabel('tag', 'Smoke');
    allure.addStep('Starting test: filling out the checkout form with valid data');
  }
  checkoutPage.fillForm('John', 'Doe', 'johndoe', 'john@example.com', '123 Main St', 'United States', 'California', '90210');
  if (typeof allure !== 'undefined') {
    allure.addStep('Form filled successfully');
    console.log('Form filled successfully');
  }
});
```

---

## 🏃 Running Tests

1. **Run all tests:**

   ```bash
   npx wdio run wdio.conf.ts
   ```

2. **Run tests in parallel:**\
   Adjust the `maxInstances` setting in your `wdio.conf.ts` file to run tests in parallel.

3. **Run with Testomat.io Integration:**\
   After tests complete, the CI/CD pipeline will automatically generate the Allure report and upload the results to Testomat.io.

---

## 📊 Generating Reports

1. **Generate the Allure Report:**

   ```bash
   allure generate --clean
   ```

2. **Open the Allure Report:**

   ```bash
   allure open
   ```

---

## 🧪 CI/CD Integration

The project includes a YAML file for CI/CD pipelines (e.g., GitHub Actions) that:

- Installs dependencies.
- Runs WebdriverIO tests.
- Generates the Allure report.
- Uploads results to Testomat.io.

---

## 📞 Support

If you have any questions or issues, please contact the project maintainer or refer to the [Testomat.io Documentation](https://help.testomat.io/).

---

## 🔗 Useful Links

- [WebdriverIO Documentation](https://webdriver.io/docs/gettingstarted/)
- [Allure Reporter Documentation](https://docs.qameta.io/allure/)
- [Testomat.io Documentation](https://help.testomat.io/)
- [FAQ](https://help.testomat.io/faq)

---

✨ *Testing made simple!*

