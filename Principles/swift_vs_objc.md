<img src="https://d2o2utebsixu4k.cloudfront.net/media/images/0deb7fc8-4b92-4f33-a8c9-e48e3676c892.jpg" align="right" width="256px" style="border-radius: 10px;"/>

# Objective-C vs. Swift

<!-- TOC depthFrom:2 -->

- [Purpose](#purpose)
- [Background](#background)
    - [Language Usage](#language-usage)
    - [Objective-C](#objective-c)
        - [Advantages: Objective-C](#advantages-objective-c)
        - [Disadvantages: Objective-C](#disadvantages-objective-c)
    - [Swift](#swift)
        - [Advantages: Swift](#advantages-swift)
        - [Disadvantages: Swift](#disadvantages-swift)
- [Proposal](#proposal)
    - [Devices SDK](#devices-sdk)
    - [Authenticator Client](#authenticator-client)
    - [FAQ](#faq)

<!-- /TOC -->

## Purpose

As Okta works toward being awesome at client software, it is important to ensure that new and improved technology is evaluated as it becomes available. As developers add new or refactor existing features throughout the different iOS codebases, we need to provide a clear definition of which design pattern to use, code-style guidelines, and programming language preference.

This document provides clear language boundaries for iOS developers who contribute to Okta's mobile clients.

## Background

Today, Okta's iOS client applications are almost exclusively written in Objective-C, while our DevEx SDKs are primarily written in Swift.

Team members began experimenting with Swift starting in September 2017 for UI testing. In February 2019, the first `.swift` file was included into our core application. Since the initial integration of Swift, **100%** UI tests are now written in Swift.

As a result of adding Swift into our core Okta Mobile application, the total IPA size grew from 12.19MB to 26.8MB (+14.61) due to the inclusion of Swift runtime binaries.

### Language Usage

| Client            | Language    |                           Percentage |
|-------------------|-------------|-------------------------------------:|
| **Okta Mobile**   |             |                                      |
|                   | Objective-C |                                42.9% |
|                   | Swift       |                                 4.1% |
|                   | Shell       |                                 3.2% |
|                   | Other       |                                49.8% |
| **Okta Verify**   |             |                                      |
|                   | Objective-C |                                68.5% |
|                   | Swift       |                                20.5% |
|                   | Shell       |                                 9.5% |
|                   | Other       |                                 1.5% |

> Percentages are based on application, test, and script source files as of 2/14/20.

### Objective-C

As shown above, Objective-C has been historically been the go-to language for Okta's development team. All team members have experience using the language and have is actively used in production. Let's examine a few of Objective-C's advantages over it's counterpart.

#### Advantages: Objective-C

1. **Team experience:** All developers are skilled using Objective-C and have a proven track record of shipping features quickly and correctly.

2. **Tight deadlines:** As we target Oktane 2020 for the launch of our new Authenticator app, learning a new language (even a simple one) requires a significant amount of time and effort. Can current non-Swift developers lean on the subset of Swift experts to hit our deliverables?

3. **Language Stability:** Industry proven and tested for more than 30+ years. The API contracts have not changed (outside of iOS updates), requiring developers to update their applications. With Swift, developers are encouraged to update the language when new major versions become stable.

4. **Interop with C++:** As a first-class citizen of iOS, adding C++ files to an Objective-C project is a simple as changing the file extension from `.m` to `.mm`. While we currently do not use C++ in any of our codebases, it is frequently used for code sharing across multiple platforms.

5. **OCMock:** One of the most widely used mocking frameworks, [OCMock](http://ocmock.org/) is a powerful test dependency for stubbing and mocking application logic. Nearly all existing unit tests leverage this library.

6. **Dynamic language:** Features like method swizzling and key-value observing (KVO) are used to accomplish specific tasks in our codebase today. These features, along with complex macro definitions are **not** easily supported in Swift.

#### Disadvantages: Objective-C

1. **Language Development**: In the future, it is likely that no updates will be made for new features or the runtime environment. Apple's documentation, 3rd party blogs, and online forums are consistently evolving to reference Swift as the clear choice for all development on Apple's ecosystem.

2. **Namespacing**: All classes are required to be globally unique, otherwise, import issues are bound to occur. As a result, Okta prefixes all current files with `Okta`, `OKT`, `OLP`, and `OKU` to avoid such collisions in our applications and libraries.

### Swift

Created by Apple in 2014, [Swift](https://swift.org) has developed into one of the [most loved](https://insights.stackoverflow.com/survey/2019#technology-_-most-loved-dreaded-and-wanted-languages) programming languages in recent years.

#### Advantages: Swift

With Swift 5, we have a number of benefits over Objective-C:

1. **Faster development time**: Easy to read and write, Swift syntax is significantly cleaner and more expressive than Objective-C. As an example, [Lyft rewrote their iOS app](https://www.fastcompany.com/3050266/tech-forecast/lyft-goes-swift-how-and-why-it-rewrote-its-app-from-scratch-in-apples-new-lang) in Swift, reducing approximately 75,000 lines of code to 22,500 (30%).

2. **Improved performance**: Boasts a [2.6x performance increase](https://www.apple.com/swift/) and strong type system through static code analysis. Catching these errors early creates a faster feedback loop for our development team.

3. **Support**: As an [open sourced](https://github.com/apple/swift) language, developers can easily debug the source code directly, reach out to maintainers for questions, and participate in a large [Swift community](https://swift.org/community/#communication).

4. **Modern language**: Feature-rich with new features, this modern language allows developers to utilize static typing, optional variables, clear mutability syntax, functional patterns, and concise syntax.

5. **Stable ABI and Binary Compatibility**: With Swift 5, binaries are now incorporated into every macOS, iOS, tvOS, and watchOS release. This significantly reduces app size bloat as Swift runtime libraries are packaged with the OS.

6. **Performance**: Swift 5 runtime is now deeply integrated and optimized with the host OS, allowing programs to launch faster, get better runtime performance, and use less memory.

7. **Swift Package Manager**: Third party libraries can **finally** ship binary frameworks written in Swift, using the Swift Package Manager ([SPM](https://swift.org/package-manager/)).

8. **[SwiftUI](https://developer.apple.com/documentation/swiftui)**: Library of UI views, controls, and layout structures that can be used for designing a user interface. This allows code sharing between applications on all Apple platforms.

#### Disadvantages: Swift

1. **Unproven**: Since it's launch in 2014, we've seen **5** major releases. Swift's rapid development causes some friction in the community, forcing developers to constantly upgrade their versions to support Apple's new features + APIs. While we're seeing more companies [migrate to Swift](https://stackshare.io/swift), it has yet to become a universal language standard for Apple development.

2. **Longer compilation time**: Unlike Objective-C's progressive compilation, Swift will compile all files with any code change. With Xcode 10 and the new build system, we saw recent improvements with compilation time; however it requires a bit of additional [developer setup](https://github.com/fastred/Optimizing-Swift-Build-Times).

## Proposal

With [recent enhancements](#swift) to the language, Swift should be the primary programming language used by our developers moving forward. That being said, this is **not** a one-size-fits-all solution, as developers should ultimately use the right tool for the job. Our goal is **not** to migrate our existing codebase over to one language completely, but to gradually introduce it to Swift.

In order to help identify when and how Swift code should be used, please see the table below.

| Use Case             | Description                                     | Objective-C |   Swift |
|----------------------|-------------------------------------------------|------------:|--------:|
| **New Feature**      |                                                 |             |         |
|                      | Requires new classes or files                   |             | **Yes** |
|                      | Requires adding functionality to existing files |     **Yes** |         |
|                      | Requires refactoring existing files             |     **Yes** | **Yes** |
|                      | Bug-fixes                                       |             | **Yes** |
| **Existing Feature** |                                                 |             |         |
|                      | Requires new classes/files                      |             | **Yes** |
|                      | Requires adding functionality to existing files |     **Yes** |         |
|                      | Requires refactoring existing files             |     **Yes** | **Yes** |
|                      | Bug-fixes                                       |     **Yes** |         |
| **UI Tests**         |                                                 |             | **Yes** |
| **Unit Tests**       |                                                 |             |         |
|                      | Feature written in Objective-C                  |     **Yes** |         |
|                      | Feature written in Swift                        |             | **Yes** |

### Devices SDK

The new [`okta-devices-swift`](https://github.com/okta/okta-devices-swift) SDK is a new library that our existing Okta Verify client (_to be renamed Authenticator_) will consume. This SDK will be written exclusively in Swift.

In order to ensure that we're leveraging APIs and that are compatible with **both** Objective-C and Swift projects, we should adhere to the following guidelines:

1. **Enforce style linting**: Leveraging an existing [ruleset](https://github.com/realm/SwiftLint/blob/master/Rules.md) and/or creating our own lint rules will reduce the possibility of interop conflicts. As an example, Airbnb's style-guide contains an [Objective-C Interoperability](https://github.com/airbnb/swift#objective-c-interoperability) section to overcome this issue.

2. **Sample Applications**: SDKs often embed a small sample application into the repository for end-to-end testing. Instead of writing two sample applications for each language, we can utilize a language-specific shim pattern for wrapping the SDK functionality. Therefore, test targets can leverage the same sample application but traverse different language paths - ultimately calling the same SDK method signatures.

### Authenticator Client

The Okta Verify app is the client implementation leveraging our new Devices SDK. Developers should reference the table above when making code changes, understanding that there sometimes exceptions to the rules:

1. **File Refactoring**: Occasionally new or existing features require minor refactoring. Dependant on complexity, developers should examine the level of effort of rewriting the existing file in Swift. Consider the following examples:
    - Client needs to extend the existing color schemes:
        - Developers should **migrate** the existing `OktaColor.m` to `OktaColor.swift`, keeping the existing method signature contract.

    ```swift
    // ObjC
    + (UIColor *)cOffWhite {
        return [UIColor colorWithRed:250/255.0 green:250/255.0 blue:250/255.0 alpha:1];
    }

    // Swift
    class func cOffWhite() -> UIColor {
        return UIColor(red: 250/255.0, green: 250/255.0, blue: 250/255.0, alpha: 1)
    }
    ```

    - Client needs to register the device using our new IDX endpoints:
        - Developers should **not** rewrite the `OktaAPIClient.m` file in Swift, instead creating a method that will delegate the responsibility to the Devices SDK. Our existing client implementation **should not be leveraging SDK functionality**.

2. **Bug Fixes**: With bugs, time is typically of the essence. For most scenarios, bug-fixes should be resolved using the same language as the file containing the fix. In rare cases, we need to create new files to satisfy the issue.

### FAQ

> **How do Swift and Objective-C interop at the application level?**

Apple provides an excellent walkthrough for developers:

- [Importing Swift into Objective-C](https://developer.apple.com/documentation/swift/imported_c_and_objective-c_apis/importing_swift_into_objective-c)
- [Importing Objective-C into Swift](https://developer.apple.com/documentation/swift/imported_c_and_objective-c_apis/importing_objective-c_into_swift)