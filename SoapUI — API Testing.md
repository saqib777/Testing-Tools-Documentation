# SoapUI / ReadyAPI — API Testing (Corrected & Practical)

## Short summary
**SoapUI (Open Source)** is a GUI tool focused on functional testing of SOAP and REST web services.  
**ReadyAPI** (commercial product from SmartBear) is the enterprise suite that builds on SoapUI with extra capabilities: a modern UI, automated security scanning, load testing (LoadUI integration), test case data-driven features, CI integrations and professional support.

---

## When to pick SoapUI vs ReadyAPI
- **SoapUI (free)** — good for learning, small projects, manual test creation, and basic automation.  
- **ReadyAPI (paid)** — use for team collaboration, scheduled/automated security and load tests, advanced reporting, and CI/CD readiness.

---

## Key Concepts (how SoapUI structures tests)
- **Project** — top-level container (service definitions, endpoints, global properties).  
- **TestSuite** — logical group of test cases (e.g., “Authentication”, “Orders”).  
- **TestCase** — sequence of test steps that form a scenario.  
- **TestStep** — a single action inside a TestCase (Request, Groovy Script, Delay, Property Transfer, JDBC, etc.).  
- **Assertions** — checks applied to responses (Status, XPath/JSONPath, Schema, Contains, Scripted).  
- **Properties** — variables stored at Project/TestSuite/TestCase/Global levels used for data-driven testing and reuse.

---

## Typical beginner → production workflow
1. Create a Project (import WSDL or OpenAPI/Swagger).  
2. Add TestSuites and TestCases.  
3. Add TestSteps (Requests), then add Assertions to each response.  
4. Parameterize using Properties (avoid hardcoding).  
5. Create DataSource (CSV/Excel/JDBC) to drive multiple test iterations.  
6. (Optional) Use Property Transfers to pass response values into subsequent requests.  
7. Run tests in the GUI for quick feedback.  
8. Export the project and run via CLI or CI using ReadyAPI `testrunner` or the Maven plugin.  
9. For load/security: use ReadyAPI features (LoadUI integration, Security scans) or tie into other tools.

---

## Practical examples & snippets

### 1) Add a simple Status assertion (no code)
- Create TestStep: HTTP GET `https://jsonplaceholder.typicode.com/posts/1`  
- Click **Add Assertion → HTTP Status → Status Is 200**

### 2) JSONPath assertion (check a field exists)
- Add assertion: **Script Assertion** (or built-in JSONPath match)  
- Example JSONPath: `$.userId` with an expected value or existence check.

### 3) Property Transfer — pass a token from login to next request
- TestStep A: POST `/auth/login` → response contains `{ "token": "abc" }`  
- TestStep B: subsequent request needs header `Authorization: Bearer ${#TestCase#authToken}`  
- In TestStep A add a **Property Transfer**:
  - Source: Response (JSONPath) `$.token` → Target: TestCase property `authToken`  
- In TestStep B use `${#TestCase#authToken}` in header.

### 4) Groovy Script Assertion (example)
- Add a **Script Assertion** on a TestStep (uses Groovy):
```groovy
def json = new groovy.json.JsonSlurper().parseText(messageExchange.responseContent)
assert json.userId == 1 : "Expected userId 1 but got ${json.userId}"
```
This fails the test with a clear message if the assertion fails.

---

## Running tests outside the GUI

### SoapUI Open Source (CLI)
SoapUI provides `testrunner.sh` / `testrunner.bat` for running projects headless:
```bash
# run all tests in a project
/path/to/soapui/bin/testrunner.sh -s"TestSuiteName" -c"TestCaseName" /path/to/project.xml

# example
/path/to/soapui/bin/testrunner.sh -s "LoginSuite" -c "ValidLogin" MyProject-soapui-project.xml
```

### ReadyAPI / Ready! API TestRunner
ReadyAPI has an enhanced `testrunner` with more options and reporting (HTML, JUnit, PDF). Command example:
```bash
/path/to/ready-api/bin/testrunner.sh -r -a -f /reports/folder -j -R "JUnit" MyReadyAPIProject.xml
# -r generate report, -a include all test suites, -f output folder, -j produce junit xml
```

