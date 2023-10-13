## Requirements
{:#requirements}

Bespreek XForms 2.0 en Solid-UI Forms toegepast op scenario en vermeld waar ze te kort schieten, bv voor schema alignment en hoe dit vertaald wordt in de requirements van deze paper (link back naar N°).
{:.todo}

machine interpretable nodig zodat machines gebruikt kunnen worden om automatisch te prefillen met reeds bestaande data.
human interpretable nodig zodat mensen de gerenderde form kunnen verstaan om zelf de verwachte informatie kunnen invullen in de form.
declarative description zorgt ervoor dat het makkelijk te updaten is, je kunt gewoon de bestaande parsen, aanpassingen maken en de description accordingly updaten.
{:.todo}


In this section, we discuss the main requirements for decentralized and declarative forms on the Web.
We review the current state of the art and summarize what features are missing by examining some relevant use cases.

Suppose Alice goes to a Google Forms form, she can only use that form to save data to the Google Drive and nowhere else.
However, we want Alice to be able to choose for herself where to store the data, e.g. she might want to store it in her Solid pod, so she keeps ownership of the data she enters.
Next, as forms worldwide have display logic for humans, but not for machines, you still need a human being like Alice to interpret the fields in the form and to know which and how to fill in the fields.
Alice can thus not rely on a machine to help her fill in the form with data she for example already entered once before in her Solid pod.
However, it could make Alice's life way easier if it can tick the checkbox automatically saying she eats vegetarian while filling out a form to register for an event, based on what she specified once earlier in her own pod.
Moreover, if Bob sends Alice a form to fill out that he created using Google Forms, Alice has no choice but to use Google Forms to fill out the form, even if she prefers the interface of Microsoft Forms and would like to use that application. Perhaps Alice dislikes GUIs and wants to fill out the form using a text-based command-line interface, but she cannot do so because Bob has made a different choice that affects Alice's options.
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
XForms 2.0 does this by declaratively specifying the form in XML and Solid-UI Forms also succeeds in having a declarative form description by expressing the form using Linked Data in the Turtle format.

The declarative form description should both be machine interpretable (R2) such that machines can be used to interpret the form and automatically prefill data, and be human interpretable (R3) such that humans can still manually fill out the form.
The latter requirement is straightforward and all state-of-the-art applications like XForms 2.0 and Solid-UI Forms fulfill this.
Machine interpretability is achieved in Solid-UI Forms due to the use of Linked Data with the Solid-UI vocabulary semantically describing the meaning of the elements.
XForms 2.0 also allows containing semantics in the form description using vocabularies, making it possible for machines to interpret the form.
Other applications that are mostly used by the wide public nowadays like Google Forms and Microsoft Forms, however, do not allow you to contain semantics in the form. This makes them not machine interpretable.
Moreover, there are no declarative descriptions of the form available to the user.


### Schema Alignment Tasks



### Footprint Tasks



### Requirements Summary



<figure id="requirements-table" class="table" markdown="1">

| N° | Category                       | Requirement                                                            |
|----|--------------------------------|------------------------------------------------------------------------|
| R1 | Multiple Viewing Environments  | Declarative description of the form                                    |
| R2 |                                | Machine interpretable description                                      |
| R3 |                                | Human interpretable description                                        |
| R4 |                                | Same form description can be rendered in multiple viewing environments |
| R5 | Schema Alignment and Footprint | Declarative description of the policies                                |
| R6 |                                | Schema alignment execution                                             |
| R7 |                                | Footprint execution                                                    |
| R8 | Uniform Reasoner Interface     | [Data, query, options] part of interface                               |
| R9 |                                | Easily switchable between implementations                              |

<figcaption markdown="block">
Summarized requirements based on the research questions.
</figcaption>
</figure>