## Introduction
{:#introduction}

Web forms are a part of our daily lives, whether we are taking a survey, filling out shipping information for an online order, or filling out an administrative request.
End-users regularly have to re-enter the same data again, without the ability to prefill a similar form with pre-existing data.
In addition, the data will almost always be stored on the service provider's server, and the end-user cannot access it again or choose to store it somewhere else.
If an end-user requires a form similar to an existing one, created by someone else or with another application, they will often have to build a new one from the ground up without the ability to copy and modify an existing form.

Current Web forms are meant to be (1) used against one endpoint, (2) often used for one (Web) display, (3) with one particular workflow in mind, and (4) without a means to send and receive the data in another way.
First, this means that when a form is submitted, the data is always sent to the same location, and the user has no control over where the data is stored.
The application developer is left to decide where and how to store the data, resulting in poor data control for users [](cite:cites berners-lee_three_2017).
Each application typically has a custom-built, non-standardized API, hindering operability between applications [](cite:cites sambra2016solid).
Second, it is not possible for form filling to use an alternative environment, like the command line, or to opt for a different website due to a preferred interface.
Third, form applications designed for one specific use case cannot typically be repurposed for another.
For example, a form for customers to provide their shipping information during a purchase cannot usually be repurposed to e.g., allow them to submit a support request.
Fourth, reusing data across multiple applications is not possible because data from one application cannot be written or read by another.

A requirement for solving these problems is to decouple the data from the application.
With the use of [Solid](cite:cites solid,sambra2016solid) and Linked Data, several solutions have been proposed, but none of them fully describe a declarative form semantically going from elements to actions.
A couple of notable exceptions exist [](cite:cites berners-lee_linked_2019,shapes),
but these works are mainly theoretical approaches to the problem.
Solid is a specification for decentralized data storage that is decoupled from the application.
This allows the form description to be stored separately from the form renderer application, which in turn improves end-user control over their data.

This paper tackles this problem by introducing a _DFDP (Declarative Form Description Pipeline)_ by looking at Web forms as a whole of 3 separate parts: *display*, *shape*, and *reasoning*.
In the DFDP, a form generator outputs the form description that serves as input to a form renderer.
The display part defines how the form should look element-wise. The shape part defines the expected data structure.
Lastly, the reasoning part exists of footprint and schema alignment.
The term *footprint* is used to describe what to do with the filled-in data at certain events such as submission.
These 3 parts provide a fully declarative description of the form, leaving no assumptions to be made by the application.
In addition, the application needs to understand any vocabulary used to express the description to fully decouple the description from the application.
This necessitates schema alignment to map the description to the vocabulary the application understands, also removing the assumption that all applications will use the same language.

In the context of dataspaces, declarative form descriptions demonstrate their relevance by not only having a well-defined data model but also by declaratively defining the form as an interface to prompt the user for data input.
For instance, within the health dataspace, each hospital can use its own form for medical data entry. By embedding semantics into the inserted data, alignment across all hospitals' data within the dataspace can be achieved.

The remaining paper is structured as follows.
[](#related-work) discusses related work, followed by a motivating example and a discussion of the requirements in [](#requirements).
[](#architecture) introduces the architecture, after which we discuss its implementation in [](#implementation).
In [](#evaluation), our presented solution is evaluated.
Finally, we present conclusions and future work in [](#conclusion).
