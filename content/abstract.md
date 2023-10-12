## Abstract
<!-- Context      -->
Web forms are used all the time <span class="comment" data-author="RT">Let's give a concrete example of such a form.</span>,
<!-- Need         -->
but they lack basic, yet important, features such as controllability, reusability, and decentralization.
With traditional centralized forms, we cannot decide where to store the submitted data, and we cannot reuse existing forms <span class="comment" data-author="RT">Devil's advocate: Is the reuse really a problem? I guess with Google Forms for example one could reuse forms?</span>.
<!-- Task         -->
To solve this, we need to describe the form and its actions <span class="comment" data-author="RT">I don't see why this is a solution to the centralization problem. Instead, I feel like in order to decentralize, we need to decouple app from storage. The declarative form description feels like something else, that probably needs another line of argumentation.</span>, i.e. what to do with the submitted data, independently of the app, so that we can edit and copy this description.
We created a three-part view on Solid <span class="comment" data-author="RT">Solid has not been mentioned before yet. When argumenting decentralization, say you'll focus on the Solid environment.</span> Web Forms by decoupling a form description into the display, validation, and reasoning parts <span class="comment" data-author="RT">For the reader, it's not clear why you need these 3 parts. Make sure to emphasize this clearly.</span>.
<!-- Object       -->
In this paper, we demonstrate <span class="comment" data-author="RT">This is not a demo paper, but a resources paper. As such, the article doesn't have demonstration at its core, but instead, the article should introduce and explain a system/resource.</span> how such a declarative form description can be created and used without making assumptions about the viewing environment or data storage.
<!-- Findings     -->
The first results of this paper are promising.<span class="comment" data-author="RT">Instead of saying they are promising, just summarize the results</span>
<!-- Conclusion   -->
<span class="comment" data-author="RT">I feel like you've made the point in the next sentence before already.</span>
Using a declarative form description, we can render a form with our favorite renderer application in any viewing environment and perform the actions described in the form description using reasoning.
This decoupling allows us to reuse forms and store data in a decentralized way.
By enabling users to modify form descriptions, we reinstate their authority over the data.
<!-- Perspectives -->
Further research <span class="comment" data-author="RT">Such as?</span> will have to show how further abstractions may push the need for Linked Data knowledge even further aside.
