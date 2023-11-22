## Motivation and Requirements
{:#requirements}

In this section, we discuss the main requirements for decentralized and declarative forms on the Web using a use case involving two personas, "Alice" and "Bob", each with their own objectives about the forms they like to publish, but both requiring full control over where and how the resulting RDF is stored.

Alice, a Web-savvy user, owns a Solid pod she wants to fill with RDF data.
She uses her favorite Web app *AliceForms* to create a form description she will use to produce RDF.
*AliceForms* resembles Google Forms: the app allows creating forms in a user-friendly way with a limited data model but provides Alice the freedom where to publish the form description and the RDF data it produces, so she can keep ownership of the data she enters (in Google Forms this is all centralized).
Alice chooses to store her form description and the produced RDF data on her own Solid pod.

When Alice wants to create RDF data, she opens the form description in a renderer app *HtmlForms* providing her with an HTML rendered version of the form description.
When Alice fills out all the fields, the RDF data will be stored on her Solid pod.
The *HtmlForms* app can be automatically pre-filled with RDF data to save Alice from repeatedly entering the same data.

Bob, a friend of Alice, wants to invite her for lunch and tries to find an appropriate date.
Bob uses his own Web app *BobForms* to create a form description he will send to Alice.
Bob configures the form description to send the resulting RDF data to his own Solid pod.
Alice receives a link to Bob's form description and prefers command-line tools to perform tasks with low cognitive load.
She uses her command-line app *TextForms* to open the form description.
*TextForms* creates a text-based rendering of Bob's form description.
She fills out the form and as a result the data as RDF data is sent to Bob's pod.

Alice likes Bob's form and wants to use it for her own use case.
She opens the form description in her *AliceForms* and edits the RDF data model.
She also adds logic that any submission should send RDF data to her own Solid pod and to the LDN Inbox of Bob's pod as a notification.
On top of that, she configures a redirect to a page she created.
Now the form description contains extra fields and logic.

In a perfect world, Alice and Bob can use a single ontology that describes the RDF data model and the form definitions.
However, many RDF data models describing the same type of data can exist.
For instance, dates and titles can be expressed using many vocabularies.
To be truly declarative, applications such as *HtmlForms* and *TextForms* should contain some schema alignment capabilities to provide a translation between differences in expressing a data model and form definition.

In this paper, we examine the following three research questions to address the issues raised by the above scenario.
In the remainder of this section, each research question will be further explained and compared to the current state of the art.
The requirements for each research question are discussed, and finally the summarized requirements are presented in [](#requirements-table).

- RQ1: How can machines be controlled in a declarative way to create forms for producing RDF in **multiple viewing environments** (such as the Web and text-based via a command line)?

- RQ2: How can machines be controlled in a declarative way to **translate form descriptions** decoupled from the application into a vocabulary that the application understands?

- RQ3: How can machines be controlled in a declarative way to **perform actions** on the filled out data?


### Multiple Viewing Environments

Forms should have declarative descriptions (R1) to enable simple reusability.
This streamlines the process of making some adjustments by parsing, adjusting and updating the description accordingly.
XForms 2.0 does this by declaratively specifying the form in XML.
Solid-UI Forms also succeeds in (R1) by expressing the form using Linked Data in the Turtle format.

The declarative form description should be machine-interpretable (R2), allowing machines to interpret the form and automatically prefill data. 
Additionally, it should be human-interpretable (R3) so that humans can manually fill out the form.
This requirement is straightforward, and all state-of-the-art applications, such as XForms 2.0 and Solid-UI Forms, fulfill it.
Machine interpretability is attained in Solid-UI Forms because Linked Data is used with the Solid-UI vocabulary, which semantically describes the elements' meanings.
XForms 2.0 also allows containing semantics in the form description using vocabularies, making it possible for machines to interpret the form.
Other applications that are mostly used by the wide public nowadays like Google Forms and Microsoft Forms, however, do not allow the user to contain semantics in the form. This makes them not machine-interpretable.
Moreover, there are no declarative descriptions of the form available to the user.

To give Alice the possibility to choose the application she wants to fill out the form, independent of the environment, the form description should be renderable in multiple viewing environments (R4).
Even though it might already be technically possible, no state-of-the-art application offers the ability yet to fill out the form in two or more different viewing environments.


### Schema Alignment Tasks

To make the concept of using multiple different applications to render the same form description work in practice, schema alignment is needed (R5) to create an independence between the vocabulary used by the application and the vocabulary used by the form description.
No state-of-the-art application supports this. XForms 2.0 only works with its own XForms vocabulary and is formatted in XML.
Similarly, Solid-UI Forms only works with its Solid-UI vocabulary.


### Footprint Tasks

To ensure that the form is entirely declarative, it is essential to provide declarative descriptions not only for the form's elements but also for the actions triggered by certain events.
Therefore, a declarative description of the policies (R6) together with the execution of these footprint tasks (R7) is required.
XForms 2.0 only allows specifying the submission endpoint using the Submission XML element, but no other policies can be specified.
Solid-UI Forms has only limited support to execute or specify any footprint tasks by the use of the extra layer [solid-ui-components](cite:cites zucker_solid_2023) currently being developed by Jeff Zucker.


### Requirements Summary

<figure id="requirements-table" class="table" markdown="1">

| N° | Category                       | Requirement                                                            |
|----|--------------------------------|------------------------------------------------------------------------|
| R1 | Multiple Viewing Environments  | Declarative description of the form                                    |
| R2 |                                | Machine-interpretable description                                      |
| R3 |                                | Human-interpretable description                                        |
| R4 |                                | Same form description can be rendered in multiple viewing environments |
| R5 | Schema Alignment Tasks         | Schema alignment execution                                             |
| R6 | Footprint Tasks                | Declarative description of the policies                                |
| R7 |                                | Footprint execution                                                    |

<figcaption markdown="block">
Summarized requirements based on the research questions.
</figcaption>
</figure>

The scenario shows the need to FAIRly describe the form description independent of the application context. [^FAIR]
The requirements of the previous scenario are grouped into three categories and summarized in [](#requirements-table).

[^FAIR]: The review of the adherence to the [FAIR principles](cite:cites wilkinson2016fair) can be found at the Wiki of the GitHub repository at [https://github.com/SolidLabResearch/FormGenerator/wiki/<wbr/>Adherence-to-the-FAIR-Principles](https://github.com/SolidLabResearch/FormGenerator/wiki/Adherence-to-the-FAIR-Principles).
