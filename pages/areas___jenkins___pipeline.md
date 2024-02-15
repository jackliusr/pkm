- Concepts
	- node: a machine which is part of the Jenkins environment and is capable of executing a Pipeline.
	- stage: A `stage` block defines a conceptually distinct subset of tasks performed through the entire Pipeline (e.g. "Build", "Test" and "Deploy" stages), which is used by many plugins to visualize or present Jenkins Pipeline status/progress.
	- step: A single task. Fundamentally, a step tells Jenkins *what* to do at a particular point in time (or "step" in the process).
- Handling credentials:  limitations of  Credentials Masking
  ```groovy
  credentials
  withCredentials
  ```
- `$class` is used to pick the kind of object to create. It may be a fully-qualified class name (`hudson.tasks.ArtifactArchiver`), but the simple name may be used when unambiguous.
- Durable Task: Library offering an extension point for processes which can run outside of Jenkins yet be monitored.