## Abstract
Web forms are used all the time, but they lack basic, yet important, features such as controllability, reusability, and decentralization.
With traditional centralized forms, we cannot decide where to store the submitted data, and we cannot reuse existing forms.
To solve this, we need to describe the form and its actions, i.e. what to do with the submitted data, independently of the app, so that we can edit and copy this description.
We created a three-part view on Solid Web Forms by decoupling a form description into the display, validation, and reasoning parts.
In this paper, we demonstrate how such a declarative form description can be created and used without making assumptions about the viewing environment or data storage.
Using a declaratively written form description, we can render a form with our favorite renderer application in any viewing environment and perform the actions described in the form description using reasoning.
This decoupling allows us to reuse forms and store data in a decentralized way.
By enabling users to modify form descriptions, we reinstate their authority over the data.
The first results of this paper are promising. Further research will have to show how further abstractions may push the need for Linked Data knowledge even further aside.
