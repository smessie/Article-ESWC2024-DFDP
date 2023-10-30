## Requirements
{:#requirements}

In this section, we discuss the main requirements for decentralized and declarative forms on the Web.
We review the current state of the art and summarize what features are missing by examining some relevant use cases.

Suppose Alice goes to a Google Forms form, she can only use that form to save data to the Google Drive and nowhere else.
However, we want Alice to be able to choose for herself where to store the data, e.g. she might want to store it in her Solid pod, so she keeps ownership of the data she enters.
Next, as forms worldwide have display logic for humans, but not for machines, you still need a human being like Alice to interpret the fields and to know how to fill them in.
However, it could make Alice's life way easier if it can tick the checkbox automatically saying she eats vegetarian while filling out a form to register for an event, if she specified that earlier in her own pod.
Moreover, if Bob sends Alice a form to fill out that he created using Google Forms, Alice has no choice but to use Google Forms to fill out the form, even if she prefers the interface of e.g. Microsoft Forms and would like to use that application.
Perhaps Alice dislikes GUIs and wants to fill out the form using a text-based command-line interface, but she cannot do so because Bob has made a different choice that affects Alice's options.
In addition, Bob may have created a form that Alice is very interested in.
She wants to reuse it for another workflow, but she needs to tweak the form a bit to fit her needs.
Now she is lost because she cannot get the form description to do this.
Any information about the data model, the display model, and the reasoning is now all centralized at Google, and it is impossible to reuse this form with a different application.

In this paper, we examine the following three research questions to address the issues raised by the above scenario.
In the remainder of this section, each research question will be further explained and compared to the current state of the art.
The requirements for each research question are discussed, and finally the summarized requirements are presented in [](#requirements-table).

- RQ1: How can machines be controlled in a declarative way to create forms for producing RDF in **multiple viewing environments** (such as the web and text-based via a command line)?

- RQ2: How can machines be controlled in a declarative way to **translate form descriptions** decoupled from the application into a vocabulary that the application understands?

- RQ3: How can machines be controlled in a declarative way to **perform actions** on the filled out data?


### Multiple Viewing Environments

Forms should have declarative descriptions (R1) to enable simple reusability.
This streamlines the process of making some adjustments, as you can parse the existing one, make the adjustments, and update the description accordingly.
XForms 2.0 does this by declaratively specifying the form in XML.
Solid-UI Forms also succeeds in having a declarative form description by expressing the form using Linked Data in the Turtle format.

The declarative form description should be machine-interpretable (R2), allowing machines to interpret the form and automatically prefill data. 
Additionally, it should be human-interpretable (R3) so that humans can manually fill out the form.
This requirement is straightforward, and all state-of-the-art applications, such as XForms 2.0 and Solid-UI Forms, fulfill it.
Machine interpretability is attained in Solid-UI Forms because Linked Data is used with the Solid-UI vocabulary, which semantically describes the elements' meanings.
XForms 2.0 also allows containing semantics in the form description using vocabularies, making it possible for machines to interpret the form.
Other applications that are mostly used by the wide public nowadays like Google Forms and Microsoft Forms, however, do not allow you to contain semantics in the form. This makes them not machine-interpretable.
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
Solid-UI Forms cannot execute or specify any footprint tasks.


### Requirements Summary

The scenario shows the need to FAIRly describe the form description independent of the application context.
The review of the adherence to the [FAIR principles](cite:cites wilkinson2016fair) can be found at the Wiki of the GitHub repository at [https://github.com/SolidLabResearch/FormGenerator/wiki/Adherence-to-the-FAIR-Principles](https://github.com/SolidLabResearch/FormGenerator/wiki/Adherence-to-the-FAIR-Principles).
The requirements of the previous scenario are grouped into three categories and summarized in [](#requirements-table).


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