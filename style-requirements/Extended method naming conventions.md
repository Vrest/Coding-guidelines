# Extended method naming conventions.
### Introduction to this document
This document serves as a reference to some of the extended naming conventions that should be taken into account when writing code for the DCPF. It should be read as a short list of best-practices and recommendations. special cases may exist where these rules would not apply. In general though those situations should be avoided if at all possible.

These conventions are meant to give a developer an instant feel for how a method behaves just by seeing the name, improving overall code quality and reducing the need for explicit documentation.
## Prerequisites
All normal coding guidelines must be taken into account. that includes that all method names shall be underscore free (with the exception of event handlers, which can should have exactly one underscore). These conventions and the accompanying style guide can be found on github at https://github.com/Vrest/Coding-guidelines.
Naming methods in DCPF code.
Methods prefixed with “try” 
  - are never static
  - guarantees that no exception will be thrown
  - the return type is a boolean indicating success (true) or failure (false)

## Methods prefixed with “tryGet”
  - follow all conventions for “try” prefixed methods
  - have a byRef argument at the last position that will hold the object to get on success.

## Methods prefixed with “get”
  - Should do as little work as possible
  - Work done may include lazy loading, simple math based on other properties of the same instance.
  - lazily loaded properties should be cached on the instance

## Methods prefixed with “is”
  - Follow all conventions for “get” prefixed methods
  - Always return a non-null boolean

## Methods prefixed with “set”
  - Should do as little work as possible
  - Work done may observable notifications, setting flags on the same instance

## Methods prefixed with “process” 
  - Should return either void or some constant value defined on the class that contains the method or one of its superclasses.

## Methods prefixed with “on”
  - Should contain event handling code. These methods are considered private API and follow the following set of extra rules whenever possible.
  - Event handlers look like this: on <Control> _ EventName(Object $sender, EventArg $arg) Where <Control> is the PascalCased property name of the control. An example for a control named `txtFirstName` could be `onTxtFirstName_ValueChanged` 
  - Event handlers should have two arguments, one `Object $sender` and one `EventArg $argument`. There is a “hidden” third argument with the name of the event for handlers registered to be fired for multiple events.
