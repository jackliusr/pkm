- How do I verify that a private key matches a certificate? (OpenSSL)
- **[Mobile Certificate Pinning Generator](https://approov.io/tools/static-pinning/)**
- [cert list](https://www.rfc-editor.org/rfc/rfc4346#section-7.4.2:~:text=certificate_list%0A%20%20%20%20%20%20This%20is%20a%20sequence%20(chain)%20of%20X.509v3%20certificates.%20%20The%20sender%27s%0A%20%20%20%20%20%20certificate%20must%20come%20first%20in%20the%20list.%20%20Each%20following)
  Public-- Intermediate -- Root --Private
- cert -->  pfx
- [Verifying Your Keys Match](https://www.digicert.com/kb/ssl-support/openssl-quick-reference-guide.htm#:~:text=yourdomain.crt%20%2Dnoout-,Verifying%20Your%20Keys%20Match,-To%20verify%20the)
	- ```bash
	  # The below commands should be entered one by one to generate three separate outputs.
	  openssl pkey -pubout -in .\private.key | openssl sha256
	  openssl req -pubkey -in .\request.csr -noout | openssl sha256
	  openssl x509 -pubkey -in .\certificate.crt -noout | openssl sha256
	  ```
- Check the SSL certificate chain
  ```bash
  openssl verify -verbose -CAfile /path/to/ca-bundle.pem /path/to/certificate.pem
  ```
- Certificate Formats: By default, OpenSSL generates keys and CSRs using the PEM format.
	- PEM to PKCS\#12
		- ```bash
		  openssl pkcs12 -export -name "yourdomain-digicert-(expiration date)" \
		  -out yourdomain.pfx -inkey yourdomain.key -in yourdomain.crt
		  ```