## Motivation and Requirements
{:#requirements}

In this section, we discuss the main requirements for decentralized and declarative Web forms using a use case involving two personas, "Alice" and "Bob", each with their own objectives about the forms they like to publish, but both requiring full control over where and how the resulting RDF is stored.

Alice, a Web-savvy user, owns a personal data store for storing RDF data.
She is a researcher seeking to include a list of her publications within her personal data store as an integral part of her CV.
Companies typically request CVs without providing a tailored form for their creation.
Rather than relying on a pre-existing CV application with a fixed data structure, Alice prefers to use her own rendering.
This allows her to employ an existing CV data model while also incorporating her own metadata.
Consequently, companies will retrieve richer data.

To create a form to populate her data store, Alice uses *AliceForms*, which shares similarities with Google Forms.
*AliceForms* enables form creation in a user-friendly manner with a simplified data model.
Importantly, Alice retains control over where the form description and resulting RDF data are stored, ensuring control over the data she enters --- an option not available in centralized platforms like Google Forms.

When Alice wants to create RDF data, she opens the form description in the renderer application *HtmlForms*, providing her with an HTML rendered version of the form description.
When Alice fills out the form, the RDF data will be stored in her data store.
*HtmlForms* can be automatically prefilled with RDF data to save Alice from repeatedly entering the same data.

Bob, a friend of Alice, wants to invite her for lunch and is searching for a suitable date.
He uses his Web application *BobForms* to generate a form description, configuring it to save the resulting RDF data to his data store.
Alice, who prefers command-line tools, receives a link to Bob's form description.
Using her command-line application *TextForms*, Alice accesses the form description, which is then rendered in a text-based format.
After completing the form, the data is sent as RDF data to Bob's data store.

Alice loves Bob's form and decides to adapt it to her own needs, effortlessly transitioning from an end-user to a form developer.
She opens the form description in *AliceForms* and modifies the RDF data model to suit her requirements.
She incorporates logic to ensure that any submission sends RDF data to her data store and notifies Bob's data store Inbox.
Furthermore, she configures a redirect to a custom page she has designed.
As a result, the form description now includes additional fields and logic tailored to Alice's specifications.
A sequence diagram of this example is included in [](#fig:interactions-motivating-example).

<figure id="fig:interactions-motivating-example">
<img src="img/sequence-diagram-motivating-example.svg" alt="[Sequence diagram showing the interactions in the motivating example]" />
<figcaption markdown="block">
The motivating example of Bob and Alice involves interactions between Alice, her data store, AliceForms, TextForms, BobForms, Bob, and his data store.
</figcaption>
</figure>

In a perfect world, Alice and Bob use a single form definition ontology.
However, many RDF data models describe the same type of data.
To be truly interoperable, applications such as *HtmlForms* and *TextForms* should contain some schema alignment capabilities to provide a translation between different form definition expressions.

In this paper, we examine the following three research questions (RQs) to address the issues raised by the above scenario.
We then further explain each RQ, comparing it to the current state of the art.
Each RQ's requirements are discussed, and summarized in [](#requirements-table).

- RQ1: How can form developers create forms to declaratively control machines for producing RDF in **multiple viewing environments** (e.g. Web pages vs text-based command line)?

- RQ2: How can machines **translate form descriptions** decoupled from the application into a vocabulary that the application understands?

- RQ3: How can machines **perform controllable and reusable actions** on the filled out data?


### Multiple Viewing Environments

To enable simple reusability, forms need declarative descriptions (R1).
This streamlines making adjustments by parsing, adjusting, and updating the description accordingly.
XForms 2.0 does this by declaratively specifying the form in XML.
In Solid-UI, forms are expressed using Linked Data in the Turtle format.

To allow machines interpreting the form and automatically prefill data, the declarative form description must be machine-interpretable (R2). 
Solid-UI's ontology semantically describes the elements' meanings, attaining machine interpretability.
XForms 2.0 allows containing semantics in the form description using vocabularies, making it possible for machines to interpret the form.
Additionally, the form description should be human-interpretable (R3) to manually fill out the form, a requirement that all state-of-the-art applications fulfil.

To allow Alice to choose the application in which she fills out the form, regardless of the environment, the form description must be renderable in multiple viewing environments (R4).
No current application offers this capability.


### Schema Alignment Tasks

To enable different applications to render the same form description, schema alignment is needed (R5) to decouple the application's vocabulary and the form description's vocabulary.
Currently, no state-of-the-art application supports this: XForms 2.0 only works with its own XForms vocabulary, formatted in XML and
Solid-UI Forms only works with its UI ontology.


### Footprint Tasks

A fully declarative form necessitates not only declarative descriptions for its elements, but also for the actions triggered by specific events.
Thus, it is crucial to have declarative policies (R6) that describe the actions to be taken, along with the execution of these footprint tasks (R7).
XForms 2.0 only allows specifying the submission endpoint using the Submission XML element, but no other policies can be specified.
Solid-UI Forms has only limited support to execute or specify any footprint tasks by the use of the extra layer [solid-ui-components](cite:cites zucker_solid_2023), currently under development.


### Requirements Summary

The scenario shows the need to [FAIRly](cite:cites wilkinson2016fair) describe the form description independent of the application context.[^FAIR]
The requirements of the previous scenario are grouped into three categories and summarized in [](#requirements-table).

[^FAIR]: The review of the adherence to the [FAIR principles](cite:cites wilkinson2016fair) can be found at the Wiki of the GitHub repository at [https://github.com/SolidLabResearch/FormGenerator/wiki/<wbr/>Adherence-to-the-FAIR-Principles](https://github.com/SolidLabResearch/FormGenerator/wiki/Adherence-to-the-FAIR-Principles).

<figure id="requirements-table" class="table" markdown="1">

| N° | Category                    | Requirement                                               |
|----|-----------------------------|-----------------------------------------------------------|
| R1 | Multiple View Environments  | Declarative description of the form                       |
| R2 | Multiple View Environments  | Machine-interpretable description                         |
| R3 | Multiple View Environments  | Human-interpretable description                           |
| R4 | Multiple View Environments  | Render one form description in multiple view environments |
| R5 | Schema Alignment Tasks      | Schema alignment execution                                |
| R6 | Footprint Tasks             | Declarative description of the policies                   |
| R7 | Footprint Tasks             | Footprint execution                                       |

<figcaption markdown="block">
Summarized requirements based on the research questions.
</figcaption>
</figure>
