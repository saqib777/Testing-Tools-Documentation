# Ranorex Studio — Cross-Platform UI Automation

## What is Ranorex Studio?
**Ranorex Studio** is an all-in-one test automation tool for web, desktop, and mobile apps.  
It focuses on **GUI testing**, combining **codeless automation** with **C# and VB.NET scripting** for advanced control.  
Ranorex integrates seamlessly with CI/CD tools and supports a wide range of technologies including HTML5, Angular, React, WPF, and WinForms.

Official site: [https://www.ranorex.com](https://www.ranorex.com)

---

## Why use Ranorex?
- 🚀 **Supports all major platforms** (Windows desktop, web browsers, Android/iOS).  
- 🧩 **Codeless + Scripted approach** — record actions or write C#/VB.NET code.  
- 🔍 **Powerful object recognition** using RanoreXPath — robust locators for dynamic UIs.  
- 📱 **Mobile testing included** — test native, hybrid, and web apps.  
- 🧠 **Smart reporting** with screenshots, logs, and video.  
- 🤝 Integrates with **Git, Jenkins, Azure DevOps, Jira, TestRail**, and others.

---

## Key Features

### 1. Cross-Technology Support
- Web: Chrome, Firefox, Edge, Safari  
- Desktop: WPF, WinForms, Java, Delphi, Qt  
- Mobile: Android/iOS (native + webview)

### 2. Object Repository & RanoreXPath
- Centralized object repository makes locator updates easy.  
- **RanoreXPath** (like XPath but for UI) locates elements dynamically.  
- Auto-adapts to UI changes when possible.

### 3. Codeless Test Creation
- Record-and-replay functionality using the built-in Recorder.  
- Drag and drop test steps, conditions, loops, and variables visually.

### 4. Full Scripting Support
- Extend any test with C# or VB.NET in Visual Studio-like environment.  
- Reuse test modules and classes across projects.

### 5. Data-Driven Testing
- Pull data from Excel, CSV, SQL databases, or external APIs.  
- Combine with parameterized variables for flexible test cases.

### 6. Continuous Testing
- Command-line runner and integration with CI/CD (Jenkins, Bamboo, GitLab).  
- Supports remote and parallel test execution.

---

## Example (C# Web Test)
```csharp
[TestModule("D6E6F4C8-12A8-4B9D-9A3A-12345ABCDE")]
public class LoginTest : ITestModule
{
    public void Run()
    {
        var repo = YourAppRepository.Instance;
        repo.WebApp.LoginPage.UsernameField.PressKeys("user1");
        repo.WebApp.LoginPage.PasswordField.PressKeys("pass123");
        repo.WebApp.LoginPage.LoginButton.Click();
        Validate.Exists(repo.WebApp.Dashboard.WelcomeMessage);
    }
}
```

---

## Setup & Workflow
1. Install Ranorex Studio.  
2. Create a **Solution → Test Suite → Test Case**.  
3. Record a test scenario using Recorder or write a scripted test.  
4. Store locators in Object Repository.  
5. Add validation steps (text, existence, image checks).  
6. Run locally or configure CI/CD execution.  
7. Review results in Ranorex Report Viewer (includes screenshots & logs).

---

## Best Practices
- Reuse modules for common actions (Login, Logout, Navigation).  
- Organize test cases logically (Smoke, Regression, Functional).  
- Maintain a clean and descriptive object repository.  
- Use data-driven tests for coverage without duplication.  
- Validate dynamically loaded content using waits and conditional logic.  
- Regularly sync tests with Git for version control.

---

## Pros and Cons

**Pros**
- Very user-friendly with strong object recognition.  
- Supports both technical and non-technical users.  
- Professional reports with videos and screenshots.  
- Great cross-platform coverage.

**Cons**
- Windows-only IDE (can test other platforms remotely).  
- Commercial license required after trial.  
- Tests can get large/heavy if not modularized.

---

## Integration Highlights
- CI/CD: Jenkins, Azure DevOps, GitLab CI  
- ALM Tools: Jira, TestRail, Zephyr  
- Version Control: Git, SVN  
- Command Line Runner for unattended execution

---

## Resources
- Docs: [https://www.ranorex.com/help/latest](https://www.ranorex.com/help/latest)  
- Academy: [https://academy.ranorex.com](https://academy.ranorex.com)  
- GitHub Samples: [https://github.com/ranorex](https://github.com/ranorex)  
- Blog: [“Automated UI Testing Made Easy”](https://www.ranorex.com/blog/ui-automation/)

---

## Summary
**Ranorex Studio** bridges the gap between testers and developers — providing a clean visual interface and full scripting power.  
For web, desktop, and mobile testing in .NET environments, it’s one of the most comprehensive end-to-end UI automation tools available.  
It’s especially effective for enterprise teams that need **robust object handling**, **cross-platform coverage**, and **detailed reporting** all in one package.

---

