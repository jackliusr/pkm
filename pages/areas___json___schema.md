- JSON Hyper-Schema: offering a [vocabulary](https://json-schema.org/learn/glossary#vocabulary) to annotate JSON documents with hypermedia controls. define links and actions that can be executed on JSON data
- [JSON Schema - Structuring a complex schema (json-schema.org)](https://json-schema.org/understanding-json-schema/structuring#structuring-a-complex-schema)
- meta-schema
- title, description,`markdownDescription`
- Subschemas
	- `$defs`: `$defs` keyword gives us a standardized place to keep subschemas intended for reuse in the current schema document.
	- `$defs` vs "definitions"
- type array vs oneOf vs anyOf
	- `anyOf` means the item must validate against at least one (but possibly *more than one*) of the schemas. `oneOf` means it must validate against *only one* of the schemas.
- combine schemas:
	- `allOf`: (AND) Must be valid against *all* of the subschemas
	- `anyOf`: (OR) Must be valid against *any* of the subschemas
	- `oneOf`: (XOR) Must be valid against *exactly one* of the subschemas
	- `not`: (NOT) Must *not* be valid against the given schema
- Conditional Schema
	- `dependentRequired`
	- `dependentSchemas`
	- if-then-else
	- implication: allOf, not etc.
- types
	- string:
		- length: `minLength` and `maxLength`
		- pattern: [ECMA 262](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/)
		- [format](https://json-schema.org/understanding-json-schema/reference/string#built-in-formats):
		  | category| name | sample|
		  | date | `date-time` | 2018-11-13T20:20:39+00:00|
		  | date | `time` | 20:20:39+00:00|
		  | date | `date` | 2018-11-13|
		  | date | `duration` | A duration as defined by the [ISO 8601 ABNF for "duration"](https://datatracker.ietf.org/doc/html/rfc3339#appendix-A). For example, `P3D` expresses a duration of 3 days.|
		  |email| email |Internet email address, see [RFC 5321, section 4.1.2](http://tools.ietf.org/html/rfc5321#section-4.1.2). |
		  |email| idn-email| The internationalized form of an Internet email address, see [RFC 6531](https://tools.ietf.org/html/rfc6531).|
		  | hostname|hostname | |
		  | idn-hostname | ||
		  |ip address | ipv4 ||
		  |ip address | ipv6 ||
		  | resource |||
		  |uri template |||
		  | json pointer |||
		  | regex|||
	- object
		- [unevaluatedProperties](https://json-schema.org/understanding-json-schema/reference/object#unevaluatedproperties): `unevaluatedProperties` works by collecting any properties that are successfully validated when processing the schemas and using those as the allowed list of properties.
		- `additionalProperties`: The value of the `additionalProperties` keyword is a schema that will be used to validate any properties in the instance that are not matched by `properties` or `patternProperties`
		- size: `minProperties` and `maxProperties`
		- [propertyNames](https://json-schema.org/draft/2020-12/draft-bhutton-json-schema-01#name-propertynames) #inbox
	- array:
		- `prefixItems`
		- `contains`
		- `minContains` and `maxContains`
		- `unevaluatedItems`
		- `uniqueItems`
- Compound Schema Document: a JSON document (sometimes called a "bundled" schema) which has multiple embedded JSON Schema Resources bundled into the same document to ease transportation.
- [Using Dynamic References to Support Generic Types (json-schema.org)](https://json-schema.org/blog/posts/dynamicref-and-generics#representing-generics-with-and)
	- `$dynamicRef`
	- `$dynamicAnchor`
- [Modelling Inheritance with JSON Schema](https://json-schema.org/blog/posts/modelling-inheritance)
- Generate jsonschema from class using prompt for chatgpt: #prompts
  ```
  Can I have a jsonschema of [class] in yaml format?
  ```
- [JSON editing in Visual Studio Code](https://code.visualstudio.com/Docs/languages/json#_json-schemas-and-settings)
  collapsed:: true
	- Mapping in the JSON: $schema
	- Mapping in the User Settings: 
	  ```json
	  "$schema": "vscode://schemas/settings/user",
	  ```
	- Mapping to a schema in the workspace
	  ```json
	  "json.schemas": [
	      {
	          "fileMatch": [
	              "**/*.foo.json"
	          ],
	          "url": "./myschema.json"
	      }
	  ]
	  ```
	- Mapping to a schema defined in settings
	  ```json
	  "json.schemas": [
	      {
	          "fileMatch": [
	              "/.myconfig"
	          ],
	          "schema": {
	              "type": "object",
	              "properties": {
	                  "name" : {
	                      "type": "string",
	                      "description": "The name of the entry"
	                  }
	              }
	          }
	      }
	  ]
	  ```
	- [Mapping a schema in an extension](https://code.visualstudio.com/api/references/contribution-points#contributes.jsonValidation)
	- File match syntax
	- Define snippets in JSON schemas: 
	  ```json
	     "defaultSnippets": [
	              {
	                  "label": "New keybinding",
	                  "description": "Binds a key to a command for a given state",
	                  "body": { "key": "$1", "command": "$2", "when": "$3" }
	              }
	     ],
	  ```
	- Use rich formatting in hovers: markdownDescription
	- Offline mode: json.schemaDownload.enable