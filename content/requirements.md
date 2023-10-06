## Requirements
{:#requirements}

Bespreek XForms 2.0 en Solid-UI Forms toegepast op scenario en vermeld waar ze te kort schieten, bv voor schema alignment en hoe dit vertaald wordt in de requirements van deze paper.
{:.todo}

machine interpretable nodig zodat machines gebruikt kunnen worden om automatisch te prefillen met reeds bestaande data
human interpretable nodig zodat mensen de gerenderde form kunnen verstaan om zelf de verwachte informatie kunnen invullen in de form
declarative description zorgt ervoor dat het makkelijk te updaten is, je kunt gewoon de bestaande parsen, aanpassingen maken en de description accordingly updaten


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