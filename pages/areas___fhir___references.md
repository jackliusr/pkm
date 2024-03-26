- ```json
  {
    // from Element: extension
    "reference" : "<string>", // I Literal reference, Relative, internal or absolute URL
    "type" : "<uri>", // Type the reference refers to (e.g. "Patient") - must be a resource in resources
    "identifier" : { Identifier }, // I Logical reference, when literal reference is not known
    "display" : "<string>" // I Text alternative for the resource
  }
  ```
- **Constraints**
- | **id** | **Level** | **Location** | **Description** | **[Expression](https://www.hl7.org/fhir/fhirpath.html)** |
  | **![img](https://www.hl7.org/fhir/assets/images/test-null.png) ref-1** | [Rule](https://www.hl7.org/fhir/conformance-rules.html#rule) | (base) | SHALL have a contained resource if a local reference is provided | reference.exists() implies (reference.startsWith('#').not() or (reference.substring(1).trace('url') in %rootResource.contained.id.trace('ids')) or (reference='#' and %rootResource!=%resource)) |
  | **![img](https://www.hl7.org/fhir/assets/images/test-null.png) ref-2** | [Rule](https://www.hl7.org/fhir/conformance-rules.html#rule) | (base) | At least one of reference, identifier and display SHALL be present (unless an extension is provided). | reference.exists() or identifier.exists() or display.exists() or extension.exists() |
- contained resource and local relative reference
  ```json
  {
    "resourceType" : "Condition",
    "contained": [
      {
        "resourceType" : "Practitioner",
        "id" : "p1",
        "name" : [{
          "family" : "Person",
          "given" : ["Patricia"]
        }]
  	  }],
     "asserter" : {
       "reference" : "#p1"
    }
  }
  ```
- For a resource that references the container, the reference is "#", 
  ```xml
  <Patient xmlns="http://hl7.org/fhir">
    <id value="something"/>
    <contained>
      <Provenance>
        <!-- no id necessary (though still allowed) -->
        <target>
          <reference value="#"/>
        </target>
      </Provenance>
    </contained>
    <!-- other attributes -->
  </Patient>
  ```