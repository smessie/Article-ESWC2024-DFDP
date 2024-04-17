## Architecture
{:#architecture}

As outlined in the [Introduction](#introduction), many Web applications tightly integrate data with the application itself, limiting end-user control over data and hindering interoperability between applications.
This issue persists even in Solid applications, where data is often assumed to reside in fixed locations within the pod and to adhere to specific vocabularies.
Therefore, this paper proposes dividing data into three parts: a form for display, a shape for validation, and a footprint for reasoning.
Reasoning is used to determine the policy that needs to be executed based on the event specified in the footprint along with its associated policy.
This three-part approach moves away from the current scenario where data is stored as an integral, tightly coupled part of the application.
While end-users can continue to create web forms using familiar methods, such as drag-and-drop interfaces, storing the data decentralized in three parts allows organizations and end-users to reuse forms and data, saving time.
As considerable research has been conducted on RDF data validation [](cite:cites tomaszuk2017rdf,prud2014shape,arndt2017using,boneva2017semantics) and several implementations exist [](cite:cites slabbinck_communitysolidservershape-validator-component_nodate,zazuko_rdf-validate-shacl_2023,bergwinkl_shacl-engine_2023), this part is not covered in this paper.

In traditional centralized Web applications, different users interact with the same centralized Web server using different interfaces, all written for and working only with that server.
Additionally, the data is stored on the application's server, outside the user's control.
The [Solid protocol](cite:cites solid-protocol) provides a standardized interface by providing a set of standard, open, and interoperable data formats and protocols [](cite:cites solid).
As a result, different applications can use this set of protocols to work with the same data, overcoming the problem of each application using its own interface only working with that server.
Because with Solid, the data is stored in a personal data store called a pod, it solves the issue of data storage outside the user's control.
However, many applications are still being built with assumptions about the data stored in the pod, like the storage location and used vocabulary.
Additionally, they are designed for one specific use case.
In this work, we push this decentralized architecture a step further with the introduction of a declarative application that makes no assumptions about the interface and application itself.
A schematic overview of the architecture is shown in [](#fig:renderer-architecture).
First, a user who wants to create a form builds a declarative form description using a form generator.
Then, the user sends a form description link to another user who can fill it out using a form renderer.
A conversion rules resource maps the form description onto the renderer's ontology, while a data resource pre-fills the form automatically.

<figure id="fig:renderer-architecture">
<img src="img/stage-2.svg" alt="[Figure of high level architecture of declarative applications]" />
<figcaption markdown="block">
A generic form renderer application can dynamically build an application for multiple viewing environments without assuming the interface and application design using the 3 inputs on the right and a reasoner to apply schema alignment and footprint tasks, to eventually store the enduser's filled in data in any data store, e.g. a Solid pod, as displayed on the left.
</figcaption>
</figure>


### Description of the Display

The previous problem of needing a separate application for each use case is solved by describing the user interface declaratively in the *form description resource*.
This RDF resource contains both the display part and the footprint for the reasoning part.
The display is the part responsible for rendering the form to the user.
Web forms are typically rendered using HTML, while RDF represents the semantics of the form, not how you represent it in HTML.
By declaratively describing the form in RDF, we achieve the ability to render the same form description in any environment.
There already exist ontologies that can be used for this purpose, such as [SHACL](cite:cites shacl), [UI ontology](cite:cites solid-ui), and [RDF-Form](cite:cites rdf-form).
Reusing these ontologies for the display part ensures maximum compatibility with existing form descriptions.
Semantic and declarative descriptions also enable machines to interpret the form's meaning, facilitating machine-driven prefilling of forms.
This is achieved with the binding property on each form field, linking to the meaning of that field and serving as the predicate of the triple with the filled-in values for these fields as objects.
The subject's type describing the form's meaning is equal to the form's binding.
The *data resource* structure mirrors the filled-out form's output, enabling automatic prefilling of the form.


### Description of the Schema Alignment Tasks

Unfortunately, the move to decentralization and decoupling comes with its own challenges.
Two main challenges need to be tackled before this can be achieved.
To allow the application to interpret multiple ontologies and hence achieve a decoupled solution, *schema alignment tasks* are introduced translating the form description into an ontology the application understands.
This enables the application to treat two definitions that semantically describe the same thing as identical.
The *conversion rules resource* from [](#fig:renderer-architecture) is used by the renderer application to perform this mapping.
By providing this resource to the application, it doesn't need to comprehend the form description's ontology.
Any ontology with a mapping can be used.
The renderer applies these rules using a reasoner to interpret the form description in its language.
As these conversion rules can be passed as a separate resource to the application, the end-user does not necessarily have to create them himself. 
Ontology creators can provide mappings to similar ontologies, or application developers can provide mappings from equivalent ontologies to the one their application understands.


### Description of the Footprint Tasks

In addition to describing how the form should look, the form description should also declaratively describe what should happen in certain events such as submission.
Therefore, the form description is extended with *policies*.
The process of executing these policies is called the *footprint tasks* and is the second application of reasoning next to schema alignment.
To describe policies, two languages are needed: a *rule language* and a *policy language*.
The policy language describes what should actually happen when a policy is executed.
The rule premise contains the event and the rule conclusion contains the policy.
Policies should describe the client-side operations that need to be performed when a certain event occurs.
This can be much more than just performing an HTTP request to the server, such as redirecting the end-user who filled out the form, performing an *N3 Patch* request, or sending a notification to someone's inbox.
