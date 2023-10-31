## Evaluation
{:#evaluation}

In this section, the proposed architecture and implementation in order to answer the research questions will be evaluated.
First, in [](#requirements-conformance), the conformance to the requirements from [](#introduction) will be analyzed.
Second, a user study will be conducted in [](#user-study) to see if next to the functional requirements, the implementations are also comprehensible for users.

### Conformance to the Requirements
{:#requirements-conformance}

In this section, we analyze the conformance of the implemented apps to the requirements defined in [](#requirements-table) under [](#requirements).

#### Multiple Viewing Environments

The first research question was: "How can machines be controlled in a declarative way to create forms for producing RDF in **multiple viewing environments** (such as the web and text-based via a command line)?".
The FormRenderer app and the FormCli app are apps in different viewing environments and thus demonstrate that it is possible to create a form renderer application in multiple viewing environments (R4).
The form was described in a declarative way (R1) as the display part is fully described using the already existing Solid-UI ontology.
By making form descriptions portable and not tight to one rendering environment or one rendering logic, machines can be controlled to create forms for producing RDF in multiple viewing environments.
It is possible to pass along data and a machine can automatically prefill your form by using the bindings attached to form fields (R2), and a user can interpret the title of the form field to manually enter a value (R3).

#### Schema Alignment Tasks

The second research question of this paper was the following: "How can machines be controlled in a declarative way to **translate form descriptions** decoupled from the application into a vocabulary that the application understands?".
N3 conversion rules can be passed along allowing reasoning to automatically translate the form description into the ontology the app understands (R5).

#### Footprint Tasks

The third research question was: "How can machines be controlled in a declarative way to **perform actions** on the filled out data?".
The form description also describes in a declarative way what should happen in case of a certain trigger (R6).
Because this is described in a machine-readable way using RDF, a machine can interpret this and execute the right actions (R7).

Considering the information above, we can confidently assert that we cover all the functional requirements outlined in [](#requirements-table).


### User Study
{:#user-study}

In what follows, the user experience will be discussed by doing a qualitative analysis [](cite:cites Creswell_Creswell_2018) by the use of open-ended interviews split up into two parts: form editing (evaluating the FormGenerator) and form usage (for evaluating the FormRenderer).
The FormCli app is not considered as this is a more complex version of the FormRenderer app where a user interacts with the app through the command line instead of a GUI.
The goal of this user study is to see if next to the functional requirements, the implementations are also comprehensible for users.
We define "comprehensible for users" as the ability for users to understand the app in such a way that they can use it correctly (i.e. accurately) without getting frustrated or giving up (i.e. in a reasonable time).

#### Method

Potential participants were directly contacted by the author out of which 19 took part in the study, with 8 evaluating the FormGenerator app and 11 evaluating the FormRenderer app.
The first group consisted of individuals with a technical background, aligning with the FormGenerator's target audience, much like creating a Google Forms is intended for users with technical proficiency.
To meet this requirement, computer science students were primarily sought as participants for this part.
The 11 participants for the FormRenderer user study were people both with and without technical backgrounds with ages spanning from 18 to 52 years.
This aligns with the target group of this and other similar traditional applications [](cite:cites petrosyan2023distribution), as it's assumed that users can already work wit a computer and the Web.
Both groups were provided with simple scenarios instructing them to either generate a form for a restaurant review or fill out an earlier generated form, modeled to mimic normal day tasks.
They can be found at [https://github.com/SolidLabResearch/FormGenerator/wiki/User-Experience-Scenarios](https://github.com/SolidLabResearch/FormGenerator/wiki/User-Experience-Scenarios).
The users remained access to the scenario while performing the task.
The users evaluating the FormGenerator app are given a list of bindings to be used to create the form, fulfilling the assumption that they have knowledge of Linked Data.
All necessary data elements were put in place for the FormRenderer app by giving the users a specific link autopopulating the input fields.
During the last step, participants completed an open-ended exit survey to evaluate the app e.g. by comparing the app they had employed with a traditional app like Google Forms.


#### Threats to Validity

As with any study, our evaluation carries threats to validity. We identified following external and internal threats [](cite:cites Creswell_Creswell_2018) because all participants were recruited from Belgium and most of them are students at Ghent University.
The findings might bot be generalizable to a more general population because of the external threat *Interaction of selection and treatment*.
However, we do assume that users of the form editing have more technical knowledge, so this lies in line with our intentions.
For the form usage we also assume that the user has some basic knowledge about working with a computer and the Web.

The internal threat *Selection* concerns the selection of participants who have certain characteristics that predispose them to have certain outcomes.
Most of the participants have a certain technical knowledge, but this is intentional as it is a prerequisite for the form editing part of the user study.
To give them all an equal knowledge of Linked Data, possible bindings were provided to them.
To mitigate a selection bias, some participants not studying at Ghent University were also recruited and participants from different ages were contacted.


#### Results

The feedback received from the open-ended interview is summarized below.
Just like the user study itself, the results are split up in two parts for the two different apps.

##### FormGenerator

Users provided feedback that the app was user-friendly, particularly due to its drag-and-drop functionality.
They appreciated the capability to reorder fields using drag-and-drop, although some users suggested the option to drop a field between two existing ones.
Multiple respondents expressed interest in having a live form preview while creating it.
Despite positive experiences, users were frustrated with the need to use bindings to create the form.
They found it challenging to understand and match the right binding to the field, rightly noting that as restaurant owners, they shouldn't need to be concerned with bindings.
In addition, a user wished for binding validation or auto-completion to ensure accuracy, but implementing this would require defining and verifying all bindings, posing some challenges.
In cases where binding definitions are lacking, like with the `ex:` namespace, full validation isn't possible.
Nonetheless, issuing a warning for incorrect bindings would enable users to proceed with form creation, minimizing disruption.
Users found the vocabulary selection confusing, as they didn't understand the basis for choosing between SHACL, Solid-UI, and RDF-Form.
This choice, initially intended to support different vocabularies, may still benefit technically proficient users seeking to create a form based on a specific vocabulary.

In SHACL, marking a field as required or permitting multiple answers is done via the `sh:minCount` and `sh:maxCount` properties.
However, users found specifying "min count" and "max count" confusing, lacking clarity about their meaning.
Lastly, some users expected a radio button field for score selection when providing a review.
Initially, a dropdown field was considered, but radio buttons were deemed more user-friendly.
However, these apps are proof of concept with a limited range of field types, and radio buttons haven't been implemented yet.
This feature should be considered for future versions of the FormGenerator app.
Consequently, this feedback, although valid, was not seen as a negative aspect of the app.
In summary, the feedback on the FormGenerator app was positive, with 6 out of 8 users successfully creating the form, despite encountering challenges with bindings.
It's important to note that only users with some technical background participated in this evaluation.
Future work should explore more abstract methods for managing bindings.

##### FormRenderer

The feedback received from all participants of this task was that the app was clear, and straightforward and easy to use.
No critical issues were raised. The app is straightforward and fulfills its expected functions.
Users suggested additional improvements, such as automatically hiding the input panel when required input fields were pre-filled via URL query parameters, aiming to reduce the technical information displayed to users.
Furthermore, one user expected a multi-line text field for the review input, but the form description was constructed using the SHACL vocabulary, which doesn't support multi-line text field definitions.
This illustrates that SHACL is primarily designed for validation, not for defining the display aspects, as previously highlighted.
The date field received mixed feedback.
Some users appreciated the pre-populated dashes in it, while others found it inconvenient to have to click on the calendar icon for entering a date via the popup calendar.
Additionally, one user expressed confusion about the purpose of the Subject URI. While there is usually at least one valid suggestion for those without prior knowledge, the lack of understanding can still lead to confusion when making a selection.
Besides that, the users did not notice that the app was using Solid and Linked Data behind the scenes and this is exactly the goal of the FormRenderer app.
People who were given a form described using the SHACL vocabulary were unaware that schema alignment tasks were being performed behind the scenes.
To conclude, the feedback on the FormRenderer app was positive and all the participating users were able to fill in the form without any issues.
The app was straightforward and users did not realize that Solid and Linked Data were involved behind the scenes.
This is a positive aspect, indicating the app's ease of use for individuals with no prior knowledge of Solid and Linked Data.
