## Conclusion
{:#conclusion}

In this article, we introduced decoupled Web forms considered as three parts by creating a Declarative Form Description Pipeline (DFDP).
The implementations of the FormRenderer and FormCli prove that the display part is loosely coupled to the rendering environment.
The FormGenerator shows how such declarative form descriptions can be produced.
This enables the developer to use the same description for multiple viewing environments.
We also provide them with tools they can build further upon to learn how to do so.

Developers and researchers can use the FormRenderer tool to insert data into a defined shape outlined in the form description, thus minimizing
the risk of data entry errors since users are only responsible for inputting raw data into the application's interface.

By using the DFDP, form developers can build new forms faster by reusing existing forms rather than starting from scratch.
Additionally, by extending upon existing display ontologies such as Solid-UI and SHACL, there is no need for developers adopting the DFDP to start over again.
They can reuse existing form descriptions and extend it with footprint tasks, rather making it an extra step to more possibilities.
To help developers perform this extra step, they can reuse the code as part of this research to execute the policies.
This allows them to quickly start performing user defined actions on filled in data.

Schema alignment enables developers to use data in their application written in any ontology that is semantically equivalent to theirs, making it easier to use existing data of other applications.
The DFDP makes it easier for developers and researchers to substitute one application in the pipeline with another without the need to also reimplement the other application.
Furthermore, existing form descriptions can still be used, making it easier for end-users to switch applications and adopt new versions, and for developers to publish new applications.
Researchers can more easily build upon existing applications to extend them with new technologies in their future research.

Such future research could focus on automatically suggesting bindings based on field names entered by the users, which can build on [_Entity Extraction_](cite:cites exner2012entity).
Other directions for future work may involve streamlining the schema alignment and footprint tasks to make them more abstract for developers.
Embedding schema alignment as a layer between the application and the data would enable developers to automatically consider semantically equivalent ontologies as the same, resulting in real interoperability without requiring extra work from the developers.

In general, declarative and decoupled Web forms will lead to a more decentralized Web where people are in more control over their own data and real data reuse becomes possible.
