- API endpoint:  access control #card
  card-last-interval:: 369.41
  card-repeats:: 6
  card-ease-factor:: 3.1
  card-next-schedule:: 2024-10-27T11:47:04.108Z
  card-last-reviewed:: 2023-10-24T02:47:04.108Z
  card-last-score:: 5
- RESTful URL design for search https://stackoverflow.com/questions/207477/restful-url-design-for-search #card
  card-last-interval:: 276.98
  card-repeats:: 6
  card-ease-factor:: 2.86
  card-next-schedule:: 2024-06-28T06:08:13.691Z
  card-last-reviewed:: 2023-09-25T07:08:13.692Z
  card-last-score:: 5
- [API Central](https://medium.com/api-center)
- **OData differs from REST and gains its focus on business logic in its feature set**. Whereas REST is an architectural style solely concerned with data transfer via web service APIs, OData builds upon that architecture with a set of metadata that can be easily integrated into most programming and scripting languages.
- Archetypes
	- **Document**: Each URI below identifies a document resource: Use “singular” name to denote document resource archetype
	  
	  ```HTTP
	  api.cricket.restapi.org/leagues/ipl
	  ```
	- **Collection**: Each URI below identifies a collection resource:, Use plural name to denote store resource archetype
	- **Store**: A store never generates new URIs. Instead, each stored resource has a URI that was chosen by a client when it was initially put into the store. Use plural name to denote store resource archetype
	- **Controller**: A controller resource models a procedural concept. Controller resources are like executable functions, with parameters and return values; inputs and outputs. **Controller names typically appear as the last segment in a URI path, with no child**
	  
	  ```HTTP
	  POST /alerts/245743/resend
	  ```
- Collection vs Store archetype
	- The main difference between a store and a collection is who is responsible for generating the URIs of the resources. In a store, the client is responsible for generating the URIs. In a collection, the server is responsible for generating the URIs.
	- Another difference is that a store is a client-managed resource repository, while a collection is a server-managed resource directory. This means that a client has more control over the resources in a store than in a collection.
- REST:
	- verbs beyond CRUD/HTTP Verbs
		- as subresources
		- :verbs
			- https://github.com/microsoft/api-guidelines/blob/vNext/azure/Guidelines.md#performing-an-action
			- https://cloud.google.com/apis/design/custom_methods#http_mapping
- [Common API Patterns](https://github.com/microsoft/api-guidelines/blob/vNext/azure/Guidelines.md#common-api-patterns)
- versioning
	- no version
	- URI versioning: kubernetes
	- Query string versioning:
	- Header versioning
	- Media type versioning
- [rest-assured](https://rest-assured.io/)