- [FSH (**F**HIR **Sh**orthand)](https://hl7.org/fhir/uv/shorthand/) is a specially-designed language for defining the content of [HL7](https://hl7.org/) [FHIR](https://www.hl7.org/fhir/R4/overview.html) [Implementation Guides](https://www.hl7.org/fhir/implementationguide.html) (IGs). It is designed to be simple and compact, and along with SUSHI can be used to produce FHIR profiles, extensions, and IGs.
- SUSHI (**S**USHI **U**nshortens **Sh**ortHand **I**nputs) is a FSH compiler. SUSHI converts FSH language to [FHIR artifacts](https://www.hl7.org/fhir/R4/overview.html). SUSHI can run in stand-alone mode or as part of the [HL7 IG Publisher](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation).
- GoFSH is a converter that takes FHIR artifacts (e.g., profiles, extensions, value sets, instances) and produces equivalent FSH. GoFSH is essentially the opposite of SUSHI. GoFSH helps you transition to FSH if you have an existing Implementation Guide produced by other methods.