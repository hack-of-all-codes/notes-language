#Structures

* always passed on as copies
* String, Array, and Dictionaries are Structs 
* have member-wise initializers
```swift
struct Resolution {
  var width = 0
  var height = 0
}

//only strucst have these freebies
var myReso = Resolution(width: 100, height: 200)
```