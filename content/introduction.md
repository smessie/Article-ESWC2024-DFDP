## Introduction
{:#introduction}

Web forms are a part of our daily lives, whether we are taking a survey, filling out shipping information for an online order, or filling out an administrative request.
If one needs a similar form to one that already exists, created by someone else or using another application, one has to develop a new form from scratch, without the possibility to start from the existing one and adapt it to one's needs.
Moreover, one cannot automatically prefill the similar form with pre-existing data that was filled in once before.
In addition, the data will almost always be stored on the server of the service provider, and the user will not be able to access it again or choose to store it somewhere else (footprint).
Current web forms are meant to be used against one endpoint (1), often used for one (web) display (2), with one particular workflow in mind (3), without a means to send and receive the data in another way (4).
This means that when submitting a form, data will always be sent to the same location, and the user won't have any influence on where the data is being stored (1).
Each application typically has a custom-built, non-standardized API that is different from every other application, preventing interoperability.
Second, filling out a form using an alternative environment, such as the command line, or even using a different website because you like the interface more, won't work.
Furthermore, form applications designed for customers to input their shipping information during a purchase cannot usually be repurposed to e.g. allow them to submit a support request (3).
Fourth, reusing data across multiple applications is not feasible because data from one application can not be written or read by another.
A first requirement for solving this problem is to decouple the data from the application.
To accomplish this, [Solid](cite:cites solid) is used.
Even after the issue is resolved and data reuse between applications becomes possible, the data format needs to be independent of the application, i.e., different applications should be able to use the same form description, even if they use different languages.
Only then the data and the application will be fully decoupled, as it cannot be assumed that all applications will use the same language to define data.

To tackle this problem, this paper introduces a solution by looking at Solid web forms as a whole of 3 separate parts: *display*, *validation*, and *reasoning*.
The display part defines how the form should look element-wise. The validation part defines the expected data structure.
Lastly, the reasoning part describes what to do with the filled in data at certain events such as submission.
These 3 parts provide a fully declarative description of the form, leaving no assumptions to be made by the application.
With the use of [Solid](cite:cites solid) and Linked Data, several solutions have been proposed, but none of them fully describe a declarative form semantically from elements to actions.
An exception to this is the [Design Issue authored by Berners-Lee](cite:cites berners-lee_linked_2019) and the [blog post on *Shaping Linked Data apps* written by Verborgh](cite:cites shapes). However, these works are solely theoretical approaches to the problem.
In addition, to fully decouple the description from the application, schema alignment is required to map the description to the vocabulary of the application.
