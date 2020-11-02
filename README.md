# Refactoring-summary
Summary of the book "Refactoring" 2nd edition

## General tips
- There are two hats - adding new features and refactoring. You can always wear only one. When you are adding a new feature, it doesn't matter if it has duplicate code or is suboptimal, just make sure the new feature works. After you are finished, put on another hat and refactor the code. 
- A good set of automated tests is crucial for refactoring. Refactoring should never break a working code. After each small change, run the tests, commit and push the change.
- Refactoring is not supposed to be done because of clean code or good engineering practice. The point is to make us faster - faster to add features, faster to fix bugs.
- When you feel the need to comment something, write a function instead. The function contains the code we wanted to comment but it is named after the intention of the code rather than the way it works. This can be done even on a single line of code.
- Any function that returns a value should not have any observable side effects. If a function return a value, that's all it should do.

## When to refactor
- Mysterious name
  - Change function declaration
  - Rename variable
  - Rename field
  
- Duplicated code
  - Extract function
  - Slide Statement
  - Pull up method
- Long function
  - Extract function
  - Too many temporary variables?
    - Replace temp with query
    - Introduce parameter object
    - Preserve whole object
    - Replace function with command
- Long parameter list
  - Replace parameter with method
  - Preserve whole object (pass the original data structure)
  - If several parameters always fit together, combine them to Introduce parameter object
  - Remove flag argument
  - Combine functions into class
- Global data
  - Encapsulate variable
- Mutable data
  - Encapsulate variable 
  - If variable is being updated to store different things, use Split Variable
  - Remove setter methods. Make field immutable
- Divergent change - Occurs when one module is often changed in different ways for different reasons, e.g. if you look at a module and say "I will have to change these three functions every time I get a new database"
  - When there is a separate context, we should move it into a separate module
  - Split method that's doing too many things into separate modules
- Shotgun surgery - Opposite of Divergent change, happens when you have to make a lot of little edits to a lot of different classes
  - Move function of Move field and put alle the changes into a single module
  - Combine functions into class
  - Inline function or Inline class to pull together poorly separated logic
- Feature envy - Occurs when a function in one module spends more time communicating with functions or data inside another module than it does within its own module.
  - Move function or Extract function
- Data clumps - Bunches of data (fields in a couple of classes, parameters in methods) that hang out together should find a home together
  - Extract class to turn the clumps into an object
  - Introduce parameter object or Preserve whole object
- Primitive obsession - Programmers stick too much to primitive data types and are reluctant to create their own fundamental data types which are useful for their domain (money, coordinates, ranges, …)
  - Replace primitive with object
  - Introduce subclasses
  - Groups of primitives that commonly appear together are data clumps
- Repeated switches
  - When the same conditional switching logic pops up in different places
  - Replace conditional with polymorphism (subclasses)
- Loops
  - Replace loops with pipeline
- Lazy element - Unnecessary structure - class that is a simple function, function that's named the same as its body code reads
  - Inline function, Inline class
  - Collapse hierarchy - merge parent and child class
- Speculative generality - Too general code to handle all possible future cases, can be spotted when the only users of a function or class are test cases
  - Inline function, Inline class, Collapse hierarchy
  - Remove dead code
- Temporary field - Class with a field that is set up only under certain circumstances
  - Extract the field into a separate class and move all code that concerns the field in to that class
- Message chains - Asking an object for another object and that for another object etc.
  - Create a helper function that hides delegation
  - Example: 
    - Before:
         Const manager = employee.department.manager;
    - After:
         Class Employee -> getManager() { return this.department.manager; }
         Const manager = employee.getManager();
    
    
## Refactoring tools
For tools described in the section above, that are not self-explanatory, I am providing a short description

- Slide statement - Move variable declaration close to the usage, this prepares them for Extract function
- Pull up method - pull method from child class to parent class
- Replace temp with query
- Replace function with command
- Remove flag argument
- Encapsulate variable - limit scope as much as possible
- Split Variable
