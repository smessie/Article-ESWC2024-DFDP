## Requirements
{:#requirements}

Bespreek XForms 2.0 en Solid-UI Forms toegepast op scenario en vermeld waar ze te kort schieten, bv voor schema alignment en hoe dit vertaald wordt in de requirements van deze paper (link back naar N°).
{:.todo}

machine interpretable nodig zodat machines gebruikt kunnen worden om automatisch te prefillen met reeds bestaande data.
human interpretable nodig zodat mensen de gerenderde form kunnen verstaan om zelf de verwachte informatie kunnen invullen in de form.
declarative description zorgt ervoor dat het makkelijk te updaten is, je kunt gewoon de bestaande parsen, aanpassingen maken en de description accordingly updaten.
{:.todo}

Therefore, we propose an architecture that splits the Solid web forms into 3 parts and implements proof-of-concept applications to show how this can be done in practice.
<span class="comment" data-author="RT">Not sure if this is the right place to introduce RQs. Might be better to do that after related work, right before you dive into the details of your approach.</span>
In this paper, the following two research questions are examined:

- RQ1: How can machines be controlled in a declarative way to create forms for producing RDF in **multiple viewing environments** (such as the web and text-based via a command line)?

- RQ2: How can machines be controlled in a declarative way to **translate form descriptions** decoupled from the application into a vocabulary that the application understands?

- RQ3: How can machines be controlled in a declarative way to **perform actions** on the filled out data?

<span class="comment" data-author="RT">Is there no decoupling of storage and app requirement?</span>

Refer to different upcoming sections in paper
{:.todo}


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