## Related Work
{:#related-work}

The idea of describing a form in RDF is not new.
This section covers related work, including research with similar focuses and relevant technologies that can be applied or extended in our work.

### Standalone Technologies

A first standalone technology is [XForms 2.0](cite:cites xforms), a W3C specification language to define forms.
It is based on XML and also has a split architecture that separates presentation, content, and purpose, closely relating to the three parts display, shape, and reasoning introduced in this paper.
A model specifies required data and can limit values by referencing an XML element, which can have attributes to define type and other constraints.
While an XML element for submission can specify the data destination and HTTP method, enabling actual reasoning within it is not feasible.
Furthermore, XForms 2.0 is not an ideal choice, given its XML nature compared to the predominant use of RDF in this field.

A technology using RDF is [RDForms](cite:cites metasolutions_rdforms_nodate), allowing form-based editing and presentation of RDF.
It consists of 2 main components: the *RDForms library* and the *RDForms templates*.
The first one is responsible for the parsing, serializing, and manipulation of RDF graphs, while the latter makes sure the right RDF expression is produced and manipulated.
Although this system successfully provides form-based editing and presentation of RDF data, it lacks reasoning capabilities, schema alignment tasks, or event-driven actions as introduced in the paper's concept.


### Ontologies

A first ontology is [SHACL](cite:cites shacl), short for Shapes Constraint Language, which is a W3C recommendation.
It is a vocabulary used to define and validate RDF graphs based on a set of conditions, which are declared in shapes and consist of constraints.
These shapes can also be viewed as a description of the data graphs they validate.
Besides validation, such descriptions can also be used for user interface building, or thus to define the form's display part.
A property shape comprises non-validating properties, which SHACL processors ignore, and validating properties that represent validation conditions.
The former can be utilized to provide supplementary information, such as for form construction, while the latter specify constraints on the values of the properties of the focus node.
Examples are `sh:datatype` and `sh:minCount`.

Solid-UI is the name for the User Interface widgets and utilities for Solid developed by the SolidOS team.
Next to the building blocks for Solid-based apps, there also exists a [Solid-UI vocabulary](cite:cites solid-ui), which will be of interest in this paper.
The vocabulary mainly focuses on the display part of forms.
Next to that, the form field's semantic meaning is contained in the form description by using the `ui:property` predicate.
Extra properties can be specified to define the field's behavior.
The blog post by Hochstenbach, Wright, and Turdean on [*RDF forms for Solid*](cite:cites hochstenbach_rdf_2022) discusses the utilization of the Solid-UI ontology to define forms in RDF and presents a state-of-the-art declarative form renderer using this ontology.

[RDF-Form](cite:cites rdf-form) is another vocabulary that can be used to define forms in RDF.
In contrast to SHACL and Solid-UI, RDF-Form has no way to link the fields to the form object.
As a result, all fields defined within the same resource file as the form are automatically associated with that form.
This approach contradicts the Linked Data principles, which encourages linking everything together and supports multiple form definitions within a single resource file.
The field type can be specified using the `form:widget` predicate, while the `form:binding` predicate is used to define a binding, similar to the previous ontologies.

For the footprint part, we need to describe what to do with the filled in data.
To describe the HTTP request that needs to take place, we can use Hydra.
[Hydra](cite:cites hydra) is a vocabulary to describe Web APIs in Linked Data. Its intended use is to describe the server side of the API in a machine-readable way.
By doing this, a client can use this description to talk to the API without the need to hard code how to talk to the API.
Even though this is already a step in the right direction, the focus of Hydra is on the server side, and not on the client side.
Additionally, only HTTP requests can be described, but there is a need of a more extensive vocabulary to also describe other actions, such as redirects or N3 Patches on existing resources.

Since Hydra falls short in achieving these tasks, we explored alternative ontologies.
The Function Ontology (FnO) [](cite:cites fno-paper) [](cite:cites fno-spec) is used to semantically define and describe implementation-independent functions, including their relations to related concepts such as parameters, and mappings to specific implementations and executions.
FnO is not restricted to describing HTTP requests, it can also describe other type of events.
Consequently, a simplified version of FnO can be used to describe the actions to be taken in response to events.
An example of such a policy is taken from the [Orchestrator specification](cite:cites orchestrator) and is shown below in [](#lst:policy-example).
When the orchestrator detects a new triple `?notification a as:Create`, it will execute the then-part.
In this case, it will send a notification to Bob. This is done by executing the function `ex:sendNotification` with the parameter `ex:notification` set to the value of `?notification`.

<figure id="lst:policy-example" class="listing">
<pre><code>rule "Notify Bob about newly created artifacts"

when
   ?notification a as:Create .

then
   ?notification as:target <http://bob.institution.org/profile/card#me> .

   [ a fno:Execution ;
     fno:executed ex:sendNotification
        ex:notification ?notification
   ] .
</code></pre>
<figcaption markdown="block">
Example of a policy with FnO.
</figcaption>
</figure>
