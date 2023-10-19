## Related Work
{:#related-work}

The idea of describing a form in RDF is not new.
In the literature, there are already some existing approaches that describe a form in RDF.
As was already mentioned in the introduction, the idea of this paper is to split up the form in three separate parts.
The first part is the display part and consists of the form definition in Linked Data.
To be able to define a form, a vocabulary or ontology is needed that functions as the language.
Most of the existing approaches to describe a form in RDF are based on one ontology to express the in this paper called display part.
In the following, first, some standalone technologies are discussed, after that some notable ontologies are discussed. Finally, some state of the art SHACL validation tools are discussed.

mention the gaps
{:.todo}


### Standalone Technologies

#### XForms 2.0

For the reasoning part, a language is needed to express what actions should happen at what events. You should e.g. be able to define what should happen with the filled-in data when the user clicks on the submit button. Do we want to perform some checks on it? Do we want to alter the data? Do we want to store it somewhere? 

One existing specification seeming useful for this problem is [XForms 2.0](cite:cites xforms).
This language to define forms is a W3C specification.
It is based on XML and also has a split architecture that separates presentation, content, and purpose, closely relating to the three parts: display, shape, and reasoning which are used to tackle the problem in this paper.
In XForms 2.0, a model defines what data is needed, then one can have XML data defined concerning the model to become submitted data.
Values can be constrained by defining bindings. A bind element can be defined by referring to an XML element which is part of a model. By adding attributes to that bind element, the type can be specified and other constraints can be set.
A submission XML element can be added to define the destination of the data. Next to that, the HTTP method can also be specified.
However, adding statements allowing to perform actual reasoning is something that does not exist in XForms 2.0.
Next to this limited possibility to reason over the data, it is also an XML-based language, and as defining the forms in RDF is desired because that is what is nowadays being used in this domain, it is not a perfect fit for this research. It could however still be useful as a form of inspiration.


#### RDForms

[RDForms](cite:cites metasolutions_rdforms_nodate) is a technology that allows form-based editing and presentation of RDF.
It is an editing framework for RDF that focuses on read-write Linked Data while keeping it as simple as possible for the developer.
It does so by providing 2 main components: the *RDForms library* and the *RDForms templates*.
The first one is responsible for the parsing, serializing, and manipulation of RDF graphs, while the latter makes sure the right RDF expression is produced and manipulated.
These templates can be used for presentation, editing, and validation of RDF data.
Although this does the job of providing form-based editing and presentation of RDF, it does not include any reasoning possibilities as was introduced for the idea of this paper.
There is no possibility to apply schema alignment tasks or anything similar to that, nor is it possible to define actions to be performed on the occurrence of certain events.
It is just a tool to construct form-based RDF editors with the requirement that RDF must be non-cyclic with a single root node.


### Ontologies

#### SHACL
{:#shacl}

The first ontology is [SHACL](cite:cites shacl), short for Shapes Constraint Language, which is a W3C recommendation. It is a vocabulary to describe and validate RDF graphs against a set of conditions. 
As the name suggests, SHACL is used to declare shapes, the target of the shape is specified with the `sh:targetClass` property.
SHACL can be used for validation, during this validation, the target nodes become focus nodes for the shape. This is a shape-validated RDF term using the triples from a data graph. In other words, the values of the properties and other characteristics of the focus node are validated against the constraints defined in the shape.
Node shapes are used to declare constraints on the focus nodes. These constraints can be various kinds of things but are about the focus node itself. Other constraints can be declared as well by the node shape via the `sh:property` property to a property shape. Constraints like `sh:datatype` and `sh:minCount` are being declared by these property shapes.
In contrast to node shapes, property shapes are used to declare constraints on the values of the properties of the focus nodes. These constraints can be about the value of the property itself or the value of the property concerning the focus node.

SHACL also provides some non-validating properties that are ignored by the SHACL processors. These properties can be used to provide additional information, e.g. for building a form. Some of those properties that speak for themselves are `sh:name`, `sh:description` and `sh:order`, but also `sh:defaultValue` and `sh:group` can be used to provide additional information.
These non-validating properties could be used in the context of a form to define what the form should look like. For example, the `sh:defaultValue` property could be used to define what the default value of a field should be. The `sh:group` property could be used to group fields together in a form. The `sh:order` property could be used to define the order in which the fields should be displayed in the form.


#### Solid-UI

Solid-UI is the name for the User Interface widgets and utilities for Solid developed by the SolidOS team. Next to the building blocks for Solid-based apps, there also exists a [Solid-UI vocabulary](cite:cites solid-ui), which will be of interest in this paper.

The vocabulary mainly focuses on the display and rendering part of the front end of forms.
Next to that, a crucial part is that it provides a binding to the underlying Linked Data. To do so, the `ui:property` predicate is used to bind a form field to a property of the underlying data.
There exist many different kinds of form fields like `ui:SingleLineTextField`, `ui:MultiLineTextField`, `ui:DateField`, `ui:BooleanField`, `ui:Choice`, etc. To define a field using one of these types, a subject must receive the `rdf:type` predicate with the type as the object.
Additionally, extra properties can be defined with predicates like `ui:label`, `ui:sequence`, `ui:required`, `ui:multiple`, `ui:maxLength`, `ui:pattern`, etc. to define the behavior of the field.
To define a choice or select field, the subject of type `ui:Choice` must receive a `ui:from` predicate with as object an instance of `owl:Class`. Then all instances of that class will be used as options for the select field.

The blog post by Hochstenbach, Wright, and Turdean on [*RDF forms for Solid*](cite:cites hochstenbach_rdf_2022) discusses how the Solid-UI ontology can be used to define forms in RDF and presents a state of the art declarative form renderer using that ontology.
These forms allow users to edit their data in their Solid Pod in a user-friendly way, providing a use case for the Solid-UI ontology.
In addition, Smessaert's blog post on [*Google Forms but the Solid way*](cite:cites smessaert_google_2022) demonstrates how such an RDF form description can be created in a user-friendly way using a drag-and-drop interface.
A form description can be created not only in the Solid-UI ontology, but also in the SHACL ontology as well as in the RDF-Form ontology.


#### RDF-Form

[RDF-Form](cite:cites rdf-form) is another vocabulary that can be used to define forms in RDF. Different from SHACL and Solid-UI, RDF-Form has no way defined to link the fields to the form object.
This means that all the fields that are defined in the same resource file as the form are being used for that form. This is a limitation of RDF-Form, but it is also a simplification as it is not needed to define a link between the form and the fields. 
However, this does not conform to the idea of Linked Data, where everything should be linked to everything else and multiple form definitions can be defined in the same resource file.

RDF-Form has multiple properties defined to function as predicates on form fields. One important predicate is `form:widget` which is used to define what kind of field it is.
The value of this predicate is a string which is the name of the field type. Examples are `"string"`, `"group"`, `"textarea"`, `"number"`, `"dropdown"`, `"duration"`, etc.
Next to that, there are also predicates like `form:label`, `form:required`, `form:order`, `form:placeholder`, `form:option`, etc.
This `form:required` is only one of the few predicates that can be used to add some basic validation to the form. However, more advanced validation is not possible with RDF-Form.
Again, a `form:binding` predicate exists to bind the field to a property of the underlying data. This triple has as its object value a URI which is the property that the field is bound to.


#### Hydra

[Hydra](cite:cites hydra) is a vocabulary to describe Web APIs in Linked Data. Its intended use is to describe the server side of the API in a machine-readable way.
There already exist some technologies to describe a data model, but with Hydra, the focus is on describing Web APIs to, as a server being, advertise to a client what possible actions are allowed to make changes to the data. 
By doing this, a client can use this description to talk to the API without the need to hardcode how to talk to the API.
The Web API is being defined as an `ApiDocumentation` class. In this class, the main entry point of the API can be defined. Next to that, it can also hold the supported operations, classes, and properties. 
As sometimes HTTP status codes are not expressive enough on their own to describe the actual problem, extra information can be given to status codes as well.
Something not yet possible in RDF serializations is the ability to machine-readable describe whether an IRI is dereferenceable or if it can only be used as an identifier. With the `Link` class, Hydra allows us to describe this.
Hydra also has the functionality to mark properties as read-only, write-only, and required. Lastly, it also has numerous other concepts that lean towards the backend description of a Web API, like the `PagedCollection` which gives extra info about paginated requests.


#### The Function Ontology

The Function Ontology (FnO) is a way to, semantically, define and describe implementation-independent functions, just like their relations to related concepts such as parameters, and mappings to specific implementations and executions.
It is first introduced in [*Implementation-independent function reuse*](cite:cites fno-paper) by Ben De Meester et al. The full specification is available at [https://w3id.org/function/spec](cite:cites fno-spec).

A link can be made with the Hydra vocabulary as the `hydra:ApiDocumentation` can be seen as a `fno:Implementation`. To be able to describe what a `fno:Implementation` is, some other parts of the Function Ontology need to be discussed first.
First, a `fno:Function` is a process that performs a specific task by associating one or more inputs to an output. It expects a list of ordered *Parameters* and returns a list of *Outputs*. The Parameters define the relation being used for the execution in the form of a predicate and can also hold a specific type or other metadata.
*Functions* can be linked to *Problems*, which are a more general description in comparison to Functions. Problems themselves can be linked to other Problems by using the [SKOS standard](cite:cites skos).
A `fno:Execution` links the input data and the resulting output data to the parameters and outputs of Functions. It allows one to describe independently of the implementation how input data is transformed into output data.
A `fno:Implementation` is a set of function units. The description of the implementation itself is decoupled from the Function Ontology (FnO). The model is not limited to a specific set of supported development contexts by allowing any development context to be specified.
Lastly, a `fno:Mapping` connects an abstract function with a specific part of a concrete implementation existing of a link between the function and the implemented method and a link between the inputs and outputs of a function and the parameters and returns values of the methods.

One application of the Function Ontology is the [Orchestrator](cite:cites orchestrator), a specification describing the implementation requirements for the Orchestrator component.
It uses FnO to describe what should happen when a trigger takes place, i.e. the event to which the Orchestrator responds.
An example of a policy is taken from the [Orchestrator specification](cite:cites orchestrator) and is shown below in [](#lst:policy-example).
These policies are written in a *policy language* understandable by the Orchestrator.
In practice, this means that policies are written using a *rule language* like SHACL, SPARQL, or Notation3.
In the then-part of the policy, the FnO description is expressed.
When the orchestrator detects that a new triple `?notification a as:Create` is added to one of the watched resources, it will execute the then-part.
In this case, it will send a notification to Bob. This is done by executing the function `ex:sendNotification` with the parameter `ex:notification` set to the value of `?notification`.

<figure id="lst:policy-example" class="listing">
<pre><code>#!turtle
rule "Notify Bob about newly created artifacts"

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
Example of a policy.
</figcaption>
</figure>


### Validation

#### Shape-Validator-Component

There has already been done quite some research on how to validate RDF data.
The most common way is to use SHACL, discussed earlier in [](#shacl).
In Slabbinck's thesis about cross-application interoperability [](cite:cites slabbinck_interoperabiliteit_2021), data validation using Shape Trees is discussed.
[Shape Trees](cite:cites prudhommeaux_shape_2021) are a way to describe the shape of data in a way that is independent of the actual data.
This allows one to validate data without having to know the actual data.
With the `st:shape` property, a Shape Tree can be linked to a SHACL or ShEx shape. This allows using SHACL or ShEx to validate data against a Shape Tree.
Slabbinck also made a [shape validator component](cite:cites slabbinck_communitysolidservershape-validator-component_nodate) implementing such a Shape Tree validator using SHACL shapes.
This component, made for the Community Solid Server, allows to validate data against a Shape Tree using a SHACL shape to make sure that all the resources in the containers conform to that shape.
Having this guarantee let applications assume that this structure in the resources is correct and can be used to build on top of it.
Only resources that conform will be able to be added to the constrained container.


#### Rdf-Validate-Shacl

The previously mentioned implementation is a validator that functions on the server side.
Next to that, client-side validation is also something possible and has been researched before.
One example is the [rdf-validate-shacl package by Zazuko](cite:cites zazuko_rdf-validate-shacl_2023).
This is a JavaScript package that implements the SHACL specification on top of the RDFJS stack.
It works by first initializing the validator with a given shape and then validating a given dataset against that shape.
The validator will then return a list of validation results that can be used to determine if the dataset conforms to the shape. This is done in the form of a `ValidationReport` object containing on one hand these results and on the other hand a boolean `conforms` indicating if the dataset conforms to the shape.
Everything is done in JavaScript and can thus be used on the client side.


#### Shacl-Engine

Another noteworthy implementation of a client-side validator in JavaScript is the [*shacl-engine* package by Thomas Bergwinkl](cite:cites bergwinkl_shacl-engine_2023).
At the time of writing, it is a new implementation of the SHACL specification that focuses on performance.
The author discovered a bottleneck in the rdf-validate-shacl package, discussed in [](#h3:related_work/rdf-validate-shacl), and decided to create a new implementation that would be faster.
Fetching all properties and values from the `Dataset` object in that package each time a shape is processed results in that bottleneck [](cite:cites bergwinkl_implementing_2023).
This implementation eliminates this cost by introducing a compile step.
This step finds a matching compile function while going through all properties of a shape and then adds the result of that function to the shape.
By doing so, validating a dataset can now be done by using the compiled validation functions.
A comparison of the performance of the two implementations shows that the `shacl-engine` package is 15 times faster than the `rdf-validate-shacl` package [](cite:cites bergwinkl_implementing_2023).
