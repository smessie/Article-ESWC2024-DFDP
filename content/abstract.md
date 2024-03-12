## Abstract
<!-- Context      -->
Forms are key to bidirectional communication on the Web: without them, end-users would be unable to place online orders or file support tickets.
Organizations often need multiple, highly similar forms, which currently requires multiple implementations.
Moreover, the data is tightly coupled to the application, restricting the user from reusing it with other applications, or storing the data somewhere else.
<!-- Need         -->
Organizations and end-users have a need for a technique to create forms that are more *controllable*, *reusable*, and *decentralized*.
<!-- Task         -->
To address this problem, we introduce the *Declarative Form Description Pipeline* (DFDP) that meets these requirements.
DFDP achieves controllability through by end-users editable declarative form descriptions.
Reusability is ensured through separate descriptions of the form fields and associated actions.
Finally, by leveraging a decentralized environment like Solid, the application is decoupled from the storage, preserving end-user's control over their data.
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without assumptions about the viewing environment or data storage.
<!-- Findings     -->
We show how separate applications can independently work together and be interchanged by using a description containing all semantics by the use of a form, policy, and rule ontology.
Furthermore, we prove how this approach solves the shortcomings of traditional Web forms.
<!-- Conclusion   -->
Our proposed pipeline enables organizations to save time by building similar forms without starting from scratch.
Similarly, end-users can save time by letting machines prefill the form with existing data.
Additionally, DFDP empowers end-users to be in control of the application they use to fill out forms and the data they enter.
<!-- Perspectives -->
User study results provide insights to further improve usability by providing automatic suggestions based on field labels entered.
