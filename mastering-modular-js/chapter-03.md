# [Chapter 03: Module Design](https://github.com/mjavascript/mastering-modular-javascript/blob/master/chapters/ch03.asciidoc)

- Properly designed module internals help keep our code readable and its intent clear.

## 3.1 Growing a Module

- Purpose-built functions scale well because they introduce little organizational complexity into the module they belong to

### 3.1.1 Composability and Scalability

- Functions are the fundamental unit of our code
- Pairing a few rules of thumb with our own intuition is an effective way of keeping functions simple, limiting their scope.
- If we had designed them with scalability in mind, we might’ve grouped many similar use cases under the same feature, and would’ve avoided an unnecessarily large API surface in the process.
- we should be able to find a common denominator that’s suitable for most use cases.
- These choices also depend on how heavily the API is going to be used, how flexible we want it to be, and how frequently we intend to make changes to it.
- Abstractions aren’t free, but they can shield portions of code from complexity.
- When we’re weighing whether to offer an interface like CSS selectors or callbacks, we’re deciding how much we want to abstract, and how much we want to leave up to the consumer.
- API design is a constant tradeoff between simplicity and flexibility

### 3.1.2 Design for Today

- A simple implementation means we pay smaller upfront costs, but it doesn’t necessarily mean that new requirements will result in breaking changes.
- Similarly, the interface could start off supporting only one way of receiving its inputs, and as use cases evolve we might bake polymorphism into the mix, accepting multiple input types in the same parameter position.
- if we wish for our interface to remain small but we predict the consumer will eventually need to hook into different pieces of our component’s internal behavior so that they can react accordingly, we’re better off waiting until this requirement materializes than building a solution for a problem we don’t yet have.
- Falling in the trap of implementing features consumers don’t yet need might be easy at first, but it’ll cost us dearly in terms of complexity, maintainability, and wasted developer hours.
- strive to keep functionality to exactly the absolute minimum that’s required.

### 3.1.3 Abstractions Evolve in Small Steps

- Abstractions should evolve naturally.
- Then we’re unsure about whether to bundle a few use cases with an abstraction, the best option is often to wait and see whether more use cases would fall into the abstraction we’re considering.
- We should first wait until use cases emerge and then reconsider an abstraction when its benefits become clear.
- Context is of the utmost relevance here.
- In any case, when we’re uncertain if our interface will be needing to expose certain surface areas, it’s highly recommended that we don’t expose any of it until we are indeed certain.
- Our interface would only offer a single solution for that particular use case.

### 3.1.4 Move Deliberately and Experiment

- Moving fast means to quickly hash out prototypes to test our newfound assumptions.
- The code that makes up a product should be covered by tests.
- A product that’s not test covered will be, ironically, unable to move fast when bugs inevitable arise and wind down engineering speed.
- We should constantly try out and validate new ideas, verifying whether they pose better solutions than the status quo.
- Interface design shouldn’t be hurried.
- This is not to advocate sloppily developed internals, but rather to encourage respectfully and deliberately thought out interface design.

## 3.2 CRUST Considerations

### 3.2.1 Do Repeat Yourself, Occasionally

- When taken to the extreme, though, DRY is harmful and hinders development.
- Our mission to find the right abstractions will be cut short if we are ever vigilant in our quest to suppress any and all repetition.
- Being too quick to follow DRY may result in picking the wrong abstraction.
- When the more concise piece of code results in a program that’s harder to read than what we had, DRY was probably a bad idea.
- Most often, DRY is the correct approach, but there are indeed cases when DRY might not be appropriate, such as when it yields trivial gains at the expense of readability or when it hinders our ability to find better abstractions.

### 3.2.2 Feature Isolation

- Even when the smaller component isn’t being reused anywhere else, and perhaps not even tested on its own, it’s still worth moving it to a different file.
- Why? Because we’re removing the complexity that makes up the child component from its parent virtually for free. We’re only paying a cheap indirection cost, where the child component is now referenced as a dependency of its parent instead of being inlined.
- The complexity didn’t dissipate, it’s subtly hidden away in the interrelationships between these child components and their parent, but that’s now the biggest concern in the parent module, whereas each of the smaller modules doesn’t need to know much about. these relationships.
- Chopping up internals doesn’t merely only work for view components and their children.
- Each layer has its own complexities and intricacies waiting to be discovered, but the complexity is spread across the layers rather than clustered on any one particular layer.
- The spread reduces the amount of complexity we have to observe and deal with on any given layer.
- It is at this stage of the design process that you might want to consider defining different layers for your application.
- Were we to truly embrace a modular architecture, we might go an extra mile after promoting each utility to its own module.
- This approach can be taken as far as we consider necessary: as long as we’d benefit from making a piece of functionality reusable across our projects, we can make it reusable, adding tests and documentation along the way.
- Hypermodularity offers diminishing returns.
- Use your own judgement to decide how far to take modular structures.
- When a piece of code is not very complex and rather small, it’s usually not worth creating a module for.
- When a piece of code involves enough complexity to warrant its own module, that doesn’t immediately make it worthwhile to create a package for it.
- External modules often involve a little bit more of maintenance work.
- Extricating the module will be challenging if it has dependencies on other parts of the codebase it belongs to, since those would have to be extricated as well.

### 3.2.3 Trade-offs when Designing Internals

- We need to design the right interface.
- The number one aspect to our goal is to find the best possible interface that caters to the needs and wants of its consumers.
- Backed up by an implementation that can deliver on the promises we make through the interface.
- Third, the implementation should be as simple as possible.
- The internals should be as performant as possible.
- We should favor simplicity and readability over speed.
- Trying to anticipate needs is more often than not going to result in more complexity, code, and time spent, with hardly anything to show for in terms of improving the consumer’s experience.

## 3.3 Pruning a Module

### 3.3.1 Error Handling, Mitigation, Detection, and Solving

- While working on software development we’ll invariably need to spend time analyzing the root cause that led to subtle bugs which seem impossible to hunt down.
- We can’t prevent this from happening over and over — not entirely. Unexpected bugs will always find their way to the surface.
- What we can do is mitigate the risk of bugs by writing more predictable code or improving test coverage. We can also become more proficient at debugging.
- We must be sure to handle every expected error.
- If we’re dealing with conventional callbacks that have an error argument, let’s handle the error in a guard clause.
- Whenever we have a promise chain, make sure to add a .catch reaction to the end of the chain that handles any errors ocurring in the chain.
- While leveraging streams or other conventional event-based interfaces, make sure to bind an error event handler.
- Test coverage can help detect unexpected errors.
- Tests can do little to prognosticate and prevent software bugs from happening, however.
- Public interface documentation underscores readable code.
- Getting into the habit of treating every bit of code and the structure around it (formal documentation, tests, comments) as documentation itself is only logical.
- Doing this in a README file instead of a module leaves us an itsy bit more detached from an eventual implementation, but the essence is the same.

### 3.3.2 Documentation as an Art

- Code we never write is code we don’t need to worry about deleting

### 3.3.3 Removing Code

### 3.3.4 Applying Context

- When you bend a rule to fit your situation, you’re not necessarily disagreeing with the advice, you might just have applied a different context to the same problem

