## Introduction
{:#introduction}

Web forms are a part of our daily lives, whether we are taking a survey, filling out shipping information for an online order, or filling out an administrative request.
Users regularly have to re-enter the same data again, without the ability to prefill a similar form with pre-existing data.
In addition, the data will almost always be stored on the service provider's server, and the user cannot access it again or choose to store it somewhere else.
If a user requires a form similar to an existing one, created by someone else or with another application, they will often have to build a new form from the ground up without the ability to copy and modify an existing form.

Current Web forms are meant to be used against one endpoint (1), often used for one (Web) display (2), with one particular workflow in mind (3), without a means to send and receive the data in another way (4).
First, this means that when a form is submitted, the data is always sent to the same location, and the user has no control over where the data is stored.
Each application typically has a custom-built, non-standardized API, hindering operability between apps.
Second, it is not feasible for form filling to use an alternative environment, like the command line, or to opt for a different website due to a preferred interface.
Third, form applications designed for customers to provide their shipping information during a purchase cannot usually be repurposed to e.g. allow them to submit a support request.
They are built for one specific use case.
Fourth, reusing data across multiple applications is not feasible because data from one application cannot be written or read by another.

A first requirement for solving these problems is to decouple the data from the application.
With the use of [Solid](cite:cites solid) and Linked Data, several solutions have been proposed, but none of them fully describe a declarative form semantically going from elements to actions.
An exception to this is the [Design Issue authored by Berners-Lee](cite:cites berners-lee_linked_2019) and the [blog post on *Shaping Linked Data apps* written by Verborgh](cite:cites shapes). However, these works are solely theoretical approaches to the problem.

This paper tackles this problem by introducing a DFDP (Declarative Form Description Pipeline) by looking at Web forms as a whole of 3 separate parts: *display*, *shape*, and *reasoning*.
In the DFDP, a form generator outputs the form description that serves as input to a form renderer.
To accomplish decentralization, the decentralized data storage technology [Solid](cite:cites solid) is used.
The display part defines how the form should look element-wise. The shape part defines the expected data structure.
Lastly, the reasoning part describes what to do with the filled-in data at certain events such as submission.
These 3 parts provide a fully declarative description of the form, leaving no assumptions to be made by the application.
In addition, the application needs to be able to understand any vocabulary used to express the description to fully decouple the description from the application.
This necessitates schema alignment to map the description to the vocabulary the application understands.
Only then will the data and the app be fully decoupled, as it cannot be assumed that all apps will use the same language to define data.

The remaining paper is structured as follows.
[](#related-work) discusses related work, followed by a motivating example and a discussion of the requirements in [](#requirements).
[](#architecture) introduces the architecture, after which we discuss its implementation in [](#implementation).
In [](#evaluation), our presented solution is evaluated.
Finally, we present conclusions and future work in [](#conclusion).
