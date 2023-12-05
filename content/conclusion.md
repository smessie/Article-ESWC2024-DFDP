## Conclusion
{:#conclusion}

In this article, we introduced decoupled Web forms considered as three parts by creating a Declarative Form Description Pipeline (DFDP).
The implementations of the FormRenderer and FormCli prove that the display part is loosely coupled to the rendering environment.
The FormGenerator shows how such declarative form descriptions can be produced.

The introduced schema alignment and footprint tasks allows users to use different vocabularies than the app understands and allows them to execute declaratively defined policies on the occurrence of events.
The introduced FormRenderer is <del class="comment" data-author="RV">thereby the first system</del> <span class="comment" data-author="RV">that's not really relevant</span> that makes no assumptions and fully works with declarative descriptions of forms.
Nonetheless, these results highlight the need for further research to improve accessibility, making these technologies more user-friendly for individuals without prior technical knowledge.
Validation, auto-completion, and automatically suggesting bindings based on field names are not currently addressed but present valuable concepts for future work.

<span class="comment" data-author="RV">All of the above is summary and is not key to the conclusion. It's not wrong, but there's nothing extra for the reader.</span>

Where users such as Alice found themselves in a centralized and strongly coupled network of service providers before,
<span class="comment" data-author="RV">Mmm, Alice is fake, so I wouldn't use her.</span>
our DFDP tools empowers her with a decentralized and decoupled alternative.
Alice can now decide where to store her filled in data by changing the form description, restoring her control over her data.
Moreover, she can now render the form in her own viewing environment thanks to the declarativity.
In addition, the form can be prefilled automatically thanks to the semantics contained in that description.
Previously, she couldn't reuse Bob's form, but now she can copy and modify it, saving time by not having to start from scratch.

<span class="comment" data-author="RV">Nothing new in the above paragraph/</span>

<span class="comment" data-author="RV">Suggestion: rewrite the entire conclusion. First take paper and pen to write down what readers really learn from this article. So not: what have they read (they already have). But what can researchers and developers now do as a result of our work, that was more difficult before? (We don't care about end-users in the conclusion.) How can researchers build upon this work? What are the open challenges? What directions can future work take?</span>
