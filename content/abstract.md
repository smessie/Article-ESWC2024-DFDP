## Abstract
<!-- Context      -->
Web forms are commonly used, such as in surveys or when entering shipping details for online orders.
<!-- Need         -->
However, they lack basic, yet important, features such as controllability, reusability, and decentralization.
Traditional centralized forms lack data reuse across apps and user control over storage location.
<!-- Task         -->
Reusability necessitates form and action descriptions independently of the app.
Similarly, decentralization requires decoupling the app from the storage, for which we will focus on Solid.
We achieve controllability by user-editable declarative form descriptions.
We create a three-part view on Solid Web Forms by decoupling a form description into the display, shape, and reasoning parts.
These parts declaratively define the form's elements, expected data structure, and how to handle filled-in information, to achieve the lacking features.
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without making assumptions about the viewing environment or data storage.
<!-- Findings     -->
We show how this description contains all semantics by the use of a form, policy
and rule ontology.
We show how the introduced declarative description, schema alignment tasks and footprint tasks solves the shortcomings of nowadays Web forms.
<!-- Conclusion   -->
The decoupling allows us to reuse forms and store data in a decentralized way.
The form can now be prefilled with existing data thanks to the machine readability provided by the semantics contained in RDF.
We empowered users to modify form descriptions, restoring their authority over the data.
<!-- Perspectives -->
Further research on auto-suggesting bindings based on user input should clarify the impact on Linked Data knowledge requirements.
