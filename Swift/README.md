#Ordnance Survey Swift Code Style Guidelines

---

The aim of this document is to promote idiomatic usage of the Swift language, to assist readability by providing a consistent style, and to make potential defects and problems easier to spot.

## Code Formatting

* Use clang-format. Spaces, not tabs; 4 spaces per indent; etc.

* Types in upper camel case. e.g. `MapView`

* Variables and constants in lower camel case, e.g. `routeRecordingController`

* Use swift modules to namespace the code, as opposed to Objective-C style class prefixes.

* enums should be uppercase, e.g.

```
enum Direction {
    case North, South, East, West
}
```
* Avoid unnecessary abbreviation - `viewController` is easier to read than `vc`

## Best Practices

* Use type inference wherever possible, to reduce redundant type declarations, e.g.

`let viewController = UIViewController()` rather than:

`let viewController: UIViewController = UIViewController()`

* Let the compiler infer `self` whenever possible. Exceptions are setting in `init()` and non-escaping closures, e.g.:

```
struct GridPoint {
    let easting: Double
    let northing: Double
    
    init(easting: Double, northing: Double) {
        self.easting = easting
        self.northing = northing
    }
}
```
* Capure list type inference - use whenever possible to avoid overly verbose code. (TODO: add examples)

* Use `let` over `var` whenever possible. Consider if your things really needs to be mutable.

* Favour value types wherever it makes sense. (TODO: clarify when it does/doesn't make sense)

* `as!` should be considered an error.

* Use `guard` and `if let` judiciously. (TODO: add examples)

* Constants should be avoided at global level, and instead declared static within the relevant type they correspond to. This allows them to be referenced without an instance of the type, e.g.

```
struct NationalGrid {
    static let nationalGridWidth = 700000
    static let nationaGridHeight = 1300000
}
```

* Computer Properties - Use the short version (i.e. omit the `get {...}` block) if you only need a getter:

```
class RandomGenerator {
    var randomNumber: UInt32 {
        return arc4random()
    }
}
```

* Converting instances - use `init()` methods, as per the convention set forth in the Swift standard library, e.g. (TODO: come up with a more relevant example)

```
extension NSColor {
    convenience init(_ mood: Mood) {
        super.init(color: NSColor.blueColor)
    }
}
```
* Singletons - If you think you need to use a singleton, think long and hard. Usually, the problem can be solved in a more elegant way. That said, if you really need one, a singleton in Swift is simple to implement and thread safe by default (unlike Objective-C):

```
class DownloadService {
    static let sharedInstance = DownloadService()
}
```

## Access Control

* TODO

## Block capture semantics

* TODO: `unowned` vs `weak`

## Optionals

* TODO

## Error Handling

* Use `guard` to fail or return fast in a method over the more verbose `if let`, e.g:

```
guard let viewController = requiredViewController? else {
    println("Warning: cannot do this without a view controller.")
    return
}
doSomething(viewController)
```
over:

```
if let viewController = requiredViewController? {
    doSomething(viewController)
} else {
    println("Warning: cannot do this without a view controller.")
    return
}

```


* Use `do/try/catch` for anything that may throw an error.

* Avoid `try!`. Instead, wrap in `do {...} catch {...}` to provide context.

* NSError

* return values

## Paradigm choice

* TODO: cover functional, object-oriented, procedural, metaprogramming and suitable usage scenarios for each.

## Protocol-Oriented design

* TODO

## Extenstions and protocol extensions

* Methods and properties that are 

## Testing

* `@testable`
* `Nimble` framework
* How to do mocks (i.e. inner classes with overrides)
* unit tests
* UI tests
* coverage

## Comments and Documentation
* Use `VVDocumenter` plugin.
* Document all public interface.
* Code should be as self-documenting as possible. Use descriptive names for types, properties, methods. Follow Cocoa conventions as closely as possible when dealing with e.g. `UIKit`, and Swift standard library conventions when dealing with pure Swift code.
* Document anything that is non-obvious, hack-like, strange or a workaround.
