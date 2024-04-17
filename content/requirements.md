## Motivation and Requirements
{:#requirements}

In this section, we discuss the main requirements for decentralized and declarative Web forms using a use case involving two personas, "Alice" and "Bob", each with their own objectives about the forms they like to publish, but both requiring full control over where and how the resulting RDF is stored.

Alice, a Web-savvy user, owns a personal data store for storing RDF data.
Her motivations for doing so can be manifold.
For instance, she may be a researcher seeking to include a list of her publications within her personal data store as an integral part of her curriculum vitae (CV).
In many cases, companies request CVs without providing a tailored form for their creation.
Rather than relying on a pre-existing CV application with a fixed data structure, Alice prefers to use her AliceForms.
This allows her to employ an existing CV data model while also incorporating her own metadata.
Consequently, companies will retrieve more rich data.

To populate her data store, she thus uses *AliceForms*, her preferred Web application, which shares similarities with Google Forms.
*AliceForms* enables the creation of forms in a user-friendly manner with a simplified data model.
Importantly, Alice retains control over where the form description and resulting RDF data are published, ensuring control over the data she enters - an option not available in centralized platforms like Google Forms.

When Alice wants to create RDF data, she opens the form description in a renderer application *HtmlForms* providing her with an HTML rendered version of the form description.
When Alice fills out all the fields, the RDF data will be stored in her data store.
The *HtmlForms* application can be automatically pre-filled with RDF data to save Alice from repeatedly entering the same data.

Bob, a friend of Alice, wants to invite her for lunch and is searching for a suitable date.
He uses his Web application *BobForms* to generate a form description, configuring it to save the resulting RDF data to his data store.
Alice, who prefers command-line tools, receives a link to Bob's form description.
Using her command-line application *TextForms*, Alice accesses the form description, which is then rendered in a text-based format.
After completing the form, the data is sent as RDF data to Bob's data store.

Alice loves Bob's form and decides to adapt it to her own needs, transitioning from an end-user to a form developer effortlessly.
She opens the form description in *AliceForms* and modifies the RDF data model to suit her requirements.
In addition, she incorporates logic to ensure that any submission sends RDF data to her personal data store and notifies Bob's data store Inbox.
Furthermore, she configures a redirect to a custom page she has designed.
As a result, the form description now includes additional fields and logic tailored to Alice's specifications.
A sequence diagram of this example is included in [](#fig:interactions-motivating-example) to model the interactions taking place.

<figure id="fig:interactions-motivating-example">
<img src="img/sequence-diagram-motivating-example.svg" alt="[Sequence diagram showing the interactions in the motivating example]" />
<figcaption markdown="block">
The motivating example of Bob and Alice involves interactions between Alice, her data store, AliceForms, TextForms, BobForms, Bob, and his data store.
</figcaption>
</figure>

In a perfect world, Alice and Bob can use a single ontology that describes the form definitions.
However, many RDF data models describing the same type of data can exist.
To be truly interoperable, applications such as *HtmlForms* and *TextForms* should contain some schema alignment capabilities to provide a translation between differences in expressing a form definition.

In this paper, we examine the following three research questions to address the issues raised by the above scenario.
In the remainder of this section, each research question will be further explained and compared to the current state of the art.
The requirements for each research question are discussed, and finally the summarized requirements are presented in [](#requirements-table).

- RQ1: How can form developers create forms to declaratively control machines for producing RDF in **multiple viewing environments** (such as Web pages and text-based via a command line)?

- RQ2: How can machines **translate form descriptions** decoupled from the application into a vocabulary that the application understands?

- RQ3: How can machines **perform controllable and reusable actions** on the filled out data?


### Multiple Viewing Environments

Forms should have declarative descriptions (R1) to enable simple reusability.
This streamlines the process of making some adjustments by parsing, adjusting, and updating the description accordingly.
XForms 2.0 does this by declaratively specifying the form in XML.
Solid-UI Forms also succeeds in (R1) by expressing the form using Linked Data in the Turtle format.

The declarative form description should be machine-interpretable (R2), allowing machines to interpret the form and automatically prefill data. 
Additionally, it should be human-interpretable (R3) so that humans can manually fill out the form, which of course all state-of-the-art applications fulfill.
Machine interpretability is attained in Solid-UI Forms because Linked Data is used with the UI ontology, which semantically describes the elements' meanings.
XForms 2.0 also allows containing semantics in the form description using vocabularies, making it possible for machines to interpret the form.

To allow Alice to choose the application in which she fills out the form, regardless of the environment, the form description should be renderable in multiple viewing environments (R4).
Although it may already be technically feasible, no current application offers this capability to fill out the form in different viewing environments.


### Schema Alignment Tasks

To enable different applications to render the same form description, schema alignment (R5) is required to create independence between the application's vocabulary and the form description's vocabulary.
Currently, no state-of-the-art application supports this. XForms 2.0 only works with its own XForms vocabulary and is formatted in XML.
Similarly, Solid-UI Forms only works with its UI ontology.


### Footprint Tasks

Ensuring full declarativity in the form necessitates not only declarative descriptions for its elements but also for the actions triggered by specific events.
Thus, it is crucial to have declarative policies (R6) that describe the actions to be taken, along with the execution of these footprint tasks (R7).
XForms 2.0 only allows specifying the submission endpoint using the Submission XML element, but no other policies can be specified.
Solid-UI Forms has only limited support to execute or specify any footprint tasks by the use of the extra layer [solid-ui-components](cite:cites zucker_solid_2023) currently under development.


### Requirements Summary

The scenario shows the need to [FAIRly](cite:cites wilkinson2016fair) describe the form description independent of the application context.[^FAIR]
The requirements of the previous scenario are grouped into three categories and summarized in [](#requirements-table).

[^FAIR]: The review of the adherence to the [FAIR principles](cite:cites wilkinson2016fair) can be found at the Wiki of the GitHub repository at [https://github.com/SolidLabResearch/FormGenerator/wiki/<wbr/>Adherence-to-the-FAIR-Principles](https://github.com/SolidLabResearch/FormGenerator/wiki/Adherence-to-the-FAIR-Principles).

<figure id="requirements-table" class="table" markdown="1">

| N° | Category                       | Requirement                                                                |
|----|--------------------------------|----------------------------------------------------------------------------|
| R1 | Multiple Viewing Environments  | Declarative description of the form                                        |
| R2 | Multiple Viewing Environments  | Machine-interpretable description                                          |
| R3 | Multiple Viewing Environments  | Human-interpretable description                                            |
| R4 | Multiple Viewing Environments  | Same form description can be rendered in <br>multiple viewing environments |
| R5 | Schema Alignment Tasks         | Schema alignment execution                                                 |
| R6 | Footprint Tasks                | Declarative description of the policies                                    |
| R7 | Footprint Tasks                | Footprint execution                                                        |

<figcaption markdown="block">
Summarized requirements based on the research questions.
</figcaption>
</figure>
