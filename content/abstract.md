<span class="comment" data-author="RV">Since this is your first abstract that I'm reviewing, some context: I tend to go pretty hard on abstracts, under the rule that <q>you never get a second chance to make a first impression</q>. This is why I'm nitpicking a lot. I'll be less nitpicky about the rest of the paper.</span>

## Abstract
<!-- Context      -->
Forms are foundational building blocks in Web infrastructure,
which are common in cases such as surveys or when entering shipping details for online orders.
<span class="comment" data-author="RV">I'll need something stronger. Surveys is something we do once a year. We need a more fundamental argument.</span>
<ins class="comment" data-author="RV">Forms realize bidirectional communication on the Web, as they enable clients to send semi-structured information to servers.</ins>
Most of these Web forms are however rather static in the fields they contain,
they are redesigned for every different use case,
and tightly couple the data with the application.
<span class="comment" data-author="RV">So this is good as a first-level attempt at the problem space, but I need something stronger, i.e., a deeper problem. Forms being static is not an issue by itself. The underlying issue is / could be, that organizations often need multiple forms that are highly similar (is that what you mean? it could be something else), and that this currently requires implementing multiple forms. Tight coupling, that's always an argument we have to spell out, because the argument can be extended in different ways.</span>
<!-- Need         -->
To solve these problems,
there is a need <span class="comment" data-author="RV">explicitize who has that need</span> for a technique to create forms that are more *controllable*, *reusable*, and *decentralized*.
<span class="comment" data-author="RV">To me, this need does not follow directly from the previous sentence. Solving this will probably require both sentences to be tweaked for alignment.</span>
<!-- Task         -->
Hence, we introduce the *Declarative Form Description Pipeline* (DFDP) that meets these requirements.
DFDP achieves controllability through user-editable declarative form descriptions.
<span class="comment" data-author="RV">That by itself would not be novel, I think; I imagine that tools like Wordpress have this built in too?</span>
Reusability is achieved by separating form and action descriptions from the app.
<span class="comment" data-author="RV">This seems like a good thing, but it's hard to understand for the intended audience. I.e., it's something you understand if you already _know_ DFDP, but it does not help those new to it.</span>
Finally, decentralization is attained by decoupling the app from the storage by building on top of the Solid decentralization environment.
<span class="comment" data-author="RV">After reading this, I don't think decentralization was anyone's goal. Decentralization is a means to an end—what end are we aiming to achieve here?</span>
Concretely, DFDP employs a three-part view on Web Forms by decoupling a form description into the display, shape, and reasoning parts.
These parts declaratively define the form's elements, expected data structure, and how to handle filled-in information, to achieve the lacking features.
<!-- Object       -->
In this paper, we introduce and explain how such a declarative form description can be created and used without needing assumptions about the viewing environment or data storage.
<!-- Findings     -->
We show how this description contains all semantics
<span class="comment" data-author="RV">Is it a goal to <q>contain all semantics</q>, and what does that mean?</span>
by the use of a form, policy,
and rule ontology.
Furthermore, we prove how this approach solves the shortcomings of traditional Web forms.
<!-- Conclusion   -->
<del class="comment" data-author="RV">Our proposed pipeline allows forms to be controllable, to be reused, and data to be stored in a decentralized way.</del>
<span class="comment" data-author="RV">The previous sentence is repetition. Conclusions are to explain lessons learned: what does this mean to the audience, what can they now do that they couldn't?</span>
<del class="comment" data-author="RV">As such, DFDP empowers users to modify form descriptions, restoring their authority over the data.</del>
<span class="comment" data-author="RV">That wasn't a goal, was it?</span>
<!-- Perspectives -->
User study results provided insights to further improve usability by providing automatic suggestions based on field labels entered.
