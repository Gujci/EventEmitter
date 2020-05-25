# EventEmitter
A lightweight tool to easily implement listener pattern.

[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Build Status](https://travis-ci.org/Gujci/EventEmitter.svg?branch=master)](https://travis-ci.org/Gujci/EventEmitter)
![Swift](https://github.com/Gujci/EventEmitter/workflows/Swift/badge.svg)

Example
========

Subscribe to events w parameters:
```swift
eventEmitterInstance.on("eventWithParameter") { (weak parameter: Any?) in
    //...
}
```
Or w/o parameters:
```swift
eventEmitterInstance.on("eventWithoutParameter") {
    //...
}
```

Defining events with an enum is also supported:
```swift
public enum AppEvent: String, Event {
    case some
    case other
}
```

```swift
eventEmitterInstance.on(AppEvent.some) {
    //...
}
```

Emit an event with an EventEmitter class
```swift
class EventEmitterClass: EventEmitter {
  var listeners: Dictionary<String, Array<Any>>? = [:]
  
  //...
  public func foo(parameter: Any?) {
    //...
    emit(AppEvent.some, information: parameter)
  }
  
  public func bar() {
    //...
    emit(AppEvent.some)
  }
}
```
Note: This is a protocoll so you can use it with `struct`s as well. 

`String` comforms to `Event` protocol, so this is also a valid code:

```swift
emit("some", information: parameter)
```

# Documentation

### Functions to be called from an EventEmitter instance

```swift
emit(_ event: Event)
```

```swift
emit<T>(_ event: Event, information: T)
```

```swift
emit(onMain event: Event)
```

```swift
emit<T>(onMain event: Event, information: T)
```


### Functions to call on an EventEmitter instance
#### subscribe

```swift
on(_ event: Event, action: (() -> ()))
```

```swift
on(_ events: [Event], action: (() -> ()))
```

```swift
once(_ event: Event, action: (() -> ()))
```

```swift
on<T>(_ event: Event, action: ((T?) -> ()))
```

```swift
on<T>(_ events: [Event], action: ((T?) -> ()))
```

```swift
once<T>(_ event: Event, action: ((T?) -> ()))
```

#### unsubscribe

```swift
removeListeners(_ event: Event?)
```

# Installation

## SPM 

Use the GitHub link in Xcode

## Carthage 

Put this line into your cartfile

```
github "Gujci/EventEmitter"
```

### Swift 3

for Swift 3 use the `0.5.5` tag. This version will not be supported.

```
github "Gujci/EventEmitter" "== 0.5.5"
```

# Debugging

To turn on logging add `EventLoggingEnabled` to 'Arguments passed on launch' at Schema/Run/Arguments

# TODO
 - [x] Travis support
 - [ ] Full code coverage
 - [ ] Support custom threads
 - [x] Once
 - [ ] More documentation

