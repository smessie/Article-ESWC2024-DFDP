## Related Work
{:#related-work}

The idea of describing a form in RDF is not new.
This section covers related work, including research with similar focuses and relevant technologies that can be applied or extended in our work.

### Standalone Technologies

A first standalone technology is [XForms 2.0](cite:cites xforms).
It is a W3C specification language to define forms based on XML and also has a split architecture that separates presentation, content, and purpose, closely relating to the three parts display, shape, and reasoning introduced in this paper.
A model specifies required data and can limit values by referencing an XML element, which can have attributes to define type and other constraints.
While an XML element for submission can specify the data destination and HTTP method, enabling actual reasoning within it is not feasible.
As we are doing research in the area of the Semantic Web where RDF is being used to semantically describe data, we believe that RDF has a lot of potential.
We therefore want to focus on RDF and do not consider XForms 2.0 any further in this research.

A technology using RDF is [RDForms](cite:cites metasolutions_rdforms_nodate), allowing form-based editing and presentation of RDF.
It consists of 2 main components: the *RDForms library* and the *RDForms templates*.
The first one is responsible for the parsing, serializing, and manipulation of RDF graphs, while the latter makes sure the right RDF expression is produced and manipulated.
Although this system successfully provides form-based editing and presentation of RDF data, it lacks reasoning capabilities, schema alignment tasks, and event-driven actions as introduced in the paper's concept.


### Ontologies

[SHACL](cite:cites shacl), short for Shapes Constraint Language, is a W3C recommendation vocabulary used to define and validate RDF graphs based on a set of conditions, which are declared in shapes and consist of constraints.
These shapes can also be viewed as a description of the data graphs they validate.
Besides validation, such descriptions can also be used for user interface building, or thus to define the form's display part.
A property shape comprises non-validating properties, ignored by SHACL processors, and validating properties that represent validation conditions.
The former can be utilized to provide supplementary information, such as for form construction, while the latter specify constraints on the values of the properties of the focus node.
Examples are `sh:datatype` and `sh:minCount`.

Solid-UI is the name for the User Interface widgets and utilities for Solid developed by the SolidOS team.
Next to the building blocks for Solid-based apps, there also exists a [Solid-UI vocabulary](cite:cites solid-ui), which will be of interest in this paper.
The vocabulary mainly focuses on the display part of forms.
Next to that, the form field's semantic meaning is contained in the form description by using the `ui:property` predicate.
Extra properties can be specified to define the field's behavior.
The blog post by Hochstenbach, Wright, and Turdean on [*RDF forms for Solid*](cite:cites hochstenbach_rdf_2022) discusses the utilization of the Solid-UI ontology to define forms in RDF and presents a state-of-the-art declarative form renderer using this ontology.

There were also other attempts to describe forms in RDF such as Daniël Beeke's [RDF-Form](cite:cites rdf-form).

For the footprint part, we need to describe what to do with the filled in data.
To describe the HTTP request that needs to take place, we can use Hydra.
[Hydra](cite:cites hydra) is a vocabulary to describe Web APIs in Linked Data. Its intended use is to describe the server side of the API in a machine-readable way.
By doing this, a client can use this description to talk to the API without the need to hard code how to talk to the API.
Even though this is already a step in the right direction, the focus of Hydra is on the server side, and not on the client side.
Additionally, only HTTP requests can be described, but there is a need for a more extensive vocabulary to also describe other actions, such as redirects or N3 Patches on existing resources.

The Function Ontology (FnO) [](cite:cites fno-paper) [](cite:cites fno-spec) is used to semantically define and describe implementation-independent functions, including their relations to related concepts such as parameters, and mappings to specific implementations and executions.
FnO is not restricted to describing HTTP requests, it can also describe other type of events.
