- Redocly vs. Swagger vs blobr
- tools comparision: https://www.blobr.io/vs-pages/redocly-vs-swagger
- fixed fields
  collapsed:: true
	- |field name | type  | description|
	  | --- | --- | ---|
	  |openapi | string|**REQUIRED**. This string MUST be the [version number](https://swagger.io/specification/#versions) of the OpenAPI Specification that the OpenAPI document uses. The `openapi` field SHOULD be used by tooling to interpret the OpenAPI document. This is *not* related to the API [`info.version`](https://swagger.io/specification/#info-version) string. |
	  |info | Info object | **REQUIRED**. Provides metadata about the API. The metadata MAY be used by tooling as required.|
	  |jsonSchemaDialect | string | The default value for the `$schema` keyword within [Schema Objects](https://swagger.io/specification/#schema-object) contained within this OAS document. This MUST be in the form of a URI.|
	  |servers| [Server Object](https://swagger.io/specification/#server-object) | An array of Server Objects, which provide connectivity information to a target server. If the `servers` property is not provided, or is an empty array, the default value would be a [Server Object](https://swagger.io/specification/#server-object) with a [url](https://swagger.io/specification/#server-url) value of `/`.|
	  |paths | Paths object | The available paths and operations for the API. |
	  | webhooks | Map[`string`, [Path Item Object](https://swagger.io/specification/#path-item-object) [Reference Object](https://swagger.io/specification/#reference-object)]| The incoming webhooks that MAY be received as part of this API and that the API consumer MAY choose to implement. Closely related to the `callbacks` feature, this section describes requests initiated other than by an API call, for example by an out of band registration. The key name is a unique string to refer to each webhook, while the (optionally referenced) Path Item Object describes a request that may be initiated by the API provider and the expected responses. An [example](https://github.com/-o-a-i/-open-a-p-i--specification/blob/main/examples/v3.1/webhook-example.yaml) is available.|
	  | component | [Components Object](https://swagger.io/specification/#components-object) | An element to hold various schemas for the document.|
	  | security | [Security Requirement Object](https://swagger.io/specification/#security-requirement-object) | A declaration of which security mechanisms can be used across the API. The list of values includes alternative security requirement objects that can be used. Only one of the security requirement objects need to be satisfied to authorize a request. Individual operations can override this definition. To make security optional, an empty security requirement (`{}`) can be included in the array.|
	  |tags | Tag object | A list of tags used by the document with additional metadata. The order of the tags can be used to reflect on their order by the parsing tools. Not all tags that are used by the [Operation Object](https://swagger.io/specification/#operation-object) must be declared. The tags that are not declared MAY be organized randomly or based on the tools' logic. Each tag name in the list MUST be unique.|
	  | externalDocs | [External Documentation Object](https://swagger.io/specification/#external-documentation-object) | | Additional external documentation. ||
- api linter
	- [api-linter](https://github.com/googleapis/api-linter?ref=apisyouwonthate.com) by Google:  protocol buffer
	- [graphql-doctor](https://github.com/cap-collectif/graphql-doctor?ref=apisyouwonthate.com) by [Cap Collectif](https://cap-collectif.com/?ref=apisyouwonthate.com)
	- [graphql-schema-linter](https://github.com/cjoudrey/graphql-schema-linter?ref=apisyouwonthate.com) by [Christian Joudrey](https://twitter.com/cjoudrey?ref=apisyouwonthate.com)
	- [Spectral](https://stoplight.io/open-source/spectral/?ref=apisyouwonthate.com) by [Stoplight](https://stoplight.io/?ref=apisyouwonthate.com): openapi, json
- **SAFE** API design: Single responsibility, API versioning, First Class Specifications, and an External interface
- toos:
	- https://bitbucket.org/atlassian/swagger-request-validator/src/master/
	- https://github.com/OpenAPITools/openapi-generator
	- openapi-examples-validator: Validates embedded JSON-examples in OpenAPI-specs (v2 and v3 are supported)
	- https://openapi.tools/
	- OpenAPI-diff