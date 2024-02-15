- Overview of TLS termination and end to end TLS with Application Gateway
	- certificate requirements
		- [The certificate on the listener requires the entire certificate chain to be uploaded (the root certificate from the CA, the intermediates and the leaf certificate) to establish the chain of trust.](https://learn.microsoft.com/en-us/azure/application-gateway/ssl-overview#end-to-end-ssl-with-the-v2-sku:~:text=The%20certificate%20on%20the%20listener%20requires%20the%20entire%20certificate%20chain%20to%20be%20uploaded%20(the%20root%20certificate%20from%20the%20CA%2C%20the%20intermediates%20and%20the%20leaf%20certificate)%20to%20establish%20the%20chain%20of%20trust.)
		- [Application gateway doesn't provide any capability to create a new certificate or send a certificate request to a certification authority.](https://learn.microsoft.com/en-us/azure/application-gateway/ssl-overview#end-to-end-ssl-with-the-v2-sku:~:text=Application%20gateway%20doesn%27t%20provide%20any%20capability%20to%20create%20a%20new%20certificate%20or%20send%20a%20certificate%20request%20to%20a%20certification%20authority.)
		- That the certificate's "Common Name" (CN) matches the host header in the request
		- [End to end TLS and allow listing of certificates](https://learn.microsoft.com/en-us/azure/application-gateway/ssl-overview#end-to-end-tls-and-allow-listing-of-certificates)
		- [End-to-end TLS with the v2 SKU](https://learn.microsoft.com/en-us/azure/application-gateway/ssl-overview#end-to-end-tls-with-the-v2-sku)
- how it works
  ![](https://learn.microsoft.com/en-us/azure/application-gateway/media/how-application-gateway-works/how-application-gateway-works.png){:height 469, :width 1017}
- components
  ![](https://learn.microsoft.com/en-us/azure/application-gateway/media/application-gateway-components/application-gateway-components.png)
- routing
	- multi-hosting
	- url routing
	- redirection
	- rewrite HTTP headers and URL
- Application Gateway Ingress Controller