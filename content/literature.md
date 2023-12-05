## Related Work
{:#related-work}

### Standalone Technologies

In 2003, [XForms](cite:cites boyer_xforms_nodate) was introduced as a standalone technology for collecting inputs from Web forms.
The original specification became a W3C Recommendation in 2009 and is still the official version.
In 2010, work started on the new version [XForms 2.0](cite:cites xforms).
The split architecture of XForms separates _presentation_, _content_, and _purpose_, in a way that closely resembles the three-part _display_, _shape_, and _reasoning architecture_ introduced in this paper.
Web forms are specified using an XML model.
Values can be limited by referencing XML elements, which use attributes to define type and other constraints.
While an XML element for submission can specify the data destination and the required HTTP method, no reasoning capabilities are available in the specification.
As a pure XML solution, XForms also lacks Semantic Web capabilities to produce and understand RDF data, which is the focus of our research in this paper.

An alternative technology that allows form-based editing and presentation of Semantic Web data is [RDForms](cite:cites metasolutions_rdforms_nodate).
This solution consists of 2 main components: *RDForms library* and *RDForms templates*.
The first one is responsible for the parsing, serializing, and manipulation of RDF graphs, while the latter makes sure the right RDF expression is produced and manipulated.
Although this system successfully provides form-based editing and presentation of RDF data, also here reasoning capabilities are not available.
In this paper, we will add schema alignment and event-driven actions as features for a fully decoupled declarative form solution.


### Ontologies

[SHACL](cite:cites shacl), short for Shapes Constraint Language, is a W3C recommendation vocabulary used to define and validate RDF graphs based on a set of conditions, which are declared in shapes and consist of constraints.
These shapes can also be viewed as a description of the data graphs they validate.
Besides validation, such descriptions can also be used to define the display fields of (Web) forms.
A property shape comprises non-validating properties, ignored by SHACL processors, and validating properties that represent validation conditions.
The former can be utilized to provide supplementary information, such as for form construction, while the latter specify constraints on the values of the properties of the focus node.
Examples are `sh:datatype` and `sh:minCount`.

_Solid-UI_ is the name for user interface widgets and utilities for Solid.
Next to the building blocks for Solid-based apps, there also exists a [Solid-UI vocabulary](cite:cites solid-ui), which will be of interest in this paper.
The vocabulary mainly focuses on the display part of forms.
Next to that, the form field's semantic meaning is contained in the form description by using the `ui:property` predicate.
Extra properties can be specified to define the field's behavior.
The Solid-UI ontology can be used to define forms in RDF with a declarative form renderer using this ontology [](cite:cites hochstenbach_rdf_2022).

There were also other <span class="rephrase" data-author="RV">attempts</span> to describe forms in RDF such as [RDF-Form](cite:cites rdf-form).
<span class="comment" data-author="RV">Careful calling other people's work <q>attempts</q></span>
All these ontologies allow for describing the fields contained in a form in a semantic way.
This corresponds to the display and shape parts of the three-part view.
In addition, we want to describe footprints, i.e. what actions to perform in case of certain events like submission.
Footprints outline the way the data entered into the form should be handled, such as where it should be stored or what updates to other documents are required [](cite:cites shapes).
Describing this information as footprints allows machines to interpret it, and actions are not tied to applications.
As a result, different apps will store the data in the same way and real interoperability is achieved.
As these ontologies do not provide a way to describe such footprints, they do not provide a complete solution for a fully declarative form description.
