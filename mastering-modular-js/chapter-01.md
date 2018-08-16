# [Chapter 01: Module Thinking](https://github.com/mjavascript/mastering-modular-javascript/blob/master/chapters/ch01.asciidoc)


Abstractions, that keep complexity hidden away from us.

## 1.1 Introduction to module thinking

- The interface needs to be well-designed so that its users don’t become frustrated.
- **Maybe if the interface didn’t exist in the first place, we’d be better off in terms of maintainability and readability.**
- Systems can be organized granularly.
- The fewer touchpoints an interface has, the smaller its surface area is, and the simpler the interface becomes.
- An interface with a large surface area is highly flexible, but it might also be a lot harder to understand and use, given the high amount of functionality exposed by the interface.
- Reap the benefits of the functionality we expose, without concerning themselves with the details of how we implemented that functionality.
- Robust, documented interfaces are one of the best ways of isolating a complicated piece of code so that others can consume its functionality without knowing any implementation details.
- **A systematic arrangement of robust interfaces can be accrued to form a layer**.
- Uniform layers, comprised of components similar in pattern or shape, offer a sense of familiarity.

## 1.2 A Brief History of Modularity

- Relying on consistent API shapes is a great way of increasing productivity, given the difficulty of coming up with adequate interface designs.
- Global window object: a variable in one script might inadvertently replace a global that another script was relying on.
- (IIFE) were invented and became an instant mainstay.
- The code in each IIFE is isolated and can only escape onto the global context via explicit statements such as window.fromIIFE = true.
- The problem in the IIFE approach was that there wasn’t an explicit dependency tree.
- Regardless of whether our application contained a hundred or thousands of modules, RequireJS would resolve the dependency tree without the need for a carefully maintained list. Given we’ve listed dependencies exactly where they were needed, we’ve eliminated the necessity for a long list of every component and how they’re related to one another.
- RequireJS wasn’t without problems. The entire pattern revolved around its ability to asynchronously load modules, which was ill-advised for production deployments due to how poorly it performed.
- On that note, there were quite a few different RequireJS functions and several ways of invoking those functions, complicating its use.
- AngularJS suffered from many of the same problems.
- This mechanism was incompatible with minifiers which would rename parameters to single characters and thus break the injector..
- Taking advantage of the fact that Node.js programs had access to the file system, the CommonJS standard is more in line with traditional module loading mechanisms.
- In CommonJS, each file is a module with its own scope and context.
- CommonJS had a one-to-one mapping between files and modules.
- Eventually, Browserify was invented as a way of bridging the gap between CommonJS modules for Node.js servers and the browser.
- This enabled better tooling and code introspection — making it easier for tools to learn the hierarchy of a CommonJS component system.
- The ES6 specification included a module syntax native to JavaScript.
- One major advantage in ESM over CJS is how ESM has — and encourages — a way of statically importing dependencies.
- Static imports in ESM are constrained to the topmost level of a module, further simplifying parsing and introspection.
- Another advantage of ESM over CommonJS require() is that ESM specifies a way of doing asynchronous module loading, which implies that parts of an application’s dependency graph could be loaded in response to specific events, concurrently, or lazily as needed.

## 1.3 The Perks of Modular Design

- Webpack is a successor to Browserify that largely took over in the role of universal module bundler thanks to a broader set of features.
- Modularity spread across files limits the amount of complexity we have to pay attention to when working on any one particular feature.
- Maintainability, or the ability to effect change in the codebase, also improves significantly because of this.
- Maintainability is valuable regardless of team size: even in a team of one.
- Modular code is meant to be highly maintainable by default.
- When each piece of code in a program is modular, the codebase appears to be simple when we’re looking at individual components, yet on the whole it is able to exhibit complex behaviors.
- **The implementation of those components is not their essence, but their interfaces are**.
- When interfaces are well-designed, they can be grown in non-breaking ways, augmenting the amount of use cases they can satisfy, without compromising existing usage.
- **Strong interfaces are effective at hiding away weak implementations**.
- Strong interfaces are also excellent for unit testing.
- Components in modular applications are defined by their interfaces.
- If the interface is well-tested and robust, we can surely consider its implementation in a secondary plane.
- We can concern ourselves with the trade-off between flexibility and simplicity.
- **Flexibility inevitably comes at the cost of added complexity**.
- And thus we need to strike the right balance by deciding how much rigidity we can get away with in our interfaces.

## 1.4 Modular Granularity

- We can apply modular design concepts on every level of a given system.
- The same can be said of applications: when they become large or complex enough, we might want to split them into differentiated products.
- When we want to make an application more maintainable, we should consider creating explicitly defined layers of code, so that we can grow each layer horizontally while preventing the complexity of those additions from spreading to other, unrelated, layers.
- The internal functions of a module won’t have as rigid of an interface either: as long as the public interface holds, we can change the implementation.
- **The key to proper modular design is in having an utmost respect for all interfaces, and that includes the interfaces exposed by internal functions.**
- Virtually everyone who has done any amount of programming has experienced a feeling of frustration when glancing at a piece of code they themselves wrote a few months prior, only to later realize that, with a fresh pair of eyes the design they had then come up with wasn’t as solid as they originally intended.
- Remember, computer program development is largely a human and collaborative endeavor.
- Our focus is to empower an organization so that its developers can remain productive and able to quickly understand and even modify pieces of code they haven’t ran across before.
- Performance should be treating it as a feature.
- **We, as developers, often over-do architecture as well**.
- It’s a lot better when we focus on problems we’re already running into, or might soon run into, instead of trying to plan for a hockey-stick growth of infrastructure and throughput without any data to back up the hockey-stick growth we’re anticipating.
- **When we don’t plan in such a long-term form, an interesting thing occurs: our systems grow more naturally**.
- If we settle on abstractions too early, and they end up being the wrong abstractions, we pay dearly for that mistake.
- **Bad abstractions force us to bend entire applications to their will, and once we’ve realized that the abstraction is bad and ought to be removed, we might be so heavily invested in it that pulling out might be costly.**
- **This, paired with the sunk cost fallacy, whereby we’re tempted to keep the abstraction just because we’ve spent a lot of time, sweat, and blood on it, can be very hazardous indeed.**

## 1.5 Modular JavaScript: A Necessity

- We’re only now barely beginning to scratch the surface of native modules.
- This shortcoming of the web is evidenced by how patterns that were adopted universally elsewhere, like layered or component-based architectures, weren’t even contemplated on the web for most of its lifetime thus far.
