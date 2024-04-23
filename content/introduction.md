## Introduction
{:#introduction}

Web forms are a part of our daily lives: taking a survey, filling out shipping information for an online order, or filling out an administrative request.
End-users regularly have to re-enter the same data, without the ability to prefill a similar form with pre-existing data.
In addition, the data will almost always be stored on the service provider's server, and the end-user cannot access it again or choose to store it somewhere else.
If an end-user requires a form similar to an existing one, created by someone else or with another application, they will often have to build a new one from the ground up without the ability to copy and modify an existing form.

Current Web forms are meant to be used (1)&nbsp;with one endpoint, (2)&nbsp;for one (Web) display, (3)&nbsp;with one workflow in mind, and (4)&nbsp;without a means to send and receive the data in another way.
First, when a form is submitted, the data is sent to the same location, and the user has no control over where the data is stored.
Typically, the application developer decides where and how to store the data --&nbsp;resulting in poor data control for users&nbsp;[](cite:cites berners-lee_three_2017)&nbsp;-- and
each application has a custom non-standardized API --&nbsp;hindering operability between applications&nbsp;[](cite:cites sambra2016solid).
Second, during form filling, it is not possible to use an alternative environment, with disparate display contexts, or to opt for a different website due to a preferred interface.
Such an alternative environment may be subtle (e.g. a dedicated mobile version, or a version that integrates seamlessly into a company's ecosystem).
For the sake of clarity, we will use an extreme example of a command line and a Web view to illustrate this problem in the remainder of the paper. 
Third, form applications designed for one specific use case cannot typically be repurposed for another, e.g.
a shipping information form for customers during a purchase cannot usually be repurposed to submit a support request.
Fourth, it is not possible to reuse data across multiple applications as data from one application cannot be written or read by another.

A requirement for solving these problems is decoupling the data from the application.
Solid is a specification for decentralized data storage that is decoupled from the application.
This allows the form description to be stored separately from the form renderer application, which in turn improves end-user control over their data.
Several solutions have been proposed using [Solid](cite:cites solid,sambra2016solid) and Linked Data, but none of them fully semantically describe a declarative form from elements to actions.
A couple of notable exceptions exist&nbsp;[](cite:cites berners-lee_linked_2019,shapes),
but these works are mainly theoretical approaches to the problem.

We introduce the _Declarative Form Description Pipeline_ (DFDP), looking at forms as 3 parts: *display*, *shape*, and *reasoning*.
In the DFDP, a *form generator* outputs the form description that serves as input to a *form renderer*.
*Display* defines how the form elements should look, *shape* defines the expected data structure, and
*reasoning* does footprint and schema alignment.
We use a *footprint* to describe what to do with the filled-in data at certain events (e.g. submission).
These 3 parts provide a fully declarative description of the form.
To fully decouple description from application, the application needs to understand any form expression vocabulary.
This necessitates schema alignment to map the description to a vocabulary the application understands, and removes the assumption that all applications will use the same language.

In the context of dataspaces, declarative form descriptions demonstrate their relevance by complementing the existing well-defined dataspaces data model with a declarative definition of the form as an interface that prompts the user for data input.
For instance, within the health dataspace, each hospital can use its own form for medical data entry.
By embedding semantics into the inserted data, alignment across all hospitals' data can be achieved.

The paper is structured as follows.
We first discuss related work ([](#related-work)) and present a motivating example and requirements ([](#requirements)).
We then introduce the architecture and discuss its implementation ([](#architecture) and [](#implementation)).
We evaluate in [](#evaluation) 
and present conclusions and future work ([](#conclusion)).
