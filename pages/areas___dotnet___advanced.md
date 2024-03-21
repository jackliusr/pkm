- appdomain
- assemlby
	- domain-neutral
- context
- Ngen.exe (Native Image Generator)
- Crossgen2
- Loader  Optimization  Attribute: 
  
  ```c#
  [System.AttributeUsage(System.AttributeTargets.Method)]
  public sealed class LoaderOptimizationAttribute : Attribute
  ```
	- The [LoaderOptimizationAttribute](https://learn.microsoft.com/en-us/dotnet/api/system.loaderoptimizationattribute?view=net-8.0) can only be set on the main method for an executable application and is ignored on all other methods.
	- | DisallowBindings | 4 | Ignored by the common language runtime. |
	  | DomainMask | 3 | Do not use. This mask selects the domain-related values, screening out the unused [DisallowBindings](https://learn.microsoft.com/en-us/dotnet/api/system.loaderoptimization?view=net-8.0#system-loaderoptimization-disallowbindings) flag. |
	  | MultiDomain | 2 | Indicates that the application will probably have many domains that use the same code, and the loader must share maximal internal resources across application domains. |
	  | MultiDomainHost | 3 | Indicates that the application will probably host unique code in multiple domains, and the loader must share resources across application domains only for globally available (strong-named) assemblies that have been added to the global assembly cache. |
	  | NotSpecified | 0 | Indicates that no optimizations for sharing internal resources are specified. If the default domain or hosting interface specified an optimization, then the loader uses that; otherwise, the loader uses [SingleDomain](https://learn.microsoft.com/en-us/dotnet/api/system.loaderoptimization?view=net-8.0#system-loaderoptimization-singledomain). |
	  | SingleDomain | 1 | Indicates that the application will probably have a single domain, and loader must not share internal resources across application domains. |
- ContextBoundObject
- CrossDomainContextAttribute