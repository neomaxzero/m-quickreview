# [Shaping Internals](https://github.com/mjavascript/mastering-modular-javascript/blob/master/chapters/ch03.asciidoc)

## 4.1 Internal Complexity

- We could perhaps set a rule whereby team members should watch out for garden paths in the codebase and fix them as they are making changes in the same functional area as the affected code.

### 4.1.1 Containing Nested Complexity

- An insidious variant of callback hell is the one where we have logic in every nesting level.
- When we have synchronous logic intermixed with asynchronous callbacks, things get more challenging.
- Our program would be in a better place if we kept the flow separate from the business logic.
- As we move logic into their own functions and flatten the callback chain, we’ll be left with the bare flow of operations being separate from the operations themselves.

### 4.1.2 Feature Entanglement and Tight Coupling

- Design features upfront.
- Being alert when reading old code can also be key in identifying what was previously a well-contained module that evolved to cover a broad range of concerns.
- Keeping each stage of the process in functions that live at the same level instead of being deeply nested.

### 4.1.3 Frameworks: the Good the Bad and the Ugly

- A large number of conventions might hinder productivity, especially if some of our conventions appeared to work as if by magic.
- When it comes to conventions, frameworks are a special case.
- Upon adopting a framework, we’re buying into its conventions and practices.
- These conventions and abstractions are tremendously helpful to keep complexity in check while building an application.
- Having clearly defined layers is paramount to the design of effective and maintainable applications once we’re past the prototyping stages.

## 4.2 Refactoring Complex Code

### 4.2.1 Embracing Variables over Clever Code

- Complex code is predominantly shorter than it should be.
- The problem with clever code is that we need to expend time and energy to read it whenever it’s intent is not clear on our mind.
- One of the underlying issues that can be identified when reading complex code is that it uses few variables.
- We don’t have the need to treat memory as a sacred.
- Code that describes what it does in the process of doing it doesn’t require as many comments.
- In this vein, it is of utmost importance to think long and deep about the name of every function, every variable, and every package, directory, or data structure we conceive.

### 4.2.2 Guard Clauses and Branch Flipping

- A better alternative is to flip the conditionals, placing all failure handling statements near the top.
- It reduces nesting and eliminates else branches while promoting failure handling to the top of our code.
- This early exit approach is often referred to as guard clauses.

### 4.2.3 An Interdependency Piramid

- By keeping only the high-level flow near the top, and the specifics towards the end, complex functionality can be designed in such a way that the reader experiences a zoomed out overview of the functionality at first.
- We should present functions in a codebase in the order that they’ll be read by the consumer.
- And not in the execution order.

### 4.2.4 Extracting Functions

- Pyramidal structures where we deal with higher level concerns near the top and switch to more specific problems as we go deeper into the inner workings of a system works wonders in keeping complexity on a tight leash.
- Pushing anything that gets in the way of the current flow to the bottom of a function is an effective way of streamlining readability.
- Bits of code that select some slice of application state are best shoved away from the relevant logic that will use this selected state to perform some action.
- When we want to name an aspect of a routine without adding a comment, we could create a function to host that functionality. Doing so doesn’t just give a name to what the algorithm is doing, but it also allows us to push that code out of the way, leaving behind only the high-level description of what’s going to happen.

### 4.2.5 Flattening Nested Callbacks

- Codebases with asynchronous code flows often fall into the so-called "callback hell".
- This kind of coupling can be reverted by naming the callbacks and placing them all in the same nesting level.
- By eliminating nesting we’ve made the scope for each function more explicit.

### 4.2.6 Factoring Similar Tasks

- Abstractions can be particularly damaging when created too early.
- A similar situation occurs when we have a concurrent flow that remains more or less constant across a number of different functions, in which case we might want to consider keeping the flow in its own function, and passing a callback for the actual processing logic that is different in each case.
- It’s not always clear when we’ll need to reuse some functionality somewhere else, and keeping every aspect of functionality isolated just in case we need to reuse them can be costly in terms of time and development effort.
- More often than not, however, abstractions can end up complicating matters. It might be that the tradeoff isn’t worth it because the code becomes much harder to read.

### 4.2.7 Slicing Large Functions

- The overall structure of your typical function should begin with guard clauses, making sure the input we receive is what we expect.
- The way of reducing complexity in a function is not by collapsing hundreds of lines of code into tens of complicated lines of code. Instead, we can move each of these long pieces of code into individual functions that only deal with one aspect of the data.

## 4.3 State as Entropy

- Each bit of state we introduce to an application creates a new dimension to take into account when trying to understand the flow of a program.

### 4.3.1 Current State: It’s Complicated

- Breaking a single large function into a dozen small functions might make the overall application more complex.
- At its heart, state is mutable.

### 4.3.2 Eliminating Incidental State

- Our focus in reducing state-based entropy must then lie in the individual aspects of the system.
- Incidental state can occur when we have a piece of data that’s used in several parts of an application, and which is derived from other pieces of data.
- When we persist derived state, we’re putting the original and the derived data at risk of falling out of sync.
- Furthermore, just like with caches and other intermediate representations of data, performance optimization can lead to bugs and code that’s ultimately harder to maintain, which is why neither should be embarked upon lightly, unless there’s a business case where performance is hurting the bottom line.

### 4.3.3 Containing State

- All that matters are the inputs we receive and the outputs we produce.
- One other case where we may incidentally increase complexity is whenever we modify the property values of an input. This type of operation should be made extremely explicit, as to not be confused, and avoided where possible.
- Type of operation should be made extremely explicit, as to not be confused, and avoided where possible.

### 4.3.4 Leveraging Immutability

- Relying on immutability would be an alternative that doesn’t involve pure loops nor does resort to breakage-prone side-effects.

## 4.4 Data Structures are King

- This in turn guarantees that the function is idempotent, where calling a function repeatedly with the same input always produces the same result.
- When the right data structures are identified, we’ll notice there’s a lot less transformation, mapping, and looping involved into getting inputs to become the outputs we need to produce.

### 4.4.1 Isolating Data and Logic

- The data structure we pick constrains and determines the shape our API can take.
- Now, we can’t possibly foresee all scenarios when coming up with the data structure we’ll use at first, but what we can do is create intermediate representations of the same underlying data using new structures that do fit the new requirements.
- When we take the road of adapting data structures to the changing needs of our programs, we’ll find that writing programs in such a data-driven way is better than relying on logic alone to drive their behaviors.

### 4.4.2 Restricting and Clustering Logic

- Keeping data strictly separate from methods that modify or access said data structures can help reduce complexity.
- The idempotence aspect is of great benefit.
- A simple interface is usually highly restrictive (e.g accepting only a boolean value.
- We should aim to keep logic restrictive and only as flexible as deemed necessary by business requirements.
- But by starting out with a small use case we’re able to grow the interface into something that’s naturally better fit to handle specific, real-world use cases.
- Data, on the other hand, should be transformed to fit elegant interfaces, rather than trying to fit the same data structure into every function.
- We should strive to keep code that deals with a particular data structure contained in as few modules as possible.
