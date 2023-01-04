# Okta Swift Style Guide

## Introduction

This document outlines Okta's Swift lint rules, containing examples from the [SwiftLint Rule documentation](https://github.com/realm/SwiftLint/blob/master/Rules.md).

To adopt these rules, embed the [`.swiftlint.yml`](/Swift/.swiftlint.yml) file into your project.

**Table of Contents**

<!-- TOC depthFrom:2 -->

- [Introduction](#introduction)
- [Spacing](#spacing)
    - [Opening Brace](#opening-brace)
    - [Closing Brace](#closing-brace)
    - [Closure](#closure)
    - [Comma](#comma)
- [Whitespace](#whitespace)
    - [Leading](#leading)
    - [Trailing](#trailing)
    - [Operator Function](#operator-function)
    - [Operator Usage](#operator-usage)
    - [Variable Declaration](#variable-declaration)
    - [Returning](#returning)
- [Empty](#empty)
    - [Empty Collection Literal](#empty-collection-literal)
    - [Empty Count](#empty-count)
    - [Empty String](#empty-string)
- [Force](#force)
    - [Force Cast](#force-cast)
    - [Force Try](#force-try)
    - [Force Unwrapping](#force-unwrapping)
- [Ordering](#ordering)
    - [File Types Order](#file-types-order)
    - [Modifier Order](#modifier-order)
    - [Protocol Property Accessors Order](#protocol-property-accessors-order)
- [Closures](#closures)
    - [Closure Body Length](#closure-body-length)
    - [Closure End Indentation](#closure-end-indentation)
    - [Closure Parameter Position](#closure-parameter-position)
- [Style](#style)
    - [Attributes](#attributes)
    - [Collection Element Alignment](#collection-element-alignment)
    - [Control Statement](#control-statement)
    - [File Header](#file-header)
    - [Implicit Return](#implicit-return)
- [Lint](#lint)
    - [AnyObject Protocol](#anyobject-protocol)
    - [Class Delegate Protocol](#class-delegate-protocol)
    - [Cyclomatic Complexity](#cyclomatic-complexity)

<!-- /TOC -->

## Spacing

- Always use **4** spaces to indent, not Tabs.
- Make liberal use of vertical whitespace to divide code into logical chunks.
- There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but often there should probably be new methods.

### Opening Brace

![SwiftLint: opening_brace](https://img.shields.io/badge/SwiftLint-opening_brace-007A87.svg)

Opening braces should be preceded by a single space and on the same line as the declaration.

**Example**:

<details>
<summary>Correct</summary>

```swift
func abc() {
}
```

```swift
[].map() { $0 }
```

```swift
[].map({ })
```

```swift
if let a = b { }
```

```swift
while a == b { }
```

```swift
guard let a = b else { }
```

```swift
if
    let a = b,
    let c = d
    where a == c
{ }
```

```swift
while
    let a = b,
    let c = d
    where a == c
{ }
```

```swift
guard
    let a = b,
    let c = d
    where a == c else
{ }
```

```swift
struct Rule {}
```

```swift
struct Parent {
    struct Child {
        let foo: Int
    }
}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
func abc()↓{
}
```

```swift
func abc()
    ↓{ }
```

```swift
[].map()↓{ $0 }
```

```swift
[].map( ↓{ } )
```

```swift
if let a = b↓{ }
```

```swift
while a == b↓{ }
```

```swift
guard let a = b else↓{ }
```

```swift
if
    let a = b,
    let c = d
    where a == c↓{ }
```

```swift
while
    let a = b,
    let c = d
    where a == c↓{ }
```

```swift
guard
    let a = b,
    let c = d
    where a == c else↓{ }
```

```swift
struct Rule↓{}
```

```swift
struct Rule
↓{
}
```

```swift
struct Rule
    ↓{
}
```

```swift
struct Parent {
    struct Child
    ↓{
        let foo: Int
    }
}
```

</details>

### Closing Brace

![SwiftLint: closing_brace](https://img.shields.io/badge/SwiftLint-closing_brace-007A87.svg)

Closing brace with closing parenthesis should not have any whitespaces in the middle.

**Example:**

<details>
<summary>Correct</summary>

```swift
[].map({ })
```

```swift
[].map(
  { }
)
```

</details>

<details>
<summary>Incorrect</summary>

```swift
[].map({ ↓} )
```

```swift
[].map({ ↓}	)
```

</details>

### Closure

![SwiftLint: closure_spacing](https://img.shields.io/badge/SwiftLint-closure_spacing-007A87.svg)

Closure expressions should have a single space inside each brace.

**Example**:

<details>
<summary>Correct</summary>

```swift
[].map ({ $0.description })
```

```swift
[].filter { $0.contains(location) }
```

```swift
extension UITableViewCell: ReusableView { }
```

```swift
extension UITableViewCell: ReusableView {}
```

</details>
<details>
<summary>Incorrect</summary>

```swift
[].filter(↓{$0.contains(location)})
```

```swift
[].map(↓{$0})
```

```swift
(↓{each in return result.contains(where: ↓{e in return e}) }).count
```

```swift
filter ↓{ sorted ↓{ $0 < $1}}
```

</details>

### Comma

![SwiftLint: comma](https://img.shields.io/badge/SwiftLint-comma-007A87.svg)

There should be no space before and one after any comma.

**Example:**

<details>
<summary>Correct</summary>

```swift
func abc(a: String, b: String) { }
```

```swift
abc(a: "string", b: "string"
```

```swift
enum a { case a, b, c }
```

```swift
func abc(
  a: String,  // comment
  bcd: String // comment
) {
}
```

```swift
func abc(
  a: String,
  bcd: String
) {
}
```

```swift
#imageLiteral(resourceName: "foo,bar,baz")
```

</details>

<details>
<summary>Incorrect</summary>

```swift
func abc(a: String↓ ,b: String) { }
```

```swift
func abc(a: String↓ ,b: String↓ ,c: String↓ ,d: String) { }
```

```swift
abc(a: "string"↓,b: "string"
```

```swift
enum a { case a↓ ,b }
```

```swift
let result = plus(
    first: 3↓ , // #683
    second: 4
)
```

</details>

## Whitespace

### Leading

![SwiftLint: leading_whitespace](https://img.shields.io/badge/SwiftLint-leading_whitespace-007A87.svg)

Files should not contain leading whitespace.

**Example:**

<details>
<summary>Correct</summary>

```swift
//
```

</details>

<details>
<summary>Incorrect</summary>

```swift
```

```swift
 //
```

</details>

### Trailing

![SwiftLint: trailing_whitespace](https://img.shields.io/badge/SwiftLint-trailing_whitespace-007A87.svg)

Lines should not have trailing whitespace.

**Example:**

<details>
<summary>Correct</summary>

```swift
let name: String
```

```swift
//
```

```swift
let name: String //
```

</details>

<details>
<summary>Incorrect</summary>

```swift
let name: String 
```

```swift
/* */ let name: String 
```

</details>

### Operator Function

![SwiftLint: operator_whitespace](https://img.shields.io/badge/SwiftLint-operator_whitespace-007A87.svg)

Operators should be surrounded by a single whitespace when defining them.

**Example:**

<details>
<summary>Correct</summary>

```swift
func <| (lhs: Int, rhs: Int) -> Int {}
```

```swift
func <|< <A>(lhs: A, rhs: A) -> A {}
```

```swift
func abc(lhs: Int, rhs: Int) -> Int {}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
↓func <|(lhs: Int, rhs: Int) -> Int {}
```

```swift
↓func <|<<A>(lhs: A, rhs: A) -> A {}
```

```swift
↓func <|  (lhs: Int, rhs: Int) -> Int {}
```

```swift
↓func <|<  <A>(lhs: A, rhs: A) -> A {}
```

```swift
↓func  <| (lhs: Int, rhs: Int) -> Int {}
```

```swift
↓func  <|< <A>(lhs: A, rhs: A) -> A {}
```

</details>

### Operator Usage

![SwiftLint: operator_usage_whitespace](https://img.shields.io/badge/SwiftLint-operator_usage_whitespace-007A87.svg)

Operators should be surrounded by a single whitespace when they are being used.

**Example:**

<details>
<summary>Correct</summary>

```swift
let foo = 1 + 2
```

```swift
let foo = 1 > 2
```

```swift
let foo = !false
```

```swift
let foo: Int?
```

```swift
let foo: Array<String>
```

```swift
let model = CustomView<Container<Button>, NSAttributedString>()
```

```swift
let foo: [String]
```

```swift
let foo = 1 + 
  2
```

```swift
let range = 1...3
```

```swift
let range = 1 ... 3
```

```swift
let range = 1..<3
```

```swift
#if swift(>=3.0)
    foo()
#endif
```

```swift
array.removeAtIndex(-200)
```

```swift
let name = "image-1"
```

```swift
button.setImage(#imageLiteral(resourceName: "image-1"), for: .normal)
```

```swift
let doubleValue = -9e-11
```

```swift
let foo = GenericType<(UIViewController) -> Void>()
```

```swift
let foo = Foo<Bar<T>, Baz>()
```

```swift
let foo = SignalProducer<Signal<Value, Error>, Error>([ self.signal, next ]).flatten(.concat)
```

</details>

<details>
<summary>Incorrect</summary>

```swift
let foo = 1↓+2
```

```swift
let foo = 1↓   + 2
```

```swift
let foo = 1↓   +    2
```

```swift
let foo = 1↓ +    2
```

```swift
let foo↓=1↓+2
```

```swift
let foo↓=1 + 2
```

```swift
let foo↓=bar
```

```swift
let range = 1↓ ..<  3
```

```swift
let foo = bar↓   ?? 0
```

```swift
let foo = bar↓??0
```

```swift
let foo = bar↓ !=  0
```

```swift
let foo = bar↓ !==  bar2
```

```swift
let v8 = Int8(1)↓  << 6
```

```swift
let v8 = 1↓ <<  (6)
```

```swift
let v8 = 1↓ <<  (6)
 let foo = 1 > 2
```

</details>

### Variable Declaration

![SwiftLint: let_var_whitespace](https://img.shields.io/badge/SwiftLint-let_var_whitespace-007A87.svg)

Let and var should be separated from other statements by a blank line.

**Example:**

<details>
<summary>Correct</summary>

```swift
let a = 0
var x = 1
x = 2
```

```swift
a = 5
var x = 1
```

```swift
struct X {
	var a = 0
}
```

```swift
let a = 1 +
	2
let b = 5
```

```swift
var x: Int {
	return 0
}
```

```swift
var x: Int {
	let a = 0
	return a
}
```

```swift
#if os(macOS)
let a = 0
#endif
```

```swift
#warning("TODO: remove it")
let a = 0
```

```swift
#error("TODO: remove it")
let a = 0
```

```swift
@available(swift 4)
let a = 0
```

```swift
class C {
	@objc
	var s: String = ""
}
```

```swift
class C {
	@objc
	func a() {}
}
```

```swift
class C {
	var x = 0
	lazy
	var y = 0
}
```

```swift
@available(OSX, introduced: 10.6)
@available(*, deprecated)
var x = 0
```

```swift
// swiftlint:disable superfluous_disable_command
// swiftlint:disable force_cast
let x = bar as! Bar
```

```swift
var x: Int {
	let a = 0
	return a
}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
var x = 1
↓x = 2
```

```swift
a = 5
↓var x = 1
```

```swift
struct X {
	let a
	↓func x() {}
}
```

```swift
var x = 0
↓@objc func f() {}
```

```swift
var x = 0
↓@objc
	func f() {}
```

```swift
@objc func f() {
}
↓var x = 0
```

</details>

### Returning

![SwiftLint: return_arrow_whitespace](https://img.shields.io/badge/SwiftLint-return_arrow_whitespace-007A87.svg)

Return arrow and return type should be separated by a single space or on a separate line.

**Example:**

<details>
<summary>Correct</summary>

```swift
func abc() -> Int {}
```

```swift
func abc() -> [Int] {}
```

```swift
func abc() -> (Int, Int) {}
```

```swift
var abc = {(param: Int) -> Void in }
```

```swift
func abc() ->
    Int {}
```

```swift
func abc()
    -> Int {}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
func abc()↓->Int {}
```

```swift
func abc()↓->[Int] {}
```

```swift
func abc()↓->(Int, Int) {}
```

```swift
func abc()↓-> Int {}
```

```swift
func abc()↓ ->Int {}
```

```swift
func abc()↓  ->  Int {}
```

```swift
var abc = {(param: Int)↓ ->Bool in }
```

```swift
var abc = {(param: Int)↓->Bool in }
```

</details>

## Empty

### Empty Collection Literal

![SwiftLint: empty_collection_literal](https://img.shields.io/badge/SwiftLint-empty_collection_literal-007A87.svg)

Prefer checking `isEmpty` over comparing collection to an empty array or dictionary literal.

**Example:**

<details>
<summary>Correct</summary>

```swift
myArray = []
```

```swift
myArray.isEmpty
```

```swift
!myArray.isEmpty
```

```swift
myDict = [:]
```

</details>

<details>
<summary>Incorrect</summary>

```swift
myArray↓ == []
```

```swift
myArray↓ != []
```

```swift
myArray↓ == [ ]
```

```swift
myDict↓ == [:]
```

```swift
myDict↓ != [:]
```

```swift
myDict↓ == [: ]
```

```swift
myDict↓ == [ :]
```

```swift
myDict↓ == [ : ]
```

</details>

### Empty Count

![SwiftLint: empty_count](https://img.shields.io/badge/SwiftLint-empty_count-007A87.svg)

Prefer checking `isEmpty` over comparing `count` to zero.

**Example:**

<details>
<summary>Correct</summary>

```swift
var count = 0
```

```swift
[Int]().isEmpty
```

```swift
[Int]().count > 1
```

```swift
[Int]().count == 1
```

```swift
[Int]().count == 0xff
```

```swift
[Int]().count == 0b01
```

```swift
[Int]().count == 0o07
```

```swift
discount == 0
```

```swift
order.discount == 0
```

</details>

<details>
<summary>Incorrect</summary>

```swift
[Int]().↓count == 0
```

```swift
[Int]().↓count > 0
```

```swift
[Int]().↓count != 0
```

```swift
[Int]().↓count == 0x0
```

```swift
[Int]().↓count == 0x00_00
```

```swift
[Int]().↓count == 0b00
```

```swift
[Int]().↓count == 0o00
```

```swift
↓count == 0
```

</details>

### Empty String

![SwiftLint: empty_string](https://img.shields.io/badge/SwiftLint-empty_string-007A87.svg)

Prefer checking `isEmpty` over comparing `string` to an empty string literal.

**Example:**

<details>
<summary>Correct</summary>

```swift
myString.isEmpty
```

```swift
!myString.isEmpty
```

</details>

<details>
<summary>Incorrect</summary>

```swift
myString↓ == ""
```

```swift
myString↓ != ""
```

</details>

## Force

### Force Cast

![SwiftLint: force_cast](https://img.shields.io/badge/SwiftLint-force_cast-007A87.svg)

Force casts should be avoided.

**Example:**

<details>
<summary>Correct</summary>

```swift
NSNumber() as? Int
```

</details>

<details>
<summary>Incorrect</summary>

```swift
NSNumber() ↓as! Int
```

</details>

### Force Try

![SwiftLint: force_try](https://img.shields.io/badge/SwiftLint-force_try-007A87.svg)

Force tries should be avoided.

**Example:**

<details>
<summary>Correct</summary>

```swift
func a() throws {}
do {
  try a()
} catch {}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
func a() throws {}
↓try! a()
```

</details>

### Force Unwrapping

![SwiftLint: force_unwrapping](https://img.shields.io/badge/SwiftLint-force_unwrapping-007A87.svg)

Force unwrapping should be avoided.

**Example:**

<details>
<summary>Correct</summary>

```swift
if let url = NSURL(string: query)
```

```swift
navigationController?.pushViewController(viewController, animated: true)
```

```swift
let s as! Test
```

```swift
try! canThrowErrors()
```

```swift
let object: Any!
```

```swift
@IBOutlet var constraints: [NSLayoutConstraint]!
```

```swift
setEditing(!editing, animated: true)
```

```swift
navigationController.setNavigationBarHidden(!navigationController.navigationBarHidden, animated: true)
```

```swift
if addedToPlaylist && (!self.selectedFilters.isEmpty || self.searchBar?.text?.isEmpty == false) {}
```

```swift
print("\(xVar)!")
```

```swift
var test = (!bar)
```

```swift
var a: [Int]!
```

```swift
private var myProperty: (Void -> Void)!
```

```swift
func foo(_ options: [AnyHashable: Any]!) {
```

```swift
func foo() -> [Int]!
```

```swift
func foo() -> [AnyHashable: Any]!
```

```swift
func foo() -> [Int]! { return [] }
```

```swift
return self
```

</details>

<details>
<summary>Incorrect</summary>

```swift
let url = NSURL(string: query)↓!
```

```swift
navigationController↓!.pushViewController(viewController, animated: true)
```

```swift
let unwrapped = optional↓!
```

```swift
return cell↓!
```

```swift
let url = NSURL(string: "http://www.google.com")↓!
```

```swift
let dict = ["Boooo": "👻"]func bla() -> String { return dict["Boooo"]↓! }
```

```swift
let dict = ["Boooo": "👻"]func bla() -> String { return dict["Boooo"]↓!.contains("B") }
```

```swift
let a = dict["abc"]↓!.contains("B")
```

```swift
dict["abc"]↓!.bar("B")
```

```swift
if dict["a"]↓!!!! {
```

```swift
var foo: [Bool]! = dict["abc"]↓!
```

```swift
context("abc") {
  var foo: [Bool]! = dict["abc"]↓!
}
```

```swift
open var computed: String { return foo.bar↓! }
```

```swift
return self↓!
```

</details>

## Ordering

### File Types Order

![SwiftLint: file_types_order](https://img.shields.io/badge/SwiftLint-file_types_order-007A87.svg)

Specifies how the types within a file should be ordered. The preferred order is:

1. Supporting Types
2. Main Types
3. Extensions

**Example:**

<details>
<summary>Correct</summary>

```swift
// Supporting Types
protocol TestViewControllerDelegate {
    func didPressTrackedButton()
}
// Main Type
class TestViewController: UIViewController {
    // Type Aliases
    typealias CompletionHandler = ((TestEnum) -> Void)
    // Subtypes
    class TestClass {
        // 10 lines
    }
    struct TestStruct {
        // 3 lines
    }
    enum TestEnum {
        // 5 lines
    }
    // Stored Type Properties
    static let cellIdentifier: String = "AmazingCell"
    // Stored Instance Properties
    var shouldLayoutView1: Bool!
    weak var delegate: TestViewControllerDelegate?
    private var hasLayoutedView1: Bool = false
    private var hasLayoutedView2: Bool = false
    // Computed Instance Properties
    private var hasAnyLayoutedView: Bool {
         return hasLayoutedView1 || hasLayoutedView2
    }
    // IBOutlets
    @IBOutlet private var view1: UIView!
    @IBOutlet private var view2: UIView!
    // Initializers
    override init(nibName nibNameOrNil: String?, bundle nibBundleOrNil: Bundle?) {
        super.init(nibName: nibNameOrNil, bundle: nibBundleOrNil)
    }
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    // Type Methods
    static func makeViewController() -> TestViewController {
        // some code
    }
    // Life-Cycle Methods
    override func viewDidLoad() {
        super.viewDidLoad()
        view1.setNeedsLayout()
        view1.layoutIfNeeded()
        hasLayoutedView1 = true
    }
    override func viewDidLayoutSubviews() {
        super.viewDidLayoutSubviews()
        view2.setNeedsLayout()
        view2.layoutIfNeeded()
        hasLayoutedView2 = true
    }
    // IBActions
    @IBAction func goNextButtonPressed() {
        goToNextVc()
        delegate?.didPressTrackedButton()
    }
    @objc
    func goToRandomVcButtonPressed() {
        goToRandomVc()
    }
    // MARK: Other Methods
    func goToNextVc() { /* TODO */ }
    func goToInfoVc() { /* TODO */ }
    func goToRandomVc() {
        let viewCtrl = getRandomVc()
        present(viewCtrl, animated: true)
    }
    private func getRandomVc() -> UIViewController { return UIViewController() }
    // Subscripts
    subscript(_ someIndexThatIsNotEvenUsed: Int) -> String {
        get {
            return "This is just a test"
        }
        set {
            log.warning("Just a test", newValue)
        }
    }
}
// Extensions
extension TestViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 1
    }
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        return UITableViewCell()
    }
}
```

```swift
// Only extensions
extension Foo {}
extension Bar {
}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
↓class TestViewController: UIViewController {}
// Supporting Types
protocol TestViewControllerDelegate {
    func didPressTrackedButton()
}
```

```swift
// Extensions
↓extension TestViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 1
    }
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        return UITableViewCell()
    }
}
class TestViewController: UIViewController {}
```

```swift
// Supporting Types
protocol TestViewControllerDelegate {
    func didPressTrackedButton()
}
↓class TestViewController: UIViewController {}
// Supporting Types
protocol TestViewControllerDelegate {
    func didPressTrackedButton()
}
```

```swift
// Supporting Types
protocol TestViewControllerDelegate {
    func didPressTrackedButton()
}
// Extensions
↓extension TestViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 1
    }
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        return UITableViewCell()
    }
}
class TestViewController: UIViewController {}
// Extensions
extension TestViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 1
    }
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        return UITableViewCell()
    }
}
```

</details>

### Modifier Order

![SwiftLint: modifier_order](https://img.shields.io/badge/SwiftLint-modifier_order-007A87.svg)

Modifier order should be consistent. The preferred order is:

1. Override
2. ACL
3. Setter ACL
4. Dynamic
5. Mutators
6. Lazy
7. Final
8. Required
9. Convenience
10. Type Methods
11. Owned

**Example:**

<details>
<summary>Correct</summary>

```swift
public class Foo {
   public static var bar: Int {
       return 42
    }
}
```

```swift
public class Foo {
   public class var bar: Int {
       return 42
   }
}
```

```swift
public class Bar {
   public class var foo: String {
       return "foo"
   }
}
public class Foo: Bar {
   override public final class var foo: String {
       return "bar"
   }
}
```

```swift
open class Bar {
   public var foo: Int? {
       return 42
   }
}
open class Foo: Bar {
   override public var foo: Int? {
       return 43
   }
}
```

```swift
open class Bar {
   open class func foo() -> Int {
       return 42
   }
}
class Foo: Bar {
   override open class func foo() -> Int {
       return 43
   }
}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
public class Foo {
   class public var bar: Int {
       return 42
   }
}
```

```swift
public class RootFoo {
   class public var foo: String {
       return "foo"
   }
}
public class Foo: RootFoo {
   override final class public var foo: String {
       return "bar"
   }
}
```

```swift
open class Bar {
   public var foo: Int? {
       return 42
   }
}
open class Foo: Bar {
    public override var foo: Int? {
       return 43
   }
}
```

```swift
protocol Foo: class {}
class Bar {
    private(set) public weak var foo: Foo?
}
```

</details>

### Protocol Property Accessors Order

![SwiftLint: protocol_property_accessors_order](https://img.shields.io/badge/SwiftLint-protocol_property_accessors_order-007A87.svg)

When declaring properties in protocols, the order of accessors should be `get set`.

**Example:**

<details>
<summary>Correct</summary>

```swift
protocol Foo {
 var bar: String { get set }
 }
```

```swift
protocol Foo {
 var bar: String { get }
 }
```

```swift
protocol Foo {
 var bar: String { set }
 }
```

</details>

<details>
<summary>Incorrect</summary>

```swift
protocol Foo {
 var bar: String { ↓set get }
 }
```

</details>

## Closures

### Closure Body Length

![SwiftLint: closure_body_length](https://img.shields.io/badge/SwiftLint-closure_body_length-007A87.svg)

Closure bodies should not span too many lines.

| :warning: | :no_entry_sign: |
| ------ | ----- |
| 50 | 100 |

**Example:**

<details>
<summary>Correct</summary>

```swift
foo.bar { $0 }
```

```swift
foo.bar { toto in
}
```

```swift
foo.bar(label: { toto in
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
}) { toto in
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
}
```
</details>

<details>
<summary>Incorrect</summary>

```swift
foo.bar ↓{ toto in
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	let a = 0
	// toto
	// toto
	// toto
	// toto
	// toto
	// toto
	// toto
	// toto
	// toto
	// toto
	
	
	
	
	
	
	
	
	
	 // Up to line 100.
}
```
</details>

### Closure End Indentation

![SwiftLint: closure_end_indentation](https://img.shields.io/badge/SwiftLint-closure_end_indentation-007A87.svg)

Closure end should have the same indentation as the line that started it.

**Example:**

<details>
<summary>Correct</summary>

```swift
SignalProducer(values: [1, 2, 3])
   .startWithNext { number in
       print(number)
   }
```

```swift
[1, 2].map { $0 + 1 }
```

```swift
return match(pattern: pattern, with: [.comment]).flatMap { range in
   return Command(string: contents, range: range)
}.flatMap { command in
   return command.expand()
}
```

```swift
foo(foo: bar,
    options: baz) { _ in }
```

```swift
someReallyLongProperty.chainingWithAnotherProperty
   .foo { _ in }
```

```swift
foo(abc, 123)
{ _ in }
```

```swift
function(
    closure: { x in
        print(x)
    },
    anotherClosure: { y in
        print(y)
    })
```

```swift
function(parameter: param,
         closure: { x in
    print(x)
})
```

```swift
function(parameter: param, closure: { x in
        print(x)
    },
    anotherClosure: { y in
        print(y)
    })
```

</details>
<details>
<summary>Incorrect</summary>

```swift
SignalProducer(values: [1, 2, 3])
   .startWithNext { number in
       print(number)
↓}
```

```swift
return match(pattern: pattern, with: [.comment]).flatMap { range in
   return Command(string: contents, range: range)
   ↓}.flatMap { command in
   return command.expand()
↓}
```

```swift
function(
    closure: { x in
        print(x)
↓},
    anotherClosure: { y in
        print(y)
↓})
```

</details>

### Closure Parameter Position

![SwiftLint: closure_parameter_position](https://img.shields.io/badge/SwiftLint-closure_parameter_position-007A87.svg)

Closure parameters should be on the same line as opening brace.

**Example:**

<details>
<summary>Correct</summary>

```swift
[1, 2].map { $0 + 1 }
```

```swift
[1, 2].map({ $0 + 1 })
```

```swift
[1, 2].map { number in
 number + 1 
}
```

```swift
[1, 2].map { number -> Int in
 number + 1 
}
```

```swift
[1, 2].map { (number: Int) -> Int in
 number + 1 
}
```

```swift
[1, 2].map { [weak self] number in
 number + 1 
}
```

```swift
[1, 2].something(closure: { number in
 number + 1 
})
```

```swift
let isEmpty = [1, 2].isEmpty()
```

```swift
rlmConfiguration.migrationBlock.map { rlmMigration in
return { migration, schemaVersion in
rlmMigration(migration.rlmMigration, schemaVersion)
}
}
```

```swift
let mediaView: UIView = { [weak self] index in
   return UIView()
}(index)
```

</details>
<details>
<summary>Incorrect</summary>

```swift
[1, 2].map {
 ↓number in
 number + 1 
}
```

```swift
[1, 2].map {
 ↓number -> Int in
 number + 1 
}
```

```swift
[1, 2].map {
 (↓number: Int) -> Int in
 number + 1 
}
```

```swift
[1, 2].map {
 [weak self] ↓number in
 number + 1 
}
```

```swift
[1, 2].map { [weak self]
 ↓number in
 number + 1 
}
```

```swift
[1, 2].map({
 ↓number in
 number + 1 
})
```

```swift
[1, 2].something(closure: {
 ↓number in
 number + 1 
})
```

```swift
[1, 2].reduce(0) {
 ↓sum, ↓number in
 number + sum 
}
```

</details>

## Style

### Attributes

![SwiftLint: attributes](https://img.shields.io/badge/SwiftLint-attributes-007A87.svg)

Attributes should be on their own lines in functions and types, but on the same line as variables and imports.

**Example:**

<details>
<summary>Correct</summary>

```swift
@objc var x: String
```

```swift
@objc private var x: String
```

```swift
@nonobjc var x: String
```

```swift
@IBOutlet private var label: UILabel
```

```swift
@IBOutlet @objc private var label: UILabel
```

```swift
@available(iOS 9.0, *)
let stackView: UIStackView
```

```swift
@objc
@IBAction func buttonPressed(button: UIButton)
```

```swift
@available(iOS 13.0, *)
func animate(view: UIStackView)
```

```swift
@nonobjc
final class X
```

```swift
@available(iOS 13.0, *)
class UIStackView
```

</details>

<details>
<summary>Incorrect</summary>

```swift
@objc
 ↓var x: String
```

```swift
@objc
 private ↓var x: String
```

```swift
@nonobjc
 ↓var x: String
```

```swift
@IBOutlet
 private ↓var label: UILabel
```

```swift
@available(iOS 13.0, *) ↓let stackView: UIStackView
```

```swift
@available(iOS 13.0, *) ↓func animate(view: UIStackView)
```

</details>

### Collection Element Alignment

![SwiftLint: collection_alignment](https://img.shields.io/badge/SwiftLint-collection_alignment-007A87.svg)

All elements in a collection literal should be vertically aligned

**Example:**

<details>
<summary>Correct</summary>

```swift
doThings(arg: [
    "foo": 1,
    "bar": 2,
    "fizz": 2,
    "buzz": 2
])
```

```swift
let abc = [
    "alpha": "a",
    "beta": "b",
    "gamma": "g",
    "delta": "d",
    "epsilon": "e"
]
```

```swift
let meals = [
                "breakfast": "oatmeal",
                "lunch": "sandwich",
                "dinner": "burger"
]
```

```swift
let coordinates = [
    CLLocationCoordinate2D(latitude: 0, longitude: 33),
    CLLocationCoordinate2D(latitude: 0, longitude: 66),
    CLLocationCoordinate2D(latitude: 0, longitude: 99)
]
```

```swift
var evenNumbers: Set<Int> = [
    2,
    4,
    6
]
```

```swift
let abc = [1, 2, 3, 4]
```

```swift
let abc = [
    1, 2, 3, 4
]
```

```swift
let abc = [
    "foo": "bar", "fizz": "buzz"
]
```

</details>

<details>
<summary>Incorrect</summary>

```swift
doThings(arg: [
    "foo": 1,
    "bar": 2,
   ↓"fizz": 2,
   ↓"buzz": 2
])
```

```swift
let abc = [
    "alpha": "a",
     ↓"beta": "b",
    "gamma": "g",
    "delta": "d",
  ↓"epsilon": "e"
]
```

```swift
let meals = [
                "breakfast": "oatmeal",
                "lunch": "sandwich",
    ↓"dinner": "burger"
]
```

```swift
let coordinates = [
    CLLocationCoordinate2D(latitude: 0, longitude: 33),
        ↓CLLocationCoordinate2D(latitude: 0, longitude: 66),
    CLLocationCoordinate2D(latitude: 0, longitude: 99)
]
```

```swift
var evenNumbers: Set<Int> = [
    2,
  ↓4,
    6
]
```

</details>

### Control Statement

![SwiftLint: control_statement](https://img.shields.io/badge/SwiftLint-control_statement-007A87.svg)

`if`, `for`, `guard`, `switch`, `while`, `repeat-while`, and `catch` statements shouldn't unnecessarily wrap their conditionals or arguments in parentheses.

**Example:**

<details>
<summary>Correct</summary>

```swift
if condition {
```

```swift
if (a, b) == (0, 1) {
```

```swift
if (a || b) && (c || d) {
```

```swift
if (min...max).contains(value) {
```

```swift
if renderGif(data) {
```

```swift
renderGif(data)
```

```swift
for item in collection {
```

```swift
for (key, value) in dictionary {
```

```swift
for (index, value) in enumerate(array) {
```

```swift
for var index = 0; index < 42; index++ {
```

```swift
guard condition else {
```

```swift
while condition {
```

```swift
} while condition {
```

```swift
do { ; } while condition {
```

```swift
switch foo {
```

```swift
do {
} catch let error as NSError {
}
```

```swift
foo().catch(all: true) {}
```

```swift
if max(a, b) < c {
```

```swift
switch (lhs, rhs) {
```

</details>

<details>
<summary>Incorrect</summary>

```swift
↓if (condition) {
```

```swift
↓if(condition) {
```

```swift
↓if (condition == endIndex) {
```

```swift
↓if ((a || b) && (c || d)) {
```

```swift
↓if ((min...max).contains(value)) {
```

```swift
↓for (item in collection) {
```

```swift
↓for (var index = 0; index < 42; index++) {
```

```swift
↓for(item in collection) {
```

```swift
↓for(var index = 0; index < 42; index++) {
```

```swift
↓guard (condition) else {
```

```swift
↓while (condition) {
```

```swift
↓while(condition) {
```

```swift
} ↓while (condition) {
```

```swift
} ↓while(condition) {
```

```swift
do { ; } ↓while(condition) {
```

```swift
do { ; } ↓while (condition) {
```

```swift
↓switch (foo) {
```

```swift
do {
} ↓catch(let error as NSError) {
}
```

```swift
↓if (max(a, b) < c) {
```

</details>

### File Header

![SwiftLint: file_header](https://img.shields.io/badge/SwiftLint-file_header-007A87.svg)

Header comments should be consistent with project patterns. The `SWIFTLINT_CURRENT_FILENAME` placeholder can optionally be used in the required and forbidden patterns. It will be replaced by the real file name.

### Implicit Return

![SwiftLint: implicit_return](https://img.shields.io/badge/SwiftLint-implicit_return-007A87.svg)

Prefer implicit returns in closures, functions and getters.

**Example:**

<details>
<summary>Correct</summary>

```swift
if foo {
  return 0
}
```

```swift
foo.map { $0 + 1 }
```

```swift
foo.map({ $0 + 1 })
```

```swift
foo.map { value in value + 1 }
```

```swift
[1, 2].first(where: {
    true
})
```

```swift
func foo() -> Int {
    0
}
```

```swift
class Foo {
    func foo() -> Int { 0 }
}
```

```swift
func fetch() -> Data? {
    do {
        return try loadData()
    } catch {
        return nil
    }
}
```

```swift
var foo: Bool { true }
```

```swift
class Foo {
    var bar: Int {
        get {
            0
        }
    }
}
```

```swift
class Foo {
    static var bar: Int {
        0
    }
}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
foo.map { value in
    return value + 1
}
```

```swift
foo.map {
    return $0 + 1
}
```

```swift
foo.map({ return $0 + 1})
```

```swift
[1, 2].first(where: {
    return true
})
```

```swift
func foo() -> Int {
    return 0
}
```

```swift
class Foo {
    func foo() -> Int { return 0 }
}
```

```swift
var foo: Bool { return true }
```

```swift
class Foo {
    var bar: Int {
        get {
            return 0
        }
    }
}
```

```swift
class Foo {
    static var bar: Int {
        return 0
    }
}
```

</details>

## Lint

### AnyObject Protocol

![SwiftLint: anyobject_protocol](https://img.shields.io/badge/SwiftLint-anyobject_protocol-007A87.svg)

Prefer using `AnyObject` over `class` for class-only protocols.

**Example:**

<details>
<summary>Correct</summary>

```swift
protocol SomeProtocol {}
```

```swift
protocol SomeClassOnlyProtocol: AnyObject {}
```

```swift
protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {}
```

```swift
@objc protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
protocol SomeClassOnlyProtocol: ↓class {}
```

```swift
protocol SomeClassOnlyProtocol: ↓class, SomeInheritedProtocol {}
```

```swift
@objc protocol SomeClassOnlyProtocol: ↓class, SomeInheritedProtocol {}
```

</details>

### Class Delegate Protocol

![SwiftLint: class_delegate_protocol](https://img.shields.io/badge/SwiftLint-class_delegate_protocol-007A87.svg)

Delegate protocols should be class-only so they can be weakly referenced.

**Example:**

<details>
<summary>Correct</summary>

```swift
protocol FooDelegate: class {}
```

```swift
protocol FooDelegate: class, BarDelegate {}
```

```swift
protocol Foo {}
```

```swift
class FooDelegate {}
```

```swift
@objc protocol FooDelegate {}
```

```swift
@objc(MyFooDelegate)
 protocol FooDelegate {}
```

```swift
protocol FooDelegate: BarDelegate {}
```

```swift
protocol FooDelegate: AnyObject {}
```

```swift
protocol FooDelegate: NSObjectProtocol {}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
↓protocol FooDelegate {}
```

```swift
↓protocol FooDelegate: Bar {}
```

</details>

### Cyclomatic Complexity

![SwiftLint: cyclomatic_complexity](https://img.shields.io/badge/SwiftLint-cyclomatic_complexity-007A87.svg)

Complexity of function bodies should be limited.

**Example:**

<details>
<summary>Correct</summary>

```swift
func f1() {
if true {
for _ in 1..5 { } }
if false { }
}
```

```swift
func f(code: Int) -> Int {switch code {
 case 0: fallthrough
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
default: return 1}}
```

```swift
func f1() {if true {}; if true {}; if true {}; if true {}; if true {}; if true {}
func f2() {
if true {}; if true {}; if true {}; if true {}; if true {}
}}
```

</details>

<details>
<summary>Incorrect</summary>

```swift
↓func f1() {
  if true {
    if true {
      if false {}
    }
  }
  if false {}
  let i = 0
  switch i {
  case 1: break
  case 2: break
  case 3: break
  case 4: break
 default: break
  }
  for _ in 1...5 {
    guard true else {
      return
    }
  }
}
```

</details>
