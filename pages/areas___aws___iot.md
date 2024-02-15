- services
	- AWS IoT Core
		- architecture
		  ![](https://docs.aws.amazon.com/images/iot/latest/developerguide/images/architecture-diagram.png){:height 478, :width 717}
		-
		- AWS IoT secure tunneling: establish bidirectional communication to remote devices over a secure connection that is managed by AWS IoT
			- local proxy: modes: `source` or `destination`
		- Device provisioning: AWS provides several different ways to provision a device and install unique client certificates on it.
		- binary payloads
			- use * to refer to the message payload as raw binary data
			  ``` sql
			  SELECT * FROM 'topic/subtopic'
			  ```
	- AWS IoT Events: enables you to monitor your equipment or device fleets for failures or changes in operation, and to trigger actions when such events occur. AWS IoT Events continuously watches IoT sensor data from devices, processes, applications, and other AWS services to identify significant events so you can take action.
		- **detector model**: (a model of your equipment or process) using *states*.
	- AWS IoT Greengrass: an open-source edge runtime and cloud service that helps you build, deploy, and manage intelligent device software.
	  ![](https://docs.aws.amazon.com/images/greengrass/v2/developerguide/images/how-it-works.png){:height 676, :width 942}
		- greengrass discovery: The Discovery API **enables devices to retrieve information required to connect to a Greengrass core that is in the same Greengrass group as the client device**.
		- client devices: local IoT devices
	- AWS IoT SiteWise
		- asset, asset hierarchy,
		- Asset models: define [attributes](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/concept-overview.html#concept-attribute), time series inputs ([measurements](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/concept-overview.html#concept-measurement)), time series transformations ([transforms](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/concept-overview.html#concept-transform)), time series aggregations ([metrics](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/concept-overview.html#concept-metric)), and [asset hierarchies](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/concept-overview.html#concept-hierarchy).
		- Attributes are asset properties that represent information that generally doesn't change, Asset properties are the structures within each asset that contain industrial data
	- IoT Device Simulator: Create and simulate hundreds of virtual connected devices without having to configure and manage physical devices
	  ![](https://raw.githubusercontent.com/aws-solutions/iot-device-simulator/main/architecture.png){:height 387, :width 977}
- [IoT PLM](https://aws.amazon.com/blogs/iot/navigating-iot-product-lifecycle-management-with-aws-iot/#:~:text=AWS%20IoT%20Greengrass%3A%20Extending%20capabilities,when%20internet%20connectivity%20is%20unavailable.)
- [Architecture Best Practices for IoT](https://aws.amazon.com/architecture/iot/?cards-all.sort-by=item.additionalFields.sortDate&cards-all.sort-order=desc&awsf.content-type=*all&awsf.methodology=*all)
- AWS IoMT Services Reference Architecture
  ![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*-jZuRqER70hjIJb-NAM4Lg.png){:height 420, :width 843}