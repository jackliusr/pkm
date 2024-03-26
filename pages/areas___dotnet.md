- EntityFramework
- decompiling
	- ILSpy for everyone   [free  OSS  C# IL  multi-platforms]
	- dotPeek for convenient decompilation   [free  C# IL]
	- dnSpy for gurus, security and hackers   [free  OSS  C# VB IL]
	- JustDecompile for everyone  [free  OSS  C# VB IL]  (continued as **CodemerxDecompile**)
	- IldAsm for nostalgia  [free IL]
	- .NET Reflector for history   [paid unsupported  C# VB IL MC++]
	- **NDepend** to go beyond decompilation
- Centralize .NET Project Settings using Directory.Build.Props and Directory.Package.Props
- .NEXT (dotNext): the family of powerful libraries aimed to improve development productivity and extend the .NET API with unique features. The project is supported by the [.NET Foundation](https://dotnetfoundation.org/).
- aspnet.core
	- Integration tests in ASP.NET Core
	- e2e test
		- playwright
		- FlueFlame
	- `UserManager`: a concrete class that manages the user. This Class Creates, Updates, and Deletes the Users. It has methods to find a user by User ID, User Name, and email. `UserManager` also provides the functionality for adding Claims, removing Claims, add and removing roles, etc. It also generates password hash, Validates Users etc.
	- `SignInManager`: a concrete class which handles the user sign in from the application. The `SignInManager` is responsible for Authenticating a user, i .e  signing in and signing out a user. It issues the authentication cookie to the user.
	- identity model
	  {{renderer code_diagram,plantuml}}
		- ```plantuml
		  @startuml
		  class User
		  class Role
		  class UserClaim
		  class UserToken
		  class UserLogin
		  class RoleClaim
		  'class UserRole
		  
		  User --* UserClaim: > has
		  User --* UserLogin: > has
		  User -- UserToken: > has
		  Role -- RoleClaim: associate
		  User *--* Role: : associate
		  @enduml
		  ```
		- Middleware order
		  <img src="https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/index/_static/middleware-pipeline.svg?view=aspnetcore-8.0"></img>
		- MVC
		  <img src="https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/index/_static/mvc-endpoint.svg?view=aspnetcore-8.0"></img>
		- IActionResultExecutor
		- IStartupFilter