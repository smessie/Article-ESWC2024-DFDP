## Abstract
<!-- Context      -->
Forms are foundational building blocks in Web infrastructure,
which are common in cases such as surveys or when entering shipping details for online orders.
Most of these Web forms are however rather static in the fields they contain,
they are redesigned for every different use case,
and tightly couple the data with the application.
<!-- Need         -->
To solve these problems,
there is a need for a technique to create forms that are more *controllable*, *reusable*, and *decentralized*.
<!-- Task         -->
Hence, in this work we introduce the *Declarative Form Description Pipeline* (DFDP) that meets these requirements.
DFDP achieves controllability through user-editable declarative form descriptions.
Reusability is achieved by separating form and action descriptions from the app.
Finally, decentralization is attained by decoupling the app from the storage by building on top of the Solid decentralization environment.
Concretely, DFDP employs a three-part view on Web Forms by decoupling a form description into the display, shape, and reasoning parts.
These parts declaratively define the form's elements, expected data structure, and how to handle filled-in information, to achieve the lacking features.
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without making assumptions about the viewing environment or data storage.
<!-- Findings     -->
We show how this description contains all semantics by the use of a form, policy
and rule ontology.
Furthermore, we prove how our approach solves the shortcomings of traditional Web forms.
<!-- Conclusion   -->
Our proposed pipeline allows forms to be controllable, to be reused, and data to be stored in a decentralized way.
<span class="comment" data-author="RT">The next sentence feels a bit out of place. Maybe we can remove it from the abstract?</span>
Forms can be pre-filled with existing data thanks to the machine readability provided by the semantics contained in RDF.
As such, DFDP empowers users to modify form descriptions, restoring their authority over the data.
<!-- Perspectives -->
<span class="comment" data-author="RT">Not sure I understand the next sentence. But perhaps the previous one is a good one to end on.</span>
Further research on auto-suggesting bindings based on user input should clarify the impact on Linked Data knowledge requirements.