### Maven integration (ReadyAPI/SoapUI Pro plugin)
Add the ReadyAPI/SoapUI maven plugin in your CI build to execute tests during the build:
```xml
<plugin>
  <groupId>com.smartbear.readyapi</groupId>
  <artifactId>ready-api-maven-plugin</artifactId>
  <version>VERSION</version>
  <executions>
    <execution>
      <phase>integration-test</phase>
      <goals>
        <goal>test</goal>
      </goals>
      <configuration>
        <projectFile>${basedir}/MyReadyAPIProject.xml</projectFile>
      </configuration>
    </execution>
  </executions>
</plugin>
```
This is commonly wired into Jenkins/GitLab CI to gate builds by API test results.

---

## Data-driven testing (practical)
- **DataSource Step**: CSV, Excel, JDBC or Workbook.  
- **Loop**: Add a DataSource loop to repeat TestCase per row.  
- **Property Transfer**: use data columns as properties in requests.  
This is how you run the same TestCase for many user credentials or payloads without duplicating TestCases.

---

## Mocking & Virtualization
- SoapUI / ReadyAPI can create **Mock Services** from WSDL/OpenAPI.  
- Useful for: testing when a downstream service is unavailable, or creating stable responses for front-end teams.  
- Mock runs locally or on a server; ReadyAPI provides more advanced virtualization features.

---

## Security & Load testing (ReadyAPI)
- **Security tests**: ReadyAPI includes automated security scans (SQLi, XSS, command injection checks). These are not in the Open Source SoapUI.  
- **Load testing**: ReadyAPI integrates with LoadUI or can export test scenarios to run distributed load. Open Source has limited load capabilities; production load testing typically uses JMeter, k6, or LoadRunner for scale.

---

## Common pitfalls & how to avoid them
- **Hardcoded URLs / tokens** — use Properties and Environments.  
- **GUI-only habit** — export projects and run via CLI in CI for real automation.  
- **Ignoring false positives** — always verify scanner results manually.  
- **Over-reliance on GUI for large suites** — move to version control and consider project export strategies to manage changes.  
- **Large binary project files** — keep test data external (CSV / DB) and reference via DataSource.

---

## Good test design tips
- Keep TestCases small and focused (one flow per TestCase).  
- Reuse TestSteps (shared requests) where sensible.  
- Use clear naming: `TS_Login_Valid`, `TS_Login_Invalid`.  
- Group related tests into TestSuites for easier targeted runs.  
- Capture response snapshots and logs for failing CI runs to speed debugging.

---

## Limitations & when to choose other tools
- **Not ideal for extreme-scale performance testing** — use JMeter / k6 / Gatling for load.  
- **GUI approach can make massive CI-driven automation uncomfortable** — teams that prefer "test-as-code" often choose language libraries (RestAssured, supertest) integrated with their test frameworks.  
- **Advanced security testing** (burp, ZAP) provides deeper attack simulation than ReadyAPI scanners.

---

## Useful built-in / advanced features (ReadyAPI)
- **Automated security scans** (OWASP-inspired checks)  
- **Enhanced reporting** (HTML/PDF) and test history  
- **TestCase scheduling and team collaboration** (via ReadyAPI TestServer / LoadUI Pro)  
- **Integration with source control and CI** via maven plugin or CLI

---

## Resources & official references
- SoapUI Open Source docs & downloads — SmartBear: https://www.soapui.org  
- ReadyAPI (commercial) documentation & tutorials — SmartBear: https://support.smartbear.com/readyapi/  
- Groovy scripting in SoapUI (assertions & custom steps): see SoapUI docs and Groovy docs for language references.  
- CLI (`testrunner`) manual pages in SoapUI/ReadyAPI installation directories.

---

## Quick checklist to make a SoapUI/ReadyAPI test CI-ready
- ✅ Parameterize endpoints and credentials via Environment variables.  
- ✅ Externalize test data (CSV / DB).  
- ✅ Use `testrunner` (CLI) with report flags in CI.  
- ✅ Fail the build if critical TestSuites fail (non-zero return codes).  
- ✅ Persist logs and result artifacts for debugging failed CI runs.

---

## Short example: run a TestSuite from CLI and fail build on errors
```bash
/path/to/ready-api/bin/testrunner.sh -s "LoginSuite" -c "ValidLogin" -r -f results MyProject.xml
if [ $? -ne 0 ]; then
  echo "API tests failed - exiting build"
  exit 1
fi
```

---

## Final notes
- SoapUI is a great entry point for API testing — build skills in requests, assertions, property transfers, and then move into automation via `testrunner` or Maven.  
- ReadyAPI is the natural upgrade when you need robust reporting, security and load features, and smoother CI/CD integration.  
- For teams that prefer "code-first" workflows, consider RestAssured (Java), Postman + Newman, or language-native libraries for test-as-code practice.

