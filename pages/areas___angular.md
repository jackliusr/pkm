- overview
  ![](https://angular.io/generated/images/guide/architecture/overview2.png)
- zone: an execution context that persists across async tasks. You can think of it as [thread-local storage](https://en.wikipedia.org/wiki/Thread-local_storage) for the JavaScript VM.
- Signals: a system that granularly tracks how and where your state is used throughout an application, allowing the framework to optimize rendering updates.
- Content projection: a pattern in which you insert, or *project*, the content you want to use inside another component
- Microtask & macrotasks
- Observable values (async scenario) in RxJS **are processed after promises.**
- Component Dev Kit (CDK): a set of behavior primitives for building UI components.
- *control flow blocks*:
- Hydration: the process that restores the server side rendered application on the client. This includes things like reusing the server rendered DOM structures, persisting the application state, transferring application data that was retrieved already by the server, and other processes.
- injector hierarchies: 
  <table>
  <thead>
  <tr>
  <th align="left">Injector hierarchies</th>
  <th align="left">Details</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td align="left"><code><a href="api/core/EnvironmentInjector" class="code-anchor">EnvironmentInjector</a></code> hierarchy</td>
  <td align="left">Configure an <code>ElementInjector</code> in this hierarchy using <code>@<a href="api/core/Injectable" class="code-anchor">Injectable</a>()</code> or <code>providers</code> array in <code><a href="api/core/ApplicationConfig" class="code-anchor">ApplicationConfig</a></code>.</td>
  </tr>
  <tr>
  <td align="left"><code>ElementInjector</code> hierarchy</td>
  <td align="left">Created implicitly at each DOM element. An <code>ElementInjector</code> is empty by default unless you configure it in the <code>providers</code> property on <code>@<a href="api/core/Directive" class="code-anchor">Directive</a>()</code> or <code>@<a href="api/core/Component" class="code-anchor">Component</a>()</code>.</td>
  </tr>
  </tbody>
  </table>
- schematic: a template-based code generator that supports complex logic. It is a set of instructions for transforming a software project by generating or modifying code. Schematics are packaged into collections and installed with npm.
- Deferrable views: be used in component template to defer the loading of select dependencies within that template. Those dependencies include components, directives, and pipes, and any associated CSS. To use this feature, you can declaratively wrap a section of your template in a [@defer](https://angular.io/api/core/defer) block which specifies the loading conditions.
  
  ``` razor
  @defer {
    <large-component />
  }
  ```
	- Triggers: Triggers provide conditions for when defer loading occurs.
- Angular’s Change Detection: Angular’s change detection mechanism is designed to run **after the microtask queue is emptied.**
- A Typical Sequence
  
  ``` mermaid
  sequenceDiagram
     participant User
     participant UI
     participant API
     participant MicroTaskQueue
     participant MacroTaskQueue
     participant Angular
     
     User ->> UI: click
     UI ->> API: API call
     API -->> UI: response
     UI ->> MicroTaskQueue: push Promises & Observables
     UI  ->> MacroTaskQueue: push setTimeout
     MicroTaskQueue ->> UI: Resolve Promises 
     MicroTaskQueue  ->> UI: Observables emit values
     UI ->> UI: Process Data with RxJS operations
     UI ->> Angular: inform Angular of data changes
     Angular ->> UI: Check for changes
     UI ->> User: Update UI with fresh data
     MacroTaskQueue ->> UI: Execute setTimeout
  ```