## Abstract
<!-- Context      -->
Web forms are used all the time, e.g. when taking part in a survey or when filling in your shipping details while placing an order online.
<!-- Need         -->
However, they lack basic, yet important, features such as controllability, reusability, and decentralization.
With traditional centralized forms, users cannot decide where to store the submitted data, and they cannot reuse existing forms they initially did not make themselves or were made using another application.
<!-- Task         -->
To achieve reusability, we need to describe the form and its actions, i.e. what to do with the submitted data, independently of the app, so that we can edit and copy this description.
To achieve decentralization, we need to decouple the app from the storage, for which we will focus on the Solid environment.
By allowing one to easily change the location of that storage location in the declarative form description, we achieve controllability.
We created a three-part view on Solid Web Forms by decoupling a form description into the display, shape, and reasoning parts. These parts declaratively define how the form should look element-wise, the expected data structure, and how to handle filled-in information to achieve the desired features.
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without making assumptions about the viewing environment or data storage.
<!-- Findings     -->
The first results of this paper show how this description contains all semantics by the use of a form, policy
and rule ontology.
Schema alignment tasks translate a description from one ontology to another, decoupling it from the used app.
Footprint tasks resolve the remaining issues where schema alignment tasks fall short and execute policies in response to declaratively defined events.
<!-- Conclusion   -->
This decoupling allows us to reuse forms and store data in a decentralized way.
Thanks to the machine-readability as a direct result of the contained semantics in RDF, that form can now automatically be prefilled with pre-existing data.
By enabling users to modify form descriptions, we reinstate their authority over the data.
<!-- Perspectives -->
Further research such as automatically suggesting bindings (i.e. the link between a form element and its semantic description) based on user-input will have to show how further abstractions may push the need for Linked Data knowledge even further aside.
