## Abstract
<!-- Context      -->
Forms are key to bidirectional communication on the Web: without them, end-users would be unable to place online orders or file support tickets.
Organizations often need multiple, highly similar forms, which currently requires multiple implementations.
<span class="comment" data-author="BE">
requires -> require
</span>
Moreover, the data is tightly coupled to the application, restricting the user from reusing it with other applications, or storing the data somewhere else.
<span class="comment" data-author="BE">
Not clear which kind of users are being restricted -- is it just the end-users, organisations, both?
</span>
<!-- Need         -->
Organizations and end-users have a need for a technique to create forms that are more *controllable*, *reusable*, and *decentralized*.
<!-- Task         -->
To address this problem, we introduce the *Declarative Form Description Pipeline* (DFDP) that meets these requirements.
DFDP achieves controllability through by end-users editable declarative form descriptions.
<span class="comment" data-author="BE">
controllability through by end-users editable -- "by" not needed & should be "end-users' editable"
</span>
Reusability is ensured through separate descriptions of the form fields and associated actions.
Finally, by leveraging a decentralized environment like Solid, the application is decoupled from the storage, preserving end-user's control over their data.
<span class="comment" data-author="BE">
end-user's control -> end-users control
</span>
<span class="comment" data-author="BE">
The need you identify is for both organisations and end-users, however I only see end-users mentioned in the task section of the abstract. Is it the case that non of tasks were for the benefit of organisations?
</span>
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without assumptions about the viewing environment or data storage.
<!-- Findings     -->
We show how separate applications can independently work together and be interchanged by using a description containing all semantics by the use of a form, policy, and rule ontology.
<span class="comment" data-author="BE">
Not clear what you mean by "containing all semantics" -- is it an ontology that has form, policy and rule concepts or do you mean something else? The sentence could be mane more clear
</span>
Furthermore, we prove how this approach solves the shortcomings of traditional Web forms.
<!-- Conclusion   -->
Our proposed pipeline enables organizations to save time by building similar forms without starting from scratch.
Similarly, end-users can save time by letting machines prefill the form with existing data.
Additionally, DFDP empowers end-users to be in control of the application they use to fill out forms and the data they enter.
<!-- Perspectives -->
User study results provide insights to further improve usability by providing automatic suggestions based on field labels entered.
<span class="comment" data-author="BE">
This comment is maybe for later after you refactor the whole paper -- how does the work here connect with the specific topics of the DMKG workshop?
I think it will be just a matter of tweaking some words to adapt it to the data management domain which is the core aspect of the workshop.
</span>