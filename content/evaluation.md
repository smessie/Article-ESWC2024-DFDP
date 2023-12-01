## Evaluation
{:#evaluation}

In this section, the proposed architecture and implementation will be evaluated.
First, in [](#requirements-conformance), the conformance to the requirements will be analyzed.
Second, a user study will be conducted in [](#user-study).
A sustainability plan has been created to guarantee the maintenance of the DFDP's tools, both short-term and long-term.[^SustainabilityPlan]

[^SustainabilityPlan]: The sustainability plan for the DFDP's tools can be found at [https://github.com/SolidLabResearch/FormGenerator/wiki/Sustainability-Plan](https://github.com/SolidLabResearch/FormGenerator/wiki/Sustainability-Plan).


### Conformance to the Requirements
{:#requirements-conformance}

In this section, we analyze the conformance of the implemented apps to the requirements defined in [](#requirements-table) under [](#requirements).

The first research question was: "How can agents create forms to declaratively control machines for producing RDF in **multiple viewing environments** (such as Web pages and text-based via a command line)?".
The FormRenderer and FormCli apps showcase the feasibility of creating a form renderer application in multiple viewing environments (R4).
The form was described declaratively (R1) as the display part is fully described using the already existing Solid-UI ontology.
Data can be passed along to automatically prefill a form by machines using the form fields' bindings (R2), and users can interpret the field title to manually enter a value (R3).

The second research question of this paper was the following: "How can machines be declaratively controlled to **translate form descriptions** decoupled from the application into a vocabulary that the application understands?".
N3 conversion rules can be passed along allowing reasoning to automatically translate the form description into the ontology the app understands (R5).

The third research question was: "How can machines be declaratively controlled to **perform actions** on the filled out data?".
The form description also declaratively describes what should happen in case of a certain trigger (R6).
Because this is described in a machine-readable way using RDF, a machine can interpret this and execute the right actions (R7).

Considering the information above, we can confidently assert that we cover all the functional requirements outlined in [](#requirements-table).


### User Study
{:#user-study}

In what follows, we discuss the user experience by doing a qualitative analysis [](cite:cites Creswell_Creswell_2018) by the use of open-ended interviews split up into two parts: form editing (evaluating the FormGenerator) and form usage (evaluating the FormRenderer).
The FormCli app is not considered as this is a more complex version of the FormRenderer app.
The goal of this user study is to see if next to the functional requirements, the implementations are also comprehensible for users.
We define "comprehensible for users" as the ability for users to understand the app in such a way that they can use it correctly (i.e. accurately) without getting frustrated or giving up (i.e. in a reasonable time).

#### Method

Potential participants were directly contacted by the author out of which 19 took part in the study.
8 individuals with a technical background evaluated the FormGenerator app, aligning with its target audience, much like creating a Google Forms is intended for users with technical proficiency.
To meet this requirement, computer science students were primarily sought as participants.
The 11 participants for the form usage part were people both with and without technical backgrounds with ages spanning from 18 to 52 years.
This aligns with the target group of this and similar traditional apps [](cite:cites petrosyan2023distribution), assuming users are familiar with a computer and the Web.
Both groups were provided with simple scenarios instructing them to either generate a form for a restaurant review or fill out an earlier generated form, modeled to mimic normal day tasks.[^UserStudies]
The FormGenerator participants were given a list of bindings to be used to create the form, fulfilling the assumption that they have knowledge of Linked Data.
All necessary data elements were put in place for the FormRenderer app by giving the users a specific link autopopulating the input fields.

[^UserStudies]: The user study scenarios can be found at [https://github.com/SolidLabResearch/FormGenerator/wiki/User-Experience-Scenarios](https://github.com/SolidLabResearch/FormGenerator/wiki/User-Experience-Scenarios).


#### Threats to Validity

As with any study, our evaluation carries threats to validity. We identified following external and internal threats [](cite:cites Creswell_Creswell_2018) because all participants were recruited from Belgium and most of them are students at Ghent University.
We identified the external threat *Interaction of selection and treatment*.
However, we do assume that users of the form editing have more technical knowledge, so this lies in line with our intentions.
For the form usage we also assume that the user has some basic knowledge about working with a computer and the Web.

The internal threat *Selection* was also identified.
Most of the participants have a certain technical knowledge, but this is intentional as it is a prerequisite for the form editing part of the user study.
To give them all an equal knowledge of Linked Data, possible bindings were provided to them.
To mitigate a selection bias, some participants not studying at Ghent University were also recruited and participants from different ages were contacted.


#### Results

Feedback from the open-ended interview is summarized by application.

##### FormGenerator

Users provided feedback that the app was user-friendly, particularly due to its drag-and-drop functionality.
Multiple respondents expressed interest in having a live form preview while creating it.
Despite positive experiences, users were frustrated with the need to use bindings to create the form.
They found it challenging to understand and match the right binding to the field, rightly noting that as restaurant owners, they shouldn't need to be concerned with bindings.
In addition, a user wished for binding validation or auto-completion to ensure accuracy, but implementing this requires defining and verifying all bindings, posing some challenges (e.g. with the `ex:` namespace).
Users found the vocabulary selection confusing, as they didn't understand the basis for choosing between SHACL, Solid-UI, and RDF-Form.
This choice may still benefit technically proficient users seeking to create a form description based on a specific vocabulary.
In SHACL, marking a field as required or permitting multiple answers is done via the `sh:minCount` and `sh:maxCount` properties.
However, users found specifying "min count" and "max count" confusing, lacking clarity about their meaning.
Lastly, some users expected a radio button field for score selection when providing a review, but only the dropdown equivalent has been implemented as these apps are proof of concepts with limited field types.
This should be considered for future versions of the app.
In summary, the feedback on the FormGenerator app was positive, with 6 out of 8 users successfully creating the form, despite encountering challenges with bindings.
Future work should explore more abstract methods for managing bindings.

##### FormRenderer

All participants noted that the app was clear, straightforward, and easy to use.
No critical issues were raised. The app fulfills its expected functions.
Users suggested additional improvements, such as automatically hiding the input panel when required input fields were pre-filled via URL query parameters, aiming to reduce the technical information displayed to users.
Furthermore, one user expected a multi-line text field for the review input, but the form description was constructed using the SHACL vocabulary, which doesn't support multi-line text field definitions.
This illustrates SHACL's limitations as display ontology.
One user expressed confusion about the purpose of the Subject URI. While there is usually at least one valid suggestion for those without prior knowledge, the lack of understanding can still lead to confusion when making a selection.
Besides that, the users did not notice that the app was using Solid and Linked Data behind the scenes and this is exactly the goal of the FormRenderer app.
People were unaware that schema alignment tasks were being performed behind the scenes.
To conclude, the feedback on the FormRenderer app was positive and all the participating users were able to fill in the form without any issues and no prior knowledge of Solid and Linked Data.
