## Related Work
{:#related-work}

### Standalone Technologies

[XForms](cite:cites boyer_xforms_nodate) was introduced in 2003 as a standalone technology for collecting inputs from Web forms.
The specification became a W3C Recommendation in 2009.
In 2010, work started on [XForms 2.0](cite:cites xforms).
The XForms architecture separates _presentation_, _content_, and _purpose_, in a way that closely resembles the _display_, _shape_, and _reasoning_ architecture introduced in this paper.
Web forms are structured using XML, with elements and attributes specifying constraints.
XForms lacks reasoning capabilities and Semantic Web functionalities for producing and understanding RDF data, limiting its potential in our research focus.

An alternative technology for form-based RDF data editing and presentation is [RDForms](cite:cites metasolutions_rdforms_nodate),
comprising two main components: the *RDForms library* parse, serialize, and manipulate RDF graphs, and *RDForms templates* ensure correct RDF expression production and manipulation. However, the system lacks reasoning capabilities.
In this paper, we propose adding schema alignment and event-driven actions to achieve a fully decoupled declarative form solution.


### Ontologies

The Shapes Constraint Language [(SHACL)](cite:cites shacl) is a W3C Recommendation to define and validate RDF graphs based on conditions declared in shapes.
These shapes serve as descriptions of the data graphs they validate and can also define display fields for forms.
Property shapes include non-validating properties (e.g. for supplementary form construction information), and validating properties (e.g. for specifying datatype and minimum count constraints).

_Solid-UI_ introduces foundational components for user interface widgets and utilities tailored for Solid applications, and a [UI ontology](cite:cites solid-ui). 
Solid-UI Forms primarily addresses form display aspects and associates semantic meaning with form fields via the `ui:property` predicate. 
Additional properties can be employed to specify field behavior.

Other efforts (e.g. [RDF-Form](cite:cites rdf-form)) also describe forms in RDF, enabling semantic representation of form fields, addressing display and shape aspects in the three-part view.
Additionally, we aim to describe footprints that outline actions for events (e.g. submission), such as data storage location or required updates to other documents&nbsp;[](cite:cites shapes).
Describing this as footprints enables machine interpretation, ensuring actions aren't bound to specific applications.
Consequently, data handling becomes standardized across applications, fostering real interoperability.
However, existing ontologies lack a mechanism for describing footprints, leaving a gap in achieving a fully declarative form description solution.
