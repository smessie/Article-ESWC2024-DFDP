## Implementation
{:#implementation}

Three proof-of-concept apps are implemented in TypeScript/JavaScript.
The FormGenerator app is an application programmed in the [Ember framework](cite:cites emberjs) generating a form description based on the form the user builds using drag-and-drop.
The FormRenderer app and FormCli app are two apps that render a given form description in respectively a Web browser using HTML or a text-based command-line interface.

### FormGenerator
{:#implementation-formgenerator}

The FormGenerator app is developed using Redpencil's [ember-solid library](cite:cites ember-solid) and [rdflib.js](cite:cites rdflibjs).
In [](#fig:FormGenerator) you can see a screenshot of the app where the user can provide policy values, next to the ability to define form fields.
Not all possible form elements are supported as it only functions as a proof of concept, but additional field types can be added similarly to the existing ones.
The drag-and-drop functionality is implemented using the [ember-drag-drop add-on](cite:cites ember-drag-drop-addon).
Authentication is managed by ember-solid, redirecting users to the Solid IDP for login when accessing the app.

<figure id="fig:FormGenerator" class="halfwidth">
<img src="img/FormGenerator.png" alt="[Screenshot of FormGenerator application]" />
<figcaption markdown="block">
Implemented FormGenerator app.
</figcaption>
</figure>

The policies are implemented using N3 rules.
Some limitations necessitate workarounds in the implementation, such as rdflib.js lacking support for N3 rules, preventing parsing of resources containing such rules.
The issue with N3 rules extends beyond rdflib.js; inserting and deleting N3 rules from a resource is also problematic.
N3 rules are distinct from standard triples as they involve quoted graphs in the subject and object [](cite:cites n3), a feature not supported in existing Solid data manipulation protocols, including SPARQL Update and N3 Patch.
The only way to insert and delete N3 rules appears to be using an HTTP PUT request with the newly updated resource as the body.
Inserting, deleting, and updating N3 rules involves retrieving the resource, locally modifying it with the new N3 rule, and then performing a PUT operation to update the server-held resource.
To implement this, the N3 rules within the retrieved resource must be parsed to identify existing rules that may require updates or deletions.
This is achieved through a RegEx pattern, as shown in [](#lst:match-n3-rules-regex).
It will however also match N3 statements that use a different namespace than the `log` vocabulary used in the N3 rules' predicates as it does not check the prefix of `:implies`.
Viewed as a feature, the N3 parser may have issues with both actual N3 rules and similar-looking N3 statements with different predicates.

<figure id="lst:match-n3-rules-regex" class="listing">
<pre><code>
/\{[^{}]*}\s*(=>|[^\s{}:]*:implies|
<http:\/\/www.w3.org\/2000\/10\/swap\/log#implies>)\s*{[^{}]*}\s*\./g
</code></pre>
<figcaption markdown="block">
RegEx to match N3 rules.
</figcaption>
</figure>

Reasoning and querying are employed to parse existing rules, enabling user display and editing.
Reasoning is performed by the [EYE-JS library](cite:cites eye-js), a browser and node-distributed EYE reasoner via WebAssembly.
Querying of the retrieved form conclusion to actually parse the policy is done by [Comunica](cite:cites taelman_iswc_resources_comunica_2018), a knowledge graph querying framework.

When constructing the form, users must specify bindings for each field, which are URIs semantically describing the fields.
Users must manually enter these bindings. To simplify this process, they can utilize prefixes, which are automatically expanded to full URIs via the [prefix.cc](https://prefix.cc) API.
As an example, `ex:MyField` will become `http://example.org/MyField`.


### FormRenderer

<figure id="fig:FormRenderer" class="halfwidth">
<img src="img/FormRenderer.png" alt="[Screenshot of FormRenderer application]" />
<figcaption markdown="block">
Implemented FormRenderer app.
</figcaption>
</figure>

The FormRenderer app is created in the [Vue.js framework](cite:cites vue).
A screenshot of this app is shown in [](#fig:FormRenderer).
Authentication is implemented using the [`@inrupt/solid-client-authn-browser`](https://www.npmjs.com/package/@inrupt/solid-client-authn-browser) library ensuring that the user's Solid pod does not need to be publicly readable and writable.
This allows a user to authenticate with their Solid pod and then the app can read and write to the pod on behalf of the user.
However, authentication is not necessary if the user only wants to render a publicly accessible form.

Schema alignment tasks are performed by applying the N3 rules from the conversion rules resource over the form description using the EYE-JS reasoner library mentioned before.
The output of this reasoning step is the equivalent form description in the Solid-UI vocabulary, which is then parsed by the Comunica engine using SPARQL queries.

When dealing with a resource containing pre-existing data for form filling, it's straightforward to determine the subject URI for writing new data — it can be reused from the existing data.
Furthermore, when no resource is provided or when multiple subjects within the resource conform to the form's structure and target class, determining the subject URI becomes ambiguous.
Various solutions were explored to address this problem.

1. Generating a new random UUID and using it as the subject URI with the `urn:uuid:` namespace [](cite:cites leach_universally_2015).

2. Prompting the user to enter a subject URI.

3. Utilizing the URI from the HTTP Request policy as the subject URI.

4. Selecting one of the existing subjects as the subject URI.

5. Employing a blank node in place of a subject URI.

6. Specifying the subject URI in the form description.

Blank nodes are often an unsuitable solution since they lack a URI, making it impossible to reference the data using a valid URI or to link to from other resources.
Using the URI to which the data is posted is also not a good solution, as this URI is not necessarily meaningful or even a unique URI.
Not all ontologies for describing forms do have a property to define the subject URI, eliminating option 6.
This leaves us with options 1, 2, and 4 as the viable choices.
Using a random UUID is a feasible solution, ensuring uniqueness, and serving as an ideal default subject URI.
Prompting the user allows the user to enter a meaningful subject URI himself, which is also feasible.
Focusing solely on this option requires users to understand subject URIs, potentially complicating app use for those new to the Semantic Web. Our goal is to ensure ease of use for all.
Using an existing subject is a good option, especially when there's a single subject, aligning with user expectations for data editing.
With multiple subjects, selection becomes a challenge for users unfamiliar with the concept.
We propose and implement a combination of the three last feasible options.
Use a random UUID as the default subject URI, while enabling user selection from existing subjects or manual subject URI entry.
Parsing the policies is done in the same was as in the FormGenerator app, described earlier in [](#implementation-formgenerator).

### FormCli

Similar to the FormRenderer app, the FormCli app is also a form renderer, but it operates as a command-line application, allowing usage without a GUI.
It is written in JavaScript and uses the Node.js runtime environment.
Its architecture and implementation closely resemble that of the FormRenderer app, and also uses Comunica for querying various resources.

The [Inquirer.js](cite:cites boudrias_sboudriasinquirerjs_2013) library is used to prompt the user interactively with the different questions contained in the form.
Based on the field type, a different kind of prompt is used.
To support easy input of dates, the [inquirer-date-prompt](cite:cites havermale_haversnailinquirer-date-prompt_2021) plugin is used.

The FormCli app does not support authentication with a Solid identity provider, as the Solid protocol lacks proper authentication for command-line applications.
Although Inrupt has a Solid authentication library for the CLI, it requires manual setup of prerequisites like refresh tokens and client credentials [](cite:cites inrupt_authenticate_nodate).
Authentication is not implemented as it falls outside the scope of this project.
The main emphasis is on demonstrating the feasibility of a form renderer app without a GUI, not requiring authentication.
