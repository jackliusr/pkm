- tech stacks: https://builtwith.com/detailed/kinobi.asia
- Kubernetes + ingress, cross+zone?
- **load test to find issues, resource limits and requests**
- protocol from app gw --> kinobi: http/1.1
- ``` bash
  echo "GET https://ntuc-executive-mentorship-programme.app.kinobi.asia/_nuxt/3.f24b7e8da8fe18a715ce.js" | vegeta attack -duration=5s | tee results.bin | vegeta report
  cat results.bin | vegeta report  -type=hdrplot
  ```
- ![image.png](../assets/image_1697723512468_0.png){:height 532, :width 762}
	- ```plantuml
	  @startuml
	  !include <awslib/AWSCommon>
	  !include <awslib/InternetOfThings/IoTRule>
	  !include <awslib/Analytics/KinesisDataStreams>
	  !include <awslib/ApplicationIntegration/SimpleQueueService>
	  !include <awslib/NetworkingContentDelivery/all.puml>
	  !include <cloudogu/common>
	  !include <cloudogu/dogus/nginx>
	  !define ICONURL https://raw.githubusercontent.com/tupadr3/plantuml-icon-font-sprites/v2.4.0
	  !includeurl ICONURL/common.puml
	  !includeurl ICONURL/devicons/nodejs.puml
	  !includeurl ICONURL/devicons/mysql.puml
	  
	  !define AzurePuml https://raw.githubusercontent.com/plantuml-stdlib/Azure-PlantUML/release/2-2/dist
	  !include AzurePuml/AzureCommon.puml
	  !include AzurePuml/Networking/AzureApplicationGateway.puml
	  
	  left to right direction
	  
	  'agent "Published Event" as event #fff
	  AzureApplicationGateway(appgw,"AppGW","")
	  Route53(dns, "DNS", "ntuc-executive-mentorship-programme")
	  
	  
	  frame region {
	      frame az1 {
	          frame subnet_public1 {
	              ElasticLoadBalancing(lb1, "lb1","lb1")
	              DOGU_NGINX(nginx1,"Nginx")
	              lb1 -down-> nginx1
	              DEV_NODEJS(nodejs1)
	              nginx1 -down-> nodejs1
	          }
	      
	      }
	  
	      frame az2 {
	          frame subnet_public2 {
	              ElasticLoadBalancing(lb2, "lb2","lb2")
	              DOGU_NGINX(nginx2,"Nginx") 
	              lb2 -down-> nginx2
	              DEV_NODEJS(nodejs2)
	              nginx2 -down-> nodejs2
	          }
	      }
	  
	      frame az3 {
	          frame subnet_public3 {
	              ElasticLoadBalancing(lb3, "lb3","lb3")
	              DOGU_NGINX(nginx3,"Nginx") 
	              lb3 -down-> nginx3
	              DEV_NODEJS(nodejs3)
	              nginx3 -down-> nodejs3 
	          } 
	      }
	  
	      frame subnet_private {
	          DEV_MYSQL(db)
	      }
	      nodejs1 -down->db
	      nodejs2 -down->db
	      nodejs3 -down->db
	  }
	  
	  dns -down->lb1
	  dns -down->lb2
	  dns -down->lb3
	  appgw -down->dns: dns resolve
	  appgw -down->lb1: or lb2, or lb3, only 1
	  @enduml
	  ```