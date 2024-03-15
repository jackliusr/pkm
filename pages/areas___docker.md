- Docker Content Trust (DCT) provides the ability to use digital signatures for data sent to and received from remote Docker registries. These signatures allow client-side or runtime verification of the integrity and publisher of specific image tags.
	- [Signing Images with Docker Content Trust](https://docs.docker.com/engine/security/trust/#signing-images-with-docker-content-trust)
		- ``` bash
		  docker trust key generate jeff
		  docker trust key load key.pem --name jeff
		  docker trust signer add --key cert.pem jeff registry.example.com/admin/demo
		  docker trust sign registry.example.com/admin/demo:1
		  
		  ' Alternatively, once the keys have been imported an image can be pushed with the 
		  ' $ docker push command, by exporting the DCT environmental variable.
		  export DOCKER_CONTENT_TRUST=1
		  docker push registry.example.com/admin/demo:1
		  
		  The push refers to repository [registry.example.com/admin/demo:1]
		  7bff100f35cb: Pushed
		  1: digest: sha256:3d2e482b82608d153a374df3357c0291589a61cc194ec4a9ca2381073a17f58e size: 528
		  Signing and pushing trust metadata
		  Enter passphrase for signer key with ID 8ae710e:
		  Successfully signed registry.example.com/admin/demo:1
		  
		  docker trust inspect --pretty registry.example.com/admin/demo:1
		  ```
	- issues:
		- [How do I look at what's cached by Docker](https://stackoverflow.com/questions/54290925/how-do-i-look-at-whats-cached-by-docker)