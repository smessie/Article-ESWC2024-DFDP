## Related Work
{:#related-work}

### Standalone Technologies

In 2003, [XForms](cite:cites boyer_xforms_nodate) was introduced as a standalone technology for collecting inputs from Web forms.
The original specification became a W3C Recommendation in 2009 and is still the official version.
In 2010, work started on the new version [XForms 2.0](cite:cites xforms).
The split architecture of XForms separates _presentation_, _content_, and _purpose_, in a way that closely resembles the three-part _display_, _shape_, and _reasoning_ architecture introduced in this paper.
Web forms are structured using XML, with elements and attributes specifying constraints.
XForms lacks reasoning capabilities and Semantic Web functionalities for producing and understanding RDF data, limiting its potential in our research focus.

An alternative technology for form-based editing and presentation of RDF data is [RDForms](cite:cites metasolutions_rdforms_nodate).
The solution comprises two main components: the *RDForms library* for parsing, serializing, and manipulating RDF graphs, and *RDForms templates* ensuring correct RDF expression production and manipulation. However, the system lacks reasoning capabilities.
In this paper, we propose adding schema alignment and event-driven actions to achieve a fully decoupled declarative form solution.


### Ontologies

[SHACL](cite:cites shacl), or Shapes Constraint Language, is a W3C recommendation used for defining and validating RDF graphs based on conditions declared in shapes.
These shapes serve as descriptions of the data graphs they validate and can also define display fields for forms.
Property shapes include non-validating properties, used for supplementary information like form construction, and validating properties, specifying constraints such as datatype and minimum count.

_Solid-UI_ encompasses user interface widgets and utilities tailored for Solid applications.
In addition to providing foundational components, a [UI ontology](cite:cites solid-ui) exists, particularly relevant to this paper. 
This vocabulary primarily addresses form display aspects and associates semantic meaning with form fields via the `ui:property` predicate. 
Additional properties can be employed to specify field behavior.

Other efforts, like [RDF-Form](cite:cites rdf-form), also aimed to describe forms in RDF, enabling semantic representation of form fields, addressing display and shape aspects in the three-part view.
Additionally, we aim to describe footprints, outlining actions for events like submission, such as data storage location or required updates to other documents [](cite:cites shapes).
Describing this as footprints enables machine interpretation, ensuring actions aren't bound to specific applications.
Consequently, data handling becomes standardized across applications, fostering real interoperability.
However, existing ontologies lack a mechanism for describing footprints, leaving a gap in achieving a fully declarative form description solution.
