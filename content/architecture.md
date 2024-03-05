## Architecture
{:#architecture}

<figure id="fig:eaen-currently-to-goal" class="halfwidth">
<img src="img/currently-to-goal.png" alt="[Figure of shift from single structure to a three-part view]" />
<figcaption markdown="block">
Transition from a single structure that hard-couples data to the application to a three-part view: form (for display), shape (for validation), and footprint (for reasoning).
</figcaption>
</figure>

As stated in the [Introduction](#introduction), many Web applications are built with the data tightly coupled to the application, resulting in poor data control for users and interoperability between applications.
This is even the case for many Solid applications that assume the data is stored in a fixed location in the pod and assuming a specific vocabulary is used.
Therefore, this paper proposes a three-part view on Solid Web forms.
While end-users will still be able to create Web forms as they do today, such as with drag-and-drop interfaces, storing the data decentralized in three parts allows organizations and end-users to reuse forms and data, saving time.
This shift from a single structure to a three-part view is shown schematically in [](#fig:eaen-currently-to-goal).
On the left, the current situation with the data stored in a single structure as a hard-coupled part of the application.
On the right, we propose a division into three parts: a form (for display), shape (for validation), and footprint (for reasoning) part.
As considerable research has been conducted on RDF data validation [](cite:cites tomaszuk2017rdf,prud2014shape,arndt2017using,boneva2017semantics) and several implementations exist [](cite:cites slabbinck_communitysolidservershape-validator-component_nodate,zazuko_rdf-validate-shacl_2023,bergwinkl_shacl-engine_2023), this part is not covered in this paper.

<figure id="fig:renderer-architecture">
<img src="img/stage-2.svg" alt="[Figure of high level architecture of declarative Solid applications]" />
<figcaption markdown="block">
A generic form renderer application can dynamically build an application for multiple viewing environments without assuming the interface and application design using the 3 inputs on the right and a reasoner to apply schema alignment and footprint tasks.
</figcaption>
</figure>

In traditional centralized Web applications, different users interact with the same centralized Web server using different interfaces, all written for and working only with that server.
Additionally, the data is stored on the server of the application, outside the user's control.
The [Solid protocol](cite:cites solid-protocol) provides a standardized interface by providing a set of standard, open, and interoperable data formats and protocols [](cite:cites solid).
As a result, different applications can use this set of protocols to work with the same data, overcoming the problem of each application using its own interface only working with that server.
Because Solid stores data in a personal data vault called a Solid pod, it solves the issue of data storage outside the user's control.
However, many applications are still being built with assumptions about the data that is stored in the pod, like the storage location and used vocabulary.
Additionally, they are designed for one specific use case.
In this work, we push this decentralized architecture a step further with the introduction of a declarative Solid application that makes no assumptions about the interface and application itself.
A schematic overview of the architecture is shown in [](#fig:renderer-architecture).
First, a user that wants to create a form should build a declarative form description using a form generator.
Then, it can send that form description to another user to fill it out.
The user wanting to fill out the form should use a form renderer to render the declarative form description.
The user can additionally provide a conversion rules resource to map the form description onto another ontology and a data resource to automatically prefill the form.


### Description of the Display

The previous problem of needing a separate application for each use case is solved by describing the user interface declaratively in the *form description resource*.
This RDF resource contains both the display part and the footprint for the reasoning part.
The display is the part responsible for rendering the form to the user.
Web forms are typically rendered using HTML, while RDF represents the semantics of the form, not how you represent it in HTML.
By declaratively describing the form in RDF, we achieve the ability to render the same form description in any environment.
There already exist ontologies that can be used for this purpose, such as [SHACL](cite:cites shacl), [Solid-UI](cite:cites solid-ui), and [RDF-Form](cite:cites rdf-form).
By reusing these ontologies for the display part, we achieve maximum compatibility with existing form descriptions.
Semantic and declarative descriptions also enable machines to interpret the form's meaning, facilitating machine-driven prefilling of forms.
This is achieved with the binding property on each form field, linking to the meaning of that field.
The already existing predicates in the UI ontologies can be reused for that, e.g. `ui:property` for Solid-UI, `form:binding` for RDF-Form, and `sh:path` for SHACL.
The form's binding, describing its meaning, serves as the type for the resulting data subject after form completion.
The form field's bindings will serve as predicates on that subject, describing the meaning of these fields, with the filled-in values for these fields as objects.
The *data resource* structure mirrors the filled-out form's output, enabling automatic prefilling of the form.


### Description of the Schema Alignment Tasks

Unfortunately, the move to decentralization and decoupling comes with its own challenges.
Two main challenges need to be tackled before this can be achieved.
To allow the application to interpret multiple ontologies and hence achieve a decoupled solution, *schema alignment tasks* are introduced translating the form description into an ontology the application understands.
This enables the application to treat two definitions that semantically describe the same thing as identical.
The *conversion rules resource* from [](#fig:renderer-architecture) is used by the renderer application to perform this mapping.
This resource consists of rules defining how to go from a part of the form description in the ontology equivalent to the one understood by the application, to the equivalent expression in that ontology the application understands.
By passing along this resource to the application, the application does not need to understand the ontology the form description is written in, and any ontology can be used for which a mapping can be provided.
As these conversion rules can be passed as a separate resource to the application, the end-user does not necessarily have to create them himself. 
Ontology creators can provide mappings to similar ontologies, or application developers can provide mappings from equivalent ontologies to the one their application understands.
The renderer application needs to apply these rules onto the form description using a reasoner to retrieve the form description in the language it understands.


### Description of the Footprint Tasks

In addition to describing how the form should look, the form description should also declaratively describe what should happen in certain events such as submission.
Therefore, the form description is extended with *policies*.
The process of executing these policies is called the *footprint tasks* and is the second application of reasoning next to schema alignment.
To describe policies, two languages are needed: a *rule language* and a *policy language*.
The policy language describes what should actually happen when a policy is executed.
The rule premise contains the event, the rule conclusion contains the policy.
Policies should describe the client-side operations that need to be performed when a certain event occurs.
This can be much more than just performing an HTTP request to the server, such as redirecting the user, performing an *N3 Patch* request, or sending a notification to someone's inbox.
