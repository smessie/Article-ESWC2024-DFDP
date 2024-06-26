## Conclusion
{:#conclusion}

In this article, we introduced a Declarative Form Description Pipeline (DFDP) offering significant enhancements in data management for both end-users and organizations.
End-users benefit from increased control over their data input, facilitated by footprints that specify data handling actions.
Additionally, they can reuse existing data to prefill forms and choose their preferred application to manage their data, regardless of the underlying ontology, thanks to schema alignment.
This decoupling of applications and data ensures greater flexibility and autonomy for end-users.
For organizations, DFDP enables better data management in terms of reusability, allowing for easy adoption and customization of existing forms without requiring additional assumptions from developers.
This, in turn, improves cost-efficiency and promotes streamlined workflows.
The DFDP enables the embedding of semantics into the input data, improving the alignment of data across different related forms in a dataspace.
Overall, DFDP marks a significant step forward in enhancing data management practices with its declarative and decoupled Web forms for both end-users and organizations.

Future research could focus on automatically suggesting bindings based on field names entered by the users, which can build on [_Entity Extraction_](cite:cites exner2012entity).
Other directions for future work may involve streamlining the schema alignment and footprint tasks to make them more abstract for developers.
Embedding schema alignment as a layer between the application and the data would enable developers to automatically consider semantically equivalent ontologies as the same, resulting in real interoperability without requiring extra work from the developers.
A first step could be to package the DFDP modules as libraries to ease the integration into existing Web applications.
