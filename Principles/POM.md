## Page Object Model Pattern
POM is a design pattern, popularly used in test automation that creates Object Repository for UI elements. 
Under this model, for each UI page in the application, there should be a corresponding Page Class. This Page class will identify the UIElements of that page and also contains Page methods which perform operations on those UIElements

![POM Design Pattern](/Principles/images/POM-Design-Pattern.png)

![Basic Structure of POM framework](/Principles/images/POM-structure.png)

## Advantages of Page Object Model approach
**Code reusability** – If multiple test scripts use the same XCUIElement, then we need not write code to handle the element in every test. Instead placing it in a separate page class makes it reusable by making it accessible by any test script.

**Code maintainability** – There is a clean separation between test code and page object code such as locators and layout which becomes very easy to maintain code. Updating the code is very easy if any XCUIElement updates or a new one adds. It enhances test maintenance and reduces code duplication.

**Readability** – Improves readability due to clean separation between test code and page specific code

## Page Object Model Guidelines
- **Each page/screen should have a separate page class** and it should contain all UI elements and methods/page actions for that page.
- **Do not write assertion in page class**, page class should contain only the behavior. 
- **The assertion should be written in the test class** or its helper class.
- **Do not use application(XCUIApplication) APIs in the test class.**

The above guideline is extracted from [martinfowler.com](https://martinfowler.com/bliki/PageObject.html)   (Martin Fowler, creator of POM pattern)

### Sample Page Object Class
```

import XCTest

class WelcomeScreen: BaseScreenClass {
    
    let app: XCUIApplication
    let welcomeLabel: XCUIElement
    let welcomeDesc: XCUIElement
    let getStartedButton: XCUIElement
    
    init(_ app: XCUIApplication) {
        self.app = app
        welcomeLabel = app.staticTexts["Welcome to the organization"]
        welcomeDesc = app.staticTexts["Securely sign in to your organization's apps"]
        getStartedButton = app.buttons["Get Started"]
    }
    
    // MARK: Screen Actions

    func isLoaded() -> Bool {
        return welcomeLabel.waitForExistence(timeout: 10)
    }
    
    func tapGetStartedButton() -> HowItWorksScreen {
        getStartedButton.tap()
        return HowItWorksScreen(app)
    }
}
```

### Sample Test Class
```

import XCTest

class AccountEnrollment: BaseTestCase {
    
    var welcomeScreen: WelcomeScreen!
    var howItWorksScreen: HowItWorksScreen!
    var loginScreen: LoginScreen!
    
    override func setUp() {
        super.setUp()
        welcomeScreen = WelcomeScreen(app)
        resetEnrollments(user)
    }
    
    func testEnrollNewAccount() {
        XCTAssertTrue(welcomeScreen.isLoaded())
        howItWorksScreen = welcomeScreen.tapGetStartedButton()
        XCTAssertTrue(howItWorksScreen.isLoaded())
        loginScreen = howItWorksScreen.tapNextButton()
        XCTAssertTrue(loginScreen.isLoaded())
    }
}
```


## Improve test readability
We can follow BDD stype or user test step name as a method name and use XCTActivity to write better readable code.

```
    // Sample BDD style
    func testNewUserLogin() {
        givenUserInLoginPage()
        whenUserEnterCredentialsAndClickSubmitBtn()
        thenLoginIsSuccessful()
    }
```

```
    // Organized the test actions using XCTActivity
    func whenUserEnterCredentialsAndClickSubmitBtn() {
        XCTContext.runActivity(named: "when User enter Credentials And Click Submit Btn") {_ in
            loginHelper.enterUserID(user.userID)
            loginHelper.enterPassword(user.password)
            loginHelper.tapSubmitButton()
        }
    }
```

