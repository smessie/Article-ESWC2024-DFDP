## Evaluation
{:#evaluation}

In this section, we evaluate the proposed architecture and implementation.
First, we analyze conformance to the requirements in [](#requirements-conformance).
Second, we describe the results of the user study in [](#user-study).
We created a sustainability plan to guarantee the maintenance of the DFDP's tools, both short-term and long-term.[^SustainabilityPlan]

[^SustainabilityPlan]: The sustainability plan can be found at [https://github.com/SolidLabResearch/FormGenerator/wiki/<wbr/>Sustainability-Plan](https://github.com/SolidLabResearch/FormGenerator/wiki/Sustainability-Plan).


### Conformance to the Requirements
{:#requirements-conformance}

In this section, we analyze the conformance of the implemented applications to the requirements defined in [](#requirements-table) under [](#requirements).

The first research question is: "How can form developers create forms to declaratively control machines for producing RDF in **multiple viewing environments** (such as Web pages and text-based via a command line)?".
The FormRenderer and FormCli applications showcase creating a form renderer application in multiple viewing environments (R4).
The form was described declaratively (R1) as the display part is fully described using the already existing UI ontology.
Data can be passed along to automatically prefill a form by machines using the form fields' bindings (R2), and users can interpret the field title to manually enter a value (R3).

The second research question is: "How can machines **translate form descriptions** decoupled from the application into a vocabulary that the application understands?".
N3 conversion rules can be passed along allowing reasoning to automatically translate the form description into the ontology the application understands (R5).

The third research question is: "How can machines **perform controllable and reusable actions** on the filled out data?".
The form description also declaratively describes what should happen in case of a certain trigger (R6).
Because this is described in a machine-readable way using RDF, a machine can interpret this and execute the right actions (R7).

Considering the information above, we can confidently assert that we cover all the functional requirements outlined in [](#requirements-table).


### User Study
{:#user-study}

To show that the user experience is not impacted due to the Semantic Web technologies used in the DFDP, we perform a user study.
The goal of this user study is to see if next to the functional requirements, the implementations are also comprehensible for end-users.
We define "comprehensible for users" as the ability for users to understand the application in such a way that they can use it correctly (i.e. accurately) without getting frustrated or giving up (i.e. in a reasonable time).
In what follows, we discuss the user experience by doing a qualitative analysis [](cite:cites Creswell_Creswell_2018) by the use of the [_think aloud method_](cite:cites van1994think) and open-ended interviews split up into two parts: form editing (evaluating the FormGenerator) and form usage (evaluating the FormRenderer).
The FormCli application is not considered as this is a more complex version of the FormRenderer application.

#### Method

Potential participants were directly contacted by the author out of which 19 took part in the study.
8 individuals with a technical background evaluated the FormGenerator application, aligning with its target audience, much like creating a Google Forms is intended for users with technical proficiency.
To meet this requirement, computer science students were primarily sought as participants.
The 11 participants for the form usage part were people both with and without technical backgrounds with ages spanning from 18 to 52 years.
This aligns with the target group of this and similar traditional applications [](cite:cites petrosyan2023distribution), assuming users are familiar with a computer and the Web.
Both groups were provided with simple scenarios instructing them to either generate a form for a restaurant review or fill out an earlier generated form, modeled to mimic normal day tasks.[^UserStudies]
The FormGenerator participants were given a list of bindings to be used to create the form, fulfilling the assumption that they have knowledge of Linked Data.
All necessary data elements were put in place for the FormRenderer application by giving the users a specific link autopopulating the input fields.

[^UserStudies]: The user study scenarios can be found at [https://github.com/SolidLabResearch/FormGenerator/wiki/<wbr/>User-Experience-Scenarios](https://github.com/SolidLabResearch/FormGenerator/wiki/User-Experience-Scenarios).


#### Threats to Validity

As with any study, our evaluation carries threats to validity. We identified the following external and internal threats [](cite:cites Creswell_Creswell_2018) because all participants were recruited from the same country and most of them are students at the same university.
We identified the external threat *Interaction of selection and treatment*.
However, we do assume that users of the form editing have more technical knowledge, so this lies in line with our intentions.
Additionally, basic computer and web proficiency are assumed for form usage.

The internal threat *Selection* was also identified.
While most participants possess technical knowledge, this is deliberate as it is a prerequisite for the form editing part.
To ensure equal knowledge of Linked Data, we provided possible bindings.
To mitigate a selection bias, we also recruited some non-students and participants from different ages.


#### Results

We categorized feedback from all users for both applications and received generally positive results.
Especially in the case of the FormRenderer, no participant noted any significant differences in terms of ease of use.
Regarding the FormGenerator, 5 out of 8 participants rightly noted that as restaurant owners, they shouldn't need to be concerned with bindings.
As a result, future research should consider the automatic suggestion of bindings based on the field label entered by the user.
