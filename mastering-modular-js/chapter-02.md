# Chapter 02: Modularity Principles

- Modularity can be the answer to complexity.
- Something is complex when it becomes hard to grasp or fully understand.
- A significant body of changes to an implementation should be able to leave the API in front of said implementation unmodified. 

## 2.1 Modular Design Essentials

- Modularity tackles the complexity problem in program design by opting for small modules with a clear-cut and well-tested API that’s also documented.

### 2.1.1 Single Responsibility Principle

- As long as the methods and properties we export from a component are related, we wouldn’t be breaking SRP.
- it’s important to figure out what the responsibility is.
- interface becomes more rigid as it’s adopted by more modules.
- When we keep the API consistent across implementations, using the same signature across every module, it’s easy to swap out implementations depending on context such as the execution environment (development vs. staging vs. production) or any other dynamic context that we need to rely upon.

### 2.1.2 API First

- More importantly, a great interface means we can swap out a poor implementation as soon as we find time to introduce a better one.
- The amount of API calls that potentially have to adapt increases with time, entrenching the API as the project grows.
- An interface often doesn’t have the necessity of supporting multiple implementations, but we must nonetheless think in terms of the public API first.
- **The answer to API design lies in figuring out which properties and methods consumers will need, while keeping the interface as small as possible.**
- When we need to implement a new component, a good rule of thumb is drawing up the API calls we’d need to make against that new component.
- Following an API-first methodology is crucial in understanding how the API might be used.

### 2.1.3 Revealing Pattern

- **When everything in a component is made public, nothing can be considered an implementation detail and thus making changes becomes hard.**

### 2.1.4 Finding the right abstractions

- **It is best to wait until a distinguishable pattern emerges and it becomes clear that introducing an abstraction would help keep complexity down.**
- **On the other hand, state generates complexity by dynamically modifying the flow in our programs. Without state, programs would run in the same way from start to finish.**

### 2.1.5 State Management

- We shall think of state as our program’s internal entropy.
- **One of the goals in modular design is to keep state to the minimum possible.**
- Modularity takes aim at this issue by chopping a state tree into manageable bits and pieces, where each branch of the tree deals with a particular subset of the state. This approach enables us to contain the growing application state as our codebase grows in size
- A function is deemed pure when its output depends solely on its input.
- An artifact of this module exporting an impure function is that the outcome of invoking increment hinges upon understanding how increment is used elsewhere in the application, as each call to increment changes its expected output.
- One potential solution would be to expose a factory which is itself pure.
- When we eliminate impurity in public interfaces, we’re effectively circumscribing entropy to the calling code.

## 2.2 CRUST: Consistent, Resilient, Unambiguous, Simple and Tiny

- A well-regarded API typically packs several of the following traits. It is consistent, meaning it is idempotent[6] and has a similar signature shape as that of related functions.
- It is resilient, meaning its interface is flexible and accepts input expressed in a few different ways.
- Yet, it is unambiguous, there aren’t multiple interpretations of how the API should be used.
- Through all of this, it manages to stay simple.
- **CRUST mostly regards the outer layer of a system (be it a package, a file, or a function), but its principles will seep into the innards of its components and result in simpler code overall.**

### 2.2.1 Consistency

- Deliberately establishing consistent patterns makes our code easier to read.
- The result is we rarely need to reach for documentation in order to understand how these functions are shaped.
- **When we have different shapes for functions that perform similar tasks, we need to make an effort to remember each individual function’s shape instead of being able to focus on the task at hand.**
- **Uniformity is desirable for any given layer in an application, because an uniform layer can be largely treated a single, atomic portion of the codebase.**

### 2.2.2 Resiliency

- Resiliency is about identifying the kinds of inputs that we should accept, and enforcing an interface where those are the only inputs we accept.
- **When designing an interface that might otherwise end up with four or more parameters, an options object carries a multitude of benefits.**
  - The consumer can declare options in any order.
  - The API can offer default values for each option.
  - The consumer doesn’t need to concern herself with options they don’t need.
  - Developers reading pieces of code which consume the API can immediately understand what parameters are being used, since they’re explicitly named in the options object.
- As we make progress, we keep naturally coming back to the options object in API design.

### 2.2.3 Unambiguity

- **The output shape for a function shouldn’t depend on how it received its input or the result that was produced.**
- you should aim to surprise consumers of your API as little as possible.
- **We should avoid optional input parameters which transform the result into a different data type.**
- **It isn’t necessary to treat failure and success with the same response shape, meaning that failure results can always be null or undefined, while success results might be an array list. However, consistency should be required across all failure cases and across all sucess cases, respectively.**

### 2.2.4 Simplicity

- Good defaults are conservative, and good options are additive.
- Negated options however tend to confuse users who are confronted with the double negative.
- Well designed interfaces have a habit of making it appear effortless for consumers to use the API for its simplest use case.

### 2.2.5 Tiny surface areas

- **A small surface area means fewer test cases that could fail, fewer bugs that may arise, fewer ways in which consumers might abuse the interface, less documentation, and more ease of use since there’s less to choose from.**
- **We can avoid creating interfaces that contain several slightly different solutions for similar problems by holistically designing the interface to solve the underlying common denominator, maximizing the reusability of a component’s internals in the process.**
