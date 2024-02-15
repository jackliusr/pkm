- https://falco.org/: a cloud-native security tool designed for Linux systems. It employs custom rules on kernel events, which are enriched with container and Kubernetes metadata, to provide real-time alerts. Falco helps you gain visibility into abnormal behavior, potential security threats, and compliance violations, contributing to comprehensive runtime security.
- What does Falco do? uses syscalls to monitor a system's activity, by:
	- Parsing the Linux syscalls from the kernel at runtime
	- Asserting the stream against a powerful rules engine
	- Alerting when a rule is violated
- Falco *rules file*: rules, macros, lists
	- [Rules](https://falco.org/docs/rules/basic-elements/#rules): *Conditions* under which an alert should be generated. A rule is accompanied by a descriptive *output string* that is sent with the alert.
		- Priority: Every Falco rule has a priority which indicates how serious a violation of the rule is.
		- Extending Rules: appending and overwrite
		- Rule Exceptions: Exceptions are a concise way to represent conditions under which a rule should not generate an alert
	- [Macros](https://falco.org/docs/rules/basic-elements/#macros): Rule condition snippets that can be re-used inside rules and even other macros. Macros provide a way to name common patterns and factor out redundancies in rules.
	- [Lists](https://falco.org/docs/rules/basic-elements/#lists): Collections of items that can be included in rules, macros, or other lists. Unlike rules and macros, lists cannot be parsed as filtering expressions.
	- Visibility [](https://falco.org/docs/rules/basic-elements/#visibility)
		- A list can only reference lists defined before it.
		- A macro can only reference macros defined before it.
		- A macro can reference any list.
		- A rule can reference any macro.
- The configuration file: The default configuration file, [`/etc/falco/falco.yaml`](https://github.com/falcosecurity/falco/blob/master/falco.yaml) makes Falco load rules from the `/etc/falco/falco_rules.yaml` file followed by any custom rules located in the `/etc/falco/rules.d` directory. This configuration is governed by the `rules_file` key:
  
  ``` yaml
  rules_file:
    - /etc/falco/falco_rules.yaml
    - /etc/falco/falco_rules.local.yaml
    - /etc/falco/rules.d
  ```
- plugin:
	- Event Sourcing Capability
	- Field Extraction Capability
	- Event Parsing Capability
	- Async Events Capability
	- Composability of Capabilities