PromiseK
============================

_PromiseK_ provides the `Promise` class designed as a _Monad_ for Swift.

```swift
// `flatMap` is `then` equivalent
//   asyncFoo, asyncBar, asyncBaz: Int -> Promise<Int>
//   # gets Int asynchronously
let a: Promise<Int> = asyncFoo(2).flatMap { asyncBar($0 + 1) }.flatMap { asyncBaz($0 * 2) }
let b: Promise<Int> = asyncFoo(3).map { $0 * $0 }
let sum: Promise<Int> = a.flatMap { a0 in b.flatMap{ b0 in Promise(a0 + b0) } }

// uses `Optional` for error handling
//   asyncQux: Int -> Promise<Int?>
//   # returns Promise(nil) when it fails.
let mightFail: Promise<Int?> = asyncQux(5).flatMap { Promise($0.map { $0 * $0 }) }
let howToCatch: Promise<Int> = asyncQux(7).flatMap { Promise($0 ?? 0) }
```

How to Install
----------------------------

Put [PromiseK.swift](Project/PromiseK/PromiseK.swift) into your project.

License
----------------------------

[The MIT License](LICENSE)

References
----------------------------

1. [Promise - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
2. [JavaScript Promises: There and back again - HTML5 Rocks](http://www.html5rocks.com/en/tutorials/es6/promises/)
3. [A Fistful of Monads - Learn You a Haskell for Great Good!](http://learnyouahaskell.com/a-fistful-of-monads)
