## Introduction
{:#introduction}

Current web forms are meant to be used against one endpoint (1), often used for one (web) display (2), with one particular workflow in mind (3), without a means to send and receive the data in another way (4).
We all use a kind of web form once in a while, that is because you take part in a survey, or maybe because you have to fill in some kind of request. 
When one needs a similar form to one that already exists, they will have to develop a new application from scratch, without the possibility to start from that existing one and adapt it to their needs.
Furthermore, the data will almost always be stored on the server of the service provider, and the user will not be able to access it again or choose to store it somewhere else (footprint).

To tackle this problem, this paper introduces a solution by looking at Solid web forms as a whole of 3 separate parts: *display*, *validation*, and *reasoning*.
With the use of [Solid](cite:cites solid) and Linked Data, several solutions have already been proposed, but none of them consider web forms as a whole of 3 separate parts, except for the [Design Issue by Berners-Lee](cite:cites berners-lee_linked_2019) and the [blog post on *Shaping Linked Data apps* by Verborgh](cite:cites shapes).
In addition, to fully decouple the description from the application, schema alignment is required to map the description to the vocabulary of the application.
This makes it possible to use the same description for different applications, even if they use different vocabularies.
This, along with the execution of the footprint tasks, is done using reasoning.

Therefore, we propose an architecture that splits the Solid web forms into 3 parts and implements proof-of-concept applications to show how this can be done in practice.
In this paper, the following three research questions are examined:

- RQ1: How can machines be controlled in a declarative way to create forms for producing RDF in **multiple viewing environments** (such as the web and text-based via a command line)?

- RQ2: How can machines be controlled in a declarative way to perform **schema alignment and footprint tasks** by the use of reasoning?

- RQ3: How can an **abstraction** be made to **run reasoning** in the browser or remotely?


Bespreek XForms 2.0 en Solid-UI Forms toegepast op scenario en vermeld waar ze te kort schieten, bv voor schema alignment en hoe dit vertaald wordt in de requirements van deze paper.
{:.todo}

machine interpretable nodig zodat machines gebruikt kunnen worden om automatisch te prefillen met reeds bestaande data
human interpretable nodig zodat mensen de gerenderde form kunnen verstaan om zelf de verwachte informatie kunnen invullen in de form
declarative description zorgt ervoor dat het makkelijk te updaten is, je kunt gewoon de bestaande parsen, aanpassingen maken en de description accordingly updaten


<figure id="requirements" class="table" markdown="1">

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