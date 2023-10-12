## Abstract
<!-- Context      -->
Web forms are used all the time, e.g. when taking part in a survey using Google Forms, Microsoft Forms, SurveyMonkey or any other alternative, or when filling in your shipping details while placing an order online.
<!-- Need         -->
However, they lack basic, yet important, features such as controllability, reusability, and decentralization.
With traditional centralized forms, we cannot decide where to store the submitted data, and we cannot reuse existing forms we initially did not make ourselves or were made using another application.
<!-- Task         -->
To achieve reusability, we need to describe the form and its actions, i.e. what to do with the submitted data, independently of the app, so that we can edit and copy this description.
To achieve decentralization, we need to decouple the app from the storage, for which we will focus on the Solid environment.
By allowing one to easily change the location of that storage location in the declarative form description, we achieve controllability.
We created a three-part view on Solid Web Forms by decoupling a form description into the display, validation, and reasoning parts. These parts declaratively define how the form should look element-wise, what the expected structure of the data is, and what to do with the filled in data; all together resulting in fulfilling the lacking features.
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without making assumptions about the viewing environment or data storage.
<!-- Findings     -->
The first results of this paper show how this declarative form description contains all semantics by the use of a form ontology like Solid-UI, a policy ontology like FnO and a rule ontology like N3.
Schema alignment tasks allow for translating a description from one ontology to another, decoupling it from the used app.
Footprint tasks resolve the remaining issues where schema alignment tasks fall short and execute policies in result to declaratively defined events.
<!-- Conclusion   -->
This decoupling allows us to reuse forms and store data in a decentralized way.
Thanks to the machine-readability as a direct result of the contained semantics in the RDF declaratively describing the form, that form can now automatically be prefilled with pre-existing data.
By enabling users to modify form descriptions, we reinstate their authority over the data.
<!-- Perspectives -->
Further research such as automatically suggesting bindings (i.e. the link between a form element and its semantic description) based on user-input will have to show how further abstractions may push the need for Linked Data knowledge even further aside.
