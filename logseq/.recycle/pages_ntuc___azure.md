- sftp:   azure firewall --> sftp server
- IRConnect: 10.25.12.49
-
- {{renderer code_diagram,plantuml}}
	- ```plantuml
	  @startuml
	  !theme materia-outline
	  hide footbox
	  'autonumber
	  ' The only difference between actor
	  'and participant is the drawing
	  
	  participant UTAP
	  participant "SFTP Server" as sftp
	  participant SAP
	  
	  note left of UTAP
	      webjobs
	  end note
	  alt Inbound
	      UTAP->sftp: put files to SFTP server
	      SAP -> sftp: pull data
	  else outbound
	      SAP -> sftp: put data
	      UTAP -> sftp: pull files and processing
	  end
	  
	  @enduml
	  ```
- | Password: Labour@18989 |