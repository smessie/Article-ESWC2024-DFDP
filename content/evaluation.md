## Evaluation
{:#evaluation}

In this section, the proposed architecture and implementation in order to answer the research questions will be evaluated.
This evaluation will be divided into two major parts: first in [](#requirements-conformance) the conformance to the requirements from [](#introduction) will be analyzed, and second in [](#user-study) a user study will be conducted to see if next to the functional requirements, the implementations are also comprehensible for users.

### Conformance to the Requirements
{:#requirements-conformance}

In this section, we analyze the conformance of the implemented apps to the requirements defined in [](#requirements-table) under [](#requirements).

#### Multiple Viewing Environments

The first research question was: "How can machines be controlled in a declarative way to create forms for producing RDF in **multiple viewing environments** (such as the web and text-based via a command line)?".
The FormRenderer app and the FormCli app are apps in different viewing environments and thus demonstrate that it is possible to create a form renderer application in multiple viewing environments (R4).
The source code shows how this can be done with the use of SPARQL queries on the declarative form description executed by the Comunica query engine.
The form was described in a declarative way (R1) as the display part is fully described using the already existing Solid-UI ontology.
By making form descriptions portable and not tight to one rendering environment or one rendering logic, machines can be controlled to create forms for producing RDF in multiple viewing environments.
It is possible to pass along data and a machine can automatically prefill your form by using the bindings attached to form fields (R2), and a user can interpret the title of the form field to manually enter a value (R3).

#### Schema Alignment Tasks

The second research question of this paper was the following: "How can machines be controlled in a declarative way to **translate form descriptions** decoupled from the application into a vocabulary that the application understands?".
It is possible to pass along a set of N3 conversion rules such that the form description will automatically be translated thanks to the reasoning into the ontology the app understands (R5).

#### Footprint Tasks

The third research question was: "How can machines be controlled in a declarative way to **perform actions** on the filled out data?".
The form description describes, next to what should be displayed, in a declarative way what should happen in case of a certain trigger (R6).
Because this is described in a machine-readable way using RDF, a machine can interpret this and execute the right actions (R7).

Add a conclusion paragraph where you explicitly state that you cover all requirements
{:.todo}


### User Study
{:#user-study}

In what follows, the user experience of the two apps that are part of the more complex scenario will be discussed by doing a qualitative analysis [](cite:cites Creswell_Creswell_2018).
These are the apps that are relevant to the end goal with the three-part view on Solid Web Forms, being the FormGenerator and the FormRenderer app.
The FormCli app is not considered as this is a more complex version of the FormRenderer app where one interacts with the app through the command line instead of a graphical user interface.
This requires the user to have a certain level of technical knowledge which is an assumption here for the form rendering part.
The goal of this user study is to see if next to the functional requirements, the implementations are also comprehensible for users.
We define "comprehensible for users" as the ability for users to understand the application in such a way that they can use the application correctly (i.e. accurately) without getting frustrated or giving up (i.e. in a reasonable time) and with a qualitative evaluation by the use of open-ended interviews.
This user study will be split up into two parts: form editing (for which the FormGenerator will be evaluated) and form usage (for which the FormRenderer will be evaluated).

#### Method

This user experience was qualitatively analyzed [](cite:cites Creswell_Creswell_2018) by letting people interact with the apps and asking them to give open-ended feedback on their experience.
For this, the users were first provided with a scenario explaining what they were supposed to do with the app.
This evaluation was split up into two parts, one for the FormGenerator app and one for the FormRenderer app.
Second, the user was asked to either generate a form according to the scenario using the FormGenerator or fill out an earlier generated form according to the scenario using the FormRenderer.
In both cases, the users remained access to the scenario while performing the task.
During the last step, an open-ended exit survey was taken which asked each participant to evaluate the app e.g. by comparing the application they had employed during the study with a traditional app like Google Forms.

##### Participants

Potential participants were directly contacted by the author.
19 people participated in our study. The FormGenerator app was evaluated by 8 participants. The FormRenderer app was evaluated by 11 participants.
For the first group, only people with some technical background were asked to participate in this evaluation. That is because the FormGenerator also targets more technically proficient users just as creating a form with Google Forms is also not meant for everyone.
To make sure this requirement is satisfied, computer science students were mostly targeted as participants for this part.
The 11 participants for the FormRenderer user study were people both with and without technical backgrounds with their ages ranging from 18 to 52 years.
This lies in line with the target group of this and other similar traditional applications (according to Statista, in 2021, 87.2% of worldwide internet users were aged between 18 and 54 [](cite:cites petrosyan2023distribution)) because we have to assume that the users of the app can already work with a computer and the Web.

##### Data

For the FormGenerator app, the users are provided with a list of bindings that they could use to create the form.
Here, the assumption is made that users interacting with this app would have some knowledge of Linked Data and the Semantic Web.
For the FormRenderer app, first, the conversion rules to go from the form description vocabulary to the form rendering app vocabulary (Solid-UI) exist and are defined in the FormRenderer app. This is done by providing the URL to the conversion rules resource by using the `?rules=` query parameter (which then automatically fills in that input field).
Second, the form description resource exists and is accessible by the FormRenderer app. This is done by providing the URL to the form description resource by using the `?form=` query parameter (also automatically filling in that input field).

Make sure "bindings" is explained somewhere earlier.
{:.todo}

##### Tasks

The tasks are kept simple to scenarios that we modeled to mimick normal day tasks.

Double-check: I've now removed the link to the user study scenarios appendix. No link is okay?
{:.todo}

#### Threats to Validity

As with any study, our evaluation carries threats to validity. We identified following external and internal threats [](cite:cites Creswell_Creswell_2018).

###### External Validity Threats

*Interaction of selection and treatment.*
This threat concerns the generalization to individuals in other settings.
All participants were recruited from Belgium and most of them are students at Ghent University, thus the findings might not be generalizable to a more general population.
However, we do assume that users of the form editing have more technical knowledge so this lies in line with our intentions, for the form usage we also assume that the user has some basic knowledge about working with a computer and the Web.

###### Internal Validity Threats

*Selection.*
This threat concerns the selection of participants who have certain characteristics that predispose them to have certain outcomes.
All participants were recruited from Belgium and most of them are students at Ghent University.
Most of them have a certain technical knowledge, but this is intentional as it is a prerequisite for the form editing part of the user study.
To mitigate a selection bias some participants not studying at Ghent University were also recruited, especially for the form usage part of the user study.
Additionally, participants from different ages were contacted.
The participants of the form editing part were all provided with possible bindings in an attempt to give them an equal knowledge of Linked Data according to the prerequisites.



#### Results

The feedback received from the open-ended interview is summarized below.
Just like the user study itself, the results are split up in two parts for the two different apps.

##### FormGenerator

The feedback that was received from these users was that the app was easy to use, especially because of the drag-and-drop functionality.
Also, the ability to reorder the fields by the use of drag-and-drop was seen as a nice feature.
However, some noted that it would be helpful to also be able to drop a field directly in between two other fields.
Multiple respondents mentioned that it would be nice to have a live preview of the form while creating it.

Even with all the positive experiences, the users did not like the fact that they had to use the bindings to create the form.
They did not understand what these bindings were and even though the list of bindings they could use was provided, some expressed difficulties in finding the right binding for the right field.
They rightly noted that as a restaurant owner, they don't want to know what bindings are.
Additionally, after mistyping the binding, someone expressed the wish to have some sort of validation or auto-completion on the bindings to make sure that the binding is correct.
While this would be a nice feature to have, this would require having all bindings be defined and then having the app check if the binding is correct.
For cases where the binding definition does not exist, e.g. when the `ex:` namespace is used, this would not be possible. 
By just returning a warning message when the binding is not correct, the user can still continue to create the form, so this should not be a big issue.
Next to bindings, the choice of vocabulary was also confusing for the users. They did not understand why they had to choose between SHACL, Solid-UI, and RDF-Form and on what this choice was based.
This is a valid remark as this choice is not based on anything and is just a remnant of the initial idea to have the FormGenerator app be able to generate forms based on different vocabularies.
However, this option could still be useful for people with more technical knowledge who want to create a form based on a specific vocabulary.

When building a form for the SHACL vocabulary, marking a field as required and allowing multiple answers is done by specifying the `sh:minCount` and `sh:maxCount` properties.
Asking users to enter the "min count" and "max count" for a field was confusing to them because they did not know what it meant.
Lastly, some people noted that they expected the possibility to enter a radio button field to be able to select the score for the review.
The initial idea was that this should be defined using a dropdown field, but using a radio button field would indeed be more intuitive for the user.
As these apps are just a proof of concept with only a limited amount of field types implemented to show the feasibility of the proposed architecture, the radio button field is one of the field types that has not been implemented yet.
However, this is something that should be added in the future when building a more complete version of the FormGenerator app.
Therefore, this point of feedback was, even though it was a valid remark, not considered a negative point for the FormGenerator app.
Overall, the feedback on the FormGenerator app was positive and 6 out of the 8 users were able to create the form without any issues besides the difficulties with the bindings.
Note however that only users with some technical background were asked to participate in this evaluation.
A better way of handling the bindings more abstractly is something that should be considered for future work.

##### FormRenderer

The feedback that was received from all the participants of this task was that the app was straightforward to use, easy to use, and clear.
There were no real critical issues mentioned, as to what the users get to see, it is a very simple app that does what it is expected to do.
Extra points for improvement given by the users were the idea of automatically hiding the input panel when the required input fields were already filled in via the URL query parameters to reduce the amount of technical information shown to the user.
After all, it does not make sense to show the input fields for the form description resource and the conversion rules if you send it to someone who just wants to fill in the form specified by the sender.
Furthermore, someone noted that they expected a multi-line text field to be used for the review field instead of a single-line text field. 
However, this was a consequence of the fact that the form description was built using the SHACL vocabulary and the SHACL vocabulary does not allow one to define a multi-line text field.
This also immediately shows empirically by people that SHACL is a vocabulary made to express validation and not to describe the display part, as pointed out earlier.
In the case of using a vocabulary to describe the display part, an ontology made for that purpose should be used, such as Solid-UI.
Some mixed feedback was given on the date field. Some people liked the fact that the date field already had the separating dashes in it, while others did not like that they had to click another time on the calendar icon to be able to enter a date via the popup calendar.
Furthermore, one person noted that it was unclear what the Subject URI was for, and even though for people without that knowledge there is always at least one valid suggestion that can be used, it can be confusing because they do not know what to choose.
Besides that, the users did not notice that the app was using Solid and Linked Data behind the scenes and this is exactly the goal of the FormRenderer app.
People who were given a form described using the SHACL vocabulary were unaware that schema alignment tasks were being performed behind the scenes.
Lastly, one person noted that a "Copy URL" button next to the load button, after you entered the input fields, would be a nice addition to the app.
To conclude, the feedback on the FormRenderer app was positive and all the participating users were able to fill in the form without any issues.
The app was straightforward and users did not realize that Solid and Linked Data were involved behind the scenes.
This is a good thing as it means that the app is easy to use for people without any knowledge of Solid and Linked Data.
