## Conclusion
{:#conclusion}

In this paper, we introduced decoupled Web forms considered as three parts by creating a Declarative Form Description Pipeline (DFDP).
This work is not solely a theoretical approach.
The implementations of the FormRenderer and FormCli prove that the display part is not tight to one rendering environment.
The FormGenerator shows how such declarative form descriptions can be produced.

The introduced schema alignment and footprint tasks allows users to use different vocabularies than the app understands and allows them to execute declaratively defined policies on the occurrence of events.
The introduced FormRenderer is thereby the first system that makes no assumptions and fully works with declarative descriptions of forms.
Nonetheless, these results highlight the need for further research to improve accessibility, making these technologies more user-friendly for individuals without prior technical knowledge.
Validation, auto-completion, and automatically suggesting bindings based on field names are not currently addressed but present valuable concepts for future work.

Where users such as Alice found themselves in a centralized and strongly coupled network of service providers before, they are now empowered with a decentralized and decoupled alternative.
Alice can now decide where to store her filled in data by changing the form description, restoring her ownership over her data.
Moreover, she can now render the form in her own viewing environment thanks to the declarativity.
In addition, the form can be prefilled automatically thanks to the semantics contained in that description.
Previously, she couldn't reuse Bob's form, but now she can copy and modify it, saving time by not having to start from scratch.
