## Abstract
<!-- Context      -->
Forms are key to bidirectional communication on the Web: without them, end-users would be unable to place online orders or file support tickets.
Organizations often need multiple, highly similar forms, currently necessitating implementing multiple ones.
Moreover, the data is tightly coupled to the app, restricting the user from reusing it with other apps or storing the data somewhere else.
<!-- Need         -->
To solve these problems, organizations that seek efficiency and end-users who desire control over their data have a need for a technique to create forms that are more *controllable*, *reusable*, and *decentralized*.
<!-- Task         -->
Hence, we introduce the *Declarative Form Description Pipeline* (DFDP) that meets these requirements.
DFDP achieves controllability through declarative form descriptions that are editable by end-users filling out the form.
Reusability is achieved by the app using a separate description of the fields contained in the form and the actions to be performed on events such as submission.
Finally, the end-user retains ownership of their data by decoupling the app from the storage by building on top of the Solid decentralization environment.
Concretely, DFDP employs a three-part view on Web Forms by decoupling a form description into the display, shape, and reasoning parts.
These parts declaratively define the form's elements, expected data structure, and how to handle filled-in information, to achieve the lacking features.
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without needing assumptions about the viewing environment or data storage.
<!-- Findings     -->
We show how separate apps can independently work together and be interchanged by using a description containing all semantics by the use of a form, policy, and rule ontology.
Furthermore, we prove how this approach solves the shortcomings of traditional Web forms.
<!-- Conclusion   -->
Our proposed pipeline enables organizations to save time by building similar forms without starting from scratch.
Similarly, end-users can save time by letting machines prefill the form with existing data.
Additionally, DFDP empowers end-users to be in control of the app they use to fill out forms and the data they enter.
<!-- Perspectives -->
User study results provide insights to further improve usability by providing automatic suggestions based on field labels entered.

<span class="comment" data-author="RT">The abstract is in really good shape now, I like it! It's just a bit on the long side, so you could consider shortening it a bit more (e.g. the Task), but I don't think this is crucial.</span>