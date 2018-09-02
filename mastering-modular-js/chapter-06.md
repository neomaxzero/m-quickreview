

# Development Methodology and Philosophy

- Pretending all of our code is going to be open-source results in better configuration and secret management

## 6.1 Secure Configuration Management

- these are typically instead obtained through environment variables or encrypted configuration files that aren’t committed to version control systems.
- it’s best to approach secrets with careful consideration by default, and avoid headaches later in the lifetime of a project.
- Any sensitive information or configurable values may qualify as a secret.
- Using what’s commonly referred to as "dot env" files is an effective way of securely managing secrets in Node.js applications, and there’s a module called nconf that can aid us in setting these up.
- We can use the nconf npm package to handle reading and merging all of these sources of application settings with ease.

## 6.2 Explicit Dependency Management

- Including dependency trees in our repositories is not practical.
- Every dependency in our application should be explicitly declared in our manifest, relying on globally installed packages or global variables as little as possible — and ideally not at all.

## 6.3 Interfaces as Black Boxes

- When writing tests we always assume that third-party modules are generally well-tested enough that it’s not our responsibility to include them in our test cases. The same thinking should apply to first party modules that just happen to be dependencies of the module we’re currently writing tests for.
- The concept of disposability goes beyond just event handlers, though. Any sort of resource that we allocate and attach to an object, component, or service is created, should be released and cleaned up when that attachment ceases to exist.
- Another improvement which could aid in complexity management is to structure applications so that all business logic is contained in a single directory structure.
- Large client-side applications often suffer from not having a single place where logic should be deposited, and as a result the logic is instead spread amongst components, view controllers, and the API, instead of being mostly handled in the server-side, and then in a single physical location in the client-side code structure.
- Regardless of our approach, the most important aspect remains that we stick to clearly isolating the view rendering aspects in our applications from its business logic aspects, as much as possible.

## 6.4 Build, Release, Run

- Whenever we incorporate environment-specific feature flags or logic, we need to pay attention to the discrepancies introduced by these changes.

## 6.6 Parity in Development and Production

## 6.7 Abstraction Matters

- Eager abstraction can result in catastrophe.
- Conversely, failure to identify and abstract away sources of major complexity can be incredibly costly as well.
- Mastering modular JavaScript isn’t strictly about following a well-defined set of rules, but rather about being able to put yourself on the shoes of your consumers, foreplanning for feature development that may be coming down the pipe.
- and treating documentation with the same respect and care that you should be putting into interface design.
