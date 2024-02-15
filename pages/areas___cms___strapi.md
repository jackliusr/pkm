- content-types
	- **Collection** types are content-types that can manage several entries.
	- **Single** types are content-types that can only manage one entry.
- **Components** are a data structure that can be used in multiple collection types and single types. Use the [Content-type Builder](https://docs.strapi.io/user-docs/content-type-builder) or create them manually.
- Dynamic zones: create a flexible space in which to compose content, based on a mixed list of [components](https://docs.strapi.io/dev-docs/backend-customization/models#components-2).
- Lifecycle hooks
- strapi
	- **back-end**, http server based on [koa](https://koajs.com/)
	- frontend: admin panel
- Plugin
- Plugins extension: Plugin extensions code is located in the `./src/extensions` folder, can be installed from the [Marketplace](https://docs.strapi.io/user-docs/plugins/installing-plugins-via-marketplace#installing-marketplace-plugins-and-providers) or as npm packages
- Providers: add an extension to the core capabilities of the plugin
- Policies: functions that execute specific logic on each request before it reaches the [controller](https://docs.strapi.io/dev-docs/backend-customization/controllers). They are mostly used for securing business logic. global or scoped
	- [Plugins polcies](https://docs.strapi.io/dev-docs/plugins) can add and expose policies to an application.
	- API policies: API policies are associated to the routes defined in the API where they have been declared.
- Content source maps: identifiers that track where a piece of content comes from. They generally indicate what CMS the data is from (the origin) and what to do when it’s opened (through href or event handlers)
- [Project structure](https://docs.strapi.io/dev-docs/project-structure)
	- v3: https://docs-v3.strapi.io/developer-docs/latest/setup-deployment-guides/file-structure.html
- ![](https://docs.strapi.io/img/assets/backend-customization/diagram-routes.png){:height 361, :width 778}
- ``` mermaid
  graph TB
      request[Request] ---> globalMiddlewareA(("Global middleware<br/>before await next()"))
      globalMiddlewareA --"Call next()"--> routePolicy{Route policy}
      globalMiddlewareA --"Returns before next()<br>Goes back up in the middleware chain"-->globalMiddlewareB
      routePolicy --Returns true--> routeMiddlewareA(("Route middleware<br/>before await next()"))
      routePolicy --Returns false or an error-->globalMiddlewareB
      routeMiddlewareA --"Returns before next()<br>Goes back up in the middleware chain"-->routeMiddlewareB
      routeMiddlewareA --"Call next()"--> controllerA{{Controller}}
      controllerA --"Call Service(s)"--> serviceA{{Service}}
      controllerA --"Don't call Service(s)" --> routeMiddlewareB
      serviceA --"Call Entity Service" --> entityService{{Entity Service}}
      serviceA --"Don't call Entity Service" --> controllerB
      entityService --"Call Query Engine"--> queryEngine{{Query Engine}}
      entityService --"Don't call Query Engine" --> serviceB
      queryEngine --> lifecyclesBefore[/Lifecycle<br> beforeX\] 
      lifecyclesBefore[/Lifecycle<br> beforeX\] --> database[(Database)]
      database --> lifecyclesAfter[\Lifecycle<br> afterX/]
      lifecyclesAfter --> serviceB{{"Service<br/>after Entity Service call"}}
      serviceB --> controllerB{{"Controller<br/>after service call"}}
      controllerB --> routeMiddlewareB(("Route middleware<br/>after await next()"))
      routeMiddlewareB --> globalMiddlewareB(("Global middleware<br/>after await next()"))
      globalMiddlewareB --> response[Response]
      linkStyle 3 stroke:green,color:green
      linkStyle 4 stroke:red,color:red
      linkStyle 2 stroke:purple,color:purple
      linkStyle 5 stroke:purple,color:purple
      click request "/dev-docs/backend-customization/requests-responses"
      click globalMiddlewareA "/dev-docs/backend-customization/middlewares"
      click globalMiddlewareB "/dev-docs/backend-customization/middlewares"
      click routePolicy "/dev-docs/backend-customization/routes"
      click routeMiddlewareA "/dev-docs/backend-customization/routes"
      click routeMiddlewareB "/dev-docs/backend-customization/routes"
      click controllerA "/dev-docs/backend-customization/controllers"
      click controllerB "/dev-docs/backend-customization/controllers"
      click serviceA "/dev-docs/backend-customization/services"
      click serviceB "/dev-docs/backend-customization/services"
      click entityService "/dev-docs/api/entity-service/"
      click lifecyclesBefore "/dev-docs/backend-customization/models#lifecycle-hooks"
      click queryEngine "/dev-docs/api/query-engine/"
      click lifecyclesAfter "/dev-docs/backend-customization/models#lifecycle-hooks"
      click response "/dev-docs/backend-customization/requests-responses"
      click queryEngine "/dev-docs/api/query-engine"
  ```
- Data Management System: import, export, transfer