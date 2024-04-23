## Implementation
{:#implementation}

We implemented three applications in TypeScript.
The FormGenerator application generates a form description based on the form the user builds using drag-and-drop.
The FormRenderer application and FormCli application are two applications that render a given form description in respectively a Web browser using HTML or a text-based command-line interface.

### FormGenerator
{:#implementation-formgenerator}

The first application in the pipeline generates the declarative form description.[^ImplementationFormGenerator]
In [](#fig:FormGenerator) a screenshot of the implemented application can be seen, showing how form developers can define policies and form fields using a drag-and-drop interface.

[^ImplementationFormGenerator]: The FormGenerator source code can be found at [https://w3id.org/DFDP/FormGenerator/source](https://w3id.org/DFDP/FormGenerator/source) and the live version at [https://w3id.org/DFDP/FormGenerator/app](https://w3id.org/DFDP/FormGenerator/app).

<figure id="fig:FormGenerator" class="halfwidth">
 <img src="img/FormGenerator.png" alt="[Screenshot of FormGenerator application]" />
 <figcaption markdown="block">
 Implemented FormGenerator application.
 </figcaption>
 </figure>

Describing footprints requires a rule and a policy language.
As rule language, [Notation3 (N3)](cite:cites n3) is used.
The rule premise defines the event, while the rule conclusion defines the policy.
We chose N3 as it proved to be a working solution for our use case and the reasoning engine EYE implementing N3 is being developed at our lab.
We therefore also made the decision to use the [EYE-JS library](cite:cites eye-js), a browser and node-distributed EYE reasoner via WebAssembly.
By the use of reasoning, we obtain the rule conclusion which is then parsed using a SPARQL query.
Querying is done using [Comunica](cite:cites taelman_iswc_resources_comunica_2018), a knowledge graph querying framework.

The policy we obtain is defined using a policy language.
There are already existing ontologies that can be reused to describe policies, even though they were not designed for this purpose.
[Hydra](cite:cites hydra) is a vocabulary to describe Web APIs in Linked Data and its intended use is to describe the server side of the API in a machine-readable way.
A major limitation of our research is that it can only describe HTTP requests, while policies go beyond that.
Therefore, we chose to not use Hydra.

The [_Function Ontology (FnO)_](cite:cites fno-paper) is used to semantically define and describe implementation-independent functions, including their relations to related concepts such as parameters, and mappings to specific implementations and executions.
As FnO allows the description of any kind of operation unlike e.g. Hydra which only allows the description of HTTP requests, a basic version of this existing ontology together with the [HTTP Vocabulary](cite:cites koch_http_2017) is reused to describe the policy.
A *Policy ontology* has been developed using the [LOT Methodology](cite:cites poveda-villalon_lot_2022) defining the missing classes and properties required for policy definition. [^PolicyOntology]
The ontology enables the description of events and the corresponding actions to be taken.
The ontology was implemented using Protégé as the ontology development environment, using the OWL language.
The ontology's source is available on GitHub, and the ontology itself is published using GitHub pages. 
A w3id is used to provide a permanent identifier for the ontology, which includes both human-readable documentation and a machine-readable file accessible via the URI using content negotiation.
Hosting the source on GitHub facilitates easy maintenance, and contributions can be made through pull requests and the issue tracker.
[](#lst:n3-form-policies-example) contains an example of a footprint task sending an HTTP request.

[^PolicyOntology]: The Policy ontology can be found at [https://w3id.org/DFDP/policy](https://w3id.org/DFDP/policy).

When constructing the form, users must specify bindings for each field, which are URIs semantically describing the fields.
Users must manually enter these bindings. To simplify this process, they can utilize prefixes, which are automatically expanded to full URIs via the [prefix.cc](https://prefix.cc) API.
As an example, `ex:MyField` will become `http://example.org/MyField`.

<figure id="lst:n3-form-policies-example" class="listing halfwidth">
<pre><code>@prefix ex:   <http://example.org/> .
@prefix pol: <https://w3id.org/DFDP/policy#> .
@prefix fno: <https://w3id.org/function/ontology#>.
@prefix http: <http://www.w3.org/2011/http#>.
{
  ?id pol:event pol:Submit.
} => {
  ex:HttpPolicy pol:policy [
    a fno:Execution;
    fno:executes http:Request;
    http:methodName "POST";
    http:requestURI <https://httpbin.org/post>;
    http:headers (
      [
        http:fieldName "Content-Type";
        http:fieldValue "application/ld+json"
      ]
    )
  ] .
} .
</code></pre>
<figcaption markdown="block">
Example of N3 rule describing HTTP request policy to be executed on the form submission event.
</figcaption>
</figure>


### FormRenderer and FormCli

<figure id="fig:FormRenderer" class="halfwidth">
 <img src="img/FormRenderer.png" alt="[Screenshot of FormRenderer application]" />
 <figcaption markdown="block">
 Implemented FormRenderer application.
 </figcaption>
</figure>

The next application in the pipeline renders the declarative form description and lets the user fill out that form.
We implemented two versions in two different viewing environments to prove that the display part of the form description is independent of the viewing environment.[^ImplementationFormRenderer] [^ImplementationFormCli]
The FormRenderer application, as shown in the screenshot in [](#fig:FormRenderer), functions in the Web browser.
The FormCli application operates as a command-line application, allowing usage without a GUI.
The form questions are prompted to the user one after the other.
While the FormRenderer application supports authenticating with a Solid identity provider, authentication is not implemented in the FormCli application as the Solid protocol lacks proper authentication for command-line applications.
We therefore consider this outside the scope of this research.

[^ImplementationFormRenderer]: The FormRenderer source code can be found at [https://w3id.org/DFDP/FormRenderer/source](https://w3id.org/DFDP/FormRenderer/source) and the live version at [https://w3id.org/DFDP/FormRenderer/app](https://w3id.org/DFDP/FormRenderer/app).
[^ImplementationFormCli]: The FormCli source code can be found at [https://w3id.org/DFDP/FormCli/source](https://w3id.org/DFDP/FormCli/source).

The UI ontology is chosen as the application's display ontology as it is designed specifically for defining user interfaces.
Schema alignment is achieved by applying conversion rules to the form description.[^ConversionRulesExample]
The implementation uses N3 rules together with the EYE-JS reasoner to apply them.
The resulting form description in the UI ontology is parsed by the Comunica engine via SPARQL queries.

[^ConversionRulesExample]: An example of SHACL to UI ontology conversion rules can be found at [https://solidlabresearch.github.io/FormRenderer/shacl-to-ui.n3](https://solidlabresearch.github.io/FormRenderer/shacl-to-ui.n3).

#### Determining the Subject for the Produced RDF

When dealing with a resource containing pre-existing data for form filling, it's straightforward to determine the subject URI for writing new data — it can be reused from the existing data.
Furthermore, when no resource is provided or when multiple subjects within the resource conform to the form's structure and target class, determining the subject URI becomes ambiguous.
Various solutions were explored to address this problem.

1. Generating a new random UUID and using it as the subject URI with the `urn:uuid:` namespace [](cite:cites leach_universally_2015).

2. Prompting the user to enter a subject URI.

3. Utilizing the URI from the HTTP Request policy as the subject URI.

4. Selecting one of the existing subjects as the subject URI.

5. Employing a blank node in place of a subject URI.

6. Specifying the subject URI in the form description.

Blank nodes are often an unsuitable solution since they lack a URI, making it impossible to reference the data using a valid URI or to link to/from other resources.
Using the URI to which the data is posted is also not a good solution, as this URI is not necessarily meaningful or even a unique URI.
Not all ontologies for describing forms have a property to define the subject URI, eliminating option 6.
This leaves us with options 1, 2, and 4 as the viable choices.
Using a random UUID is a feasible solution, ensuring uniqueness, and serving as an ideal default subject URI.
Prompting the user enables them to enter a relevant subject URI themselves, which is also feasible.
Focusing solely on this option requires users to understand subject URIs, potentially complicating application use for those new to the Semantic Web. Our goal is to ensure ease of use for all.
Using an existing subject is a good option, especially when there's a single subject, aligning with user expectations for data editing.
With multiple subjects, selection becomes a challenge for users unfamiliar with the concept.
We propose and implement a combination of the three feasible options.
Use a random UUID as the default subject URI, while enabling user selection from existing subjects or manual subject URI entry.
Parsing the policies is done in the same way as in the FormGenerator application, described earlier in [](#implementation-formgenerator).
