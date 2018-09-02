
# Modular Patterns and Practices

## 5.1 Leveraging Modern JavaScript

- When used judiciously, the latest JavaScript features can be of great help in reducing the amount of code whose sole purpose is to work around language limitations.

### 5.1.1 Template Literals

- You can prefix the template with a custom function that transforms the template’s output, enabling use cases like input sanitization, formatting, or anything else.
- It’s important to differentiate between purely stylistic choices, which tend to devolve in contentious time-sinking discussions, and choices where there’s more ground to be covered in the everlasting battle against complexity.
- but the exact style is unimportant as long as we enforce it consistently.

## 5.1.2 Destructuring, Rest, and Spread

- Destructuring helps us indicate the fields of an object that we’ll be using to compute the output of a function.
- Another benefit worth pointing out is that Object.assign() can cause accidents.

### 5.1.3 Striving for simple const bindings.

### 5.1.4 Navigating Callbacks, Promises, and Asynchronous Functions

- Callbacks are typically a solid choice, but we often need to get libraries involved when we want to execute our work concurrently.
- Promises might be hard to understand at first, but they offer a few utilities like Promise#all for concurrent work, yet they might be hard to debug under some circumstances.
- Consistency should remain as the primary driving force of how we decide which pattern to use.
- Our focus should be on how these flows are connected together, regardless of whether they’re comprised of callbacks, promises, or something else.

## 5.2 Composition and Inheritance

- Inheritance, where we scale vertically by stacking pieces of code on top of each other.
- Composition, where we scale our application horizontally by adding related or unrelated pieces of code at the same level of abstraction while keeping complexity to a minimum.

### 5.2.1 Inheritance through Classes

- Even though ES6 classes look a lot like classes in other languages, they’re syntactic sugar using prototypes under the hood.
- Inheritance is also useful when there’s an abstract interface to implement and methods to override, particularly when the objects being represented can be mapped to the real world.

### 5.2.2 The Perks of Composition: Aspects and Extensions

- When we write code based on inheritance chains, complexity is spread across the different classes.
- composition relies on stringing together orthogonal aspects of functionality.
- orthogonality means that the bits of functionality we compose together complements each other, but doesn’t alter one another’s behavior.
- One way to compose functionality is additive.
- Another way of doing composition, that doesn’t rely on extension functions, is to rely on functional aspects instead, without mutating your target object.
- Using a plain Map would prevent garbage collection from cleaning things up when target is only being referenced by Map entries, whereas WeakMap allows garbage collection to take place on the objects that make up its keys.

### 5.2.3 Choosing between Composition and Inheritance

- The functional approach is a bit more cumbersome to implement than simply mutating objects or adding base classes, but it offers the most flexibility.
- Picking the right pattern for each situation and striving for consistency might seem at odds with each other, but this is again a balancing act.
- The trade-off is between consistency in the grand scale of our codebase versus simplicity in the local piece of code we’re working on.

## 5.3 Code Patterns

### 5.3.1 Revealing Module

- The premise is simple enough: expose precisely what consumers should be able to access, and avoid exposing anything else.
- When we expose only a thin interface, our implementation can change largely without having an impact on how consumers use the module.

### 5.3.2 Object Factories

- In most other situations, however, sharing persistent state across public interface methods is a recipe for unexpected bugs.
- The methods on this object are equivalent to the exported interface of a plain JavaScript module, but state mutations are contained to instances that consumers create.
- we should always strive to contain mutable state as close to its consumers as possible.

### 5.3.3 Event Emission

### 5.3.4 Message Passing and the Simplicity of JSON

- JSON — now a subset of the JavaScript grammar — was purpose-built for this use case, where we often have to serialize data, send it over the wire, and deserialize it on the other end.
