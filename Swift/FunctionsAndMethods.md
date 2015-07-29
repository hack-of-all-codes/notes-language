# Functions
Functions are self-contained chunks of code that perform a specific task
```swift

//CODE:complete function:
func countAPersonsResidence(person:Person, residence: Residence?) -> Int {
    return person.residence!.numberOfRooms;
}

//CODE: default parameter value
func join(s1: String, s2: String, joiner: String = " ") -> String {
    return s1 + joiner + s2
}

//param "joiner" is optional
var joined = join("Hello", "World") //Hello World

//providing a "joiner" param requires the use of the explicit external name
joined = join("Hello", "World", joiner:"-") //Hello-World

//TODO: Curried functions

//CODE: In-Out parameters
//function type: (inout Int, inout Int) -> ()
func swapTwoInts(inout i1: Int, inout i2: Int) {
    var temp = i1
    i1 = i2
    i2 = temp
}

var i1 = 100
var i2 = 200

swapTwoInts(&i1, &i2) //i1=200, i2=100

//TODO: Multiple return values
```

## External Parameter Names
Sometimes it’s useful to name each parameter when you call a function, to indicate the purpose of each argument you pass to the function
```swift
var a = 1
var b = 2

func sum(withAddend a1: Int, a2: Int) -> Int {
    return a1 + a2
}

//note: if you provide an external parameter name for a parameter, that external name must always be used when you call the function
println("sum:\(sum(withAddend: a,b))")

//shorthand: external and local parameter name are the same
func sum(#a1: Int, #a2: Int) -> Int {
    return a1 + a2
}
println("sum:\(sum(a1: a,a2: b))")
```

## Variadic Parameters
A variadic parameter accepts zero or more values of a specified type. You use a variadic parameter to specify that the parameter can be passed a varying number of input values when the function is called. Write variadic parameters by inserting three period characters (...) after the parameter’s type name
```swift
//note: the variadic parameter must be the last in the parameter list
func sumAll(a1: Int, a2: Double...) -> Double {
    var sum = 0.0
    sum += Double(a1)
    
    for d in a2 {
        sum += d
    }
    
    return sum
}

println("sum:\(sumAll(1, 2.0, 3.0, 5.0))") //11.0
```

## Constant and Variable Parameters
Function parameters are constants by default. Trying to change the value of a function parameter from within the body of that function results in a compile-time error. This means that you can’t change the value of a parameter by mistake
```swift
func varParam(var p1: Int, p2: Int) {
    p1 = 3
    p2 = 3333 //ERROR: by default, parameters are local constants
    println("p1: \(p1) p2: \(p2)")
}
```

## Function Types
You can use a function type such as (Int, Int) -> Int as a parameter type for another function. This enables you to leave some aspects of a function’s implementation for the function’s caller to provide when the function is called.

You can use a function type as the return type of another function. You do this by writing a complete function type immediately after the return arrow (->) of the returning function.
```swift
func simpleFunction() {
    println("simpleFunction")
}

//function with no parameter and no return
var sf: () -> () = simpleFunction

func singleParam(p1: Int) -> Int {
    println("singleParam:\(p1)")
    return 1
}

//function with one param and one return
var sp: (Int) -> Int = singleParam

//function with function as parameter and return type
func funcParamExe(withFunction f: (Int)-> Int) -> () -> (){
    f(100)
    return sf
}

funcParamExe(withFunction: sp)
```

Reference: [Functions, Apple Inc.](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-ID158)

# Methods
Methods are functions that are associated with a particular type

Reference: [Methods, Apple Inc.](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Methods.html#//apple_ref/doc/uid/TP40014097-CH15-ID234)

```swift
//TODO: demonstrate SELF
```

# Subscripts
Subscripts enable you to query instances of a type by writing one or more values in square brackets after the instance name

```swift
subscript(index: Int) -> Int {
    get {
        // return an appropriate subscript value here
    }
    set(newValue) {
        // perform a suitable setting action here
    }
}
```
Reference: [Subscripts, Apple Inc.](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Subscripts.html#//apple_ref/doc/uid/TP40014097-CH16-ID305)