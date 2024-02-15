- case study: conference system
  collapsed:: true
	- used by an external customer to create their attendee accounts, review the conference sessions available, and book their attendee.
	- context diagram: 
	  {{renderer code_diagram,plantuml}}
		- ```plantuml
		  @startuml
		  !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml
		  
		  Person(customer, "Customer", "A conference delegate or potential delegate")
		  System(ecommerce, "Conference System", "Allows customers to view conference sessions and make bookings")
		  Rel_R(customer, ecommerce, "Interacts via browser to book conference sessions")
		  
		  @enduml
		  ```
	- {{renderer code_diagram,plantuml}}
		- ```plantuml
		  @startuml
		  !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
		  
		  !define DEVICONS https://raw.githubusercontent.com/tupadr3/plantuml-icon-font-sprites/master/devicons
		  !include DEVICONS/msql_server.puml
		  
		  Person(customer, "Customer", "A conference delegate or potential delegate")
		  
		  System_Boundary(c0, "Conference System") {
		  
		      Container(web_app, "Web Application", "Software", $descr="The conference website user interface")
		      Container(app, "Conference Application", "Software", $descr="Responds to UI, manage attendee and sessions")
		      ContainerDb(db, "Database", "Microsoft SQL", "Single store for conference information", $sprite="msql_server")
		  
		  }
		  Rel_R(customer, c0, "interacts with")
		  Rel_R(web_app, app, "make api calls using HTTP(S)")
		  Rel_R(app, db, "store and retrieve from database")
		  @enduml
		  ```
	- component diagram:
	  {{renderer code_diagram,plantuml}}
		- ```plantuml
		  @startuml
		  !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
		  !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Component.puml
		  !define DEVICONS https://raw.githubusercontent.com/tupadr3/plantuml-icon-font-sprites/master/devicons
		  !include DEVICONS/msql_server.puml
		  
		  Container(web_app, "Web Application", "Software", $descr="The conference website user interface")
		  Component(api, "API Controller", "Component: Package/Module", $descr="Retrieves REST connections and routes to appropriate subsystems")
		  Component(attendee, "Attendee", "Component: Package/Module", $descr="Manages creation and retrieval of attendee from the system")
		  Component(booking, "Bookings", "Component: Package/Module", $descr="Allow customers to view conference sessions and manage bookings")
		  Component(session, "Session", "Component: Package/Module", $descr="Allow customers to view conference sessions and manage bookings")
		  ComponentDb(db, "Database", "Microsoft SQL", "Single store for conference information", $sprite="msql_server")
		  
		  Lay_D(attendee, booking)
		  Lay_D(booking, session)
		  
		  Rel_R(web_app, api, "make api calls using HTTP(S)")
		  Rel_R(api, attendee, "Routes reqeusts internally")
		  Rel_R(api, booking, "Routes reqeusts internally")
		  Rel_R(api, session, "Routes reqeusts internally")
		  
		  Rel_R(attendee, db, "CRUD operations on attendee (SQL, Out of process)")
		  Rel_R(booking, db, "Links attendees and sessions (SQL, Out of process)")
		  Rel_R(session, db, "CRUD operations on attendee (SQL, Out of process)")
		  
		  @enduml
		  ```
	- evolutionary steps:
		- {{renderer code_diagram,plantuml}}
			- ```plantuml
			  @startuml
			  !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml
			  
			  Person(customer, "Customer", "A conference delegate or potential delegate")
			  System(ecommerce, "Legacy Conference System", "Allows customers to view conference sessions and make bookings")
			  System(attendee, "Attendee", "API-based service for manage attendees")
			  Rel_R(customer, ecommerce, "Interacts via browser to book conference sessions")
			  Rel_R(ecommerce, attendee, "API calls to manage attendees")
			  
			  @enduml
			  ```
		- api architecture and traffic patterns
			- north-south traffic: api gateway
			- east-west traffic: infrastructure components such as k8s, service mesh, app&discovery
- ADR