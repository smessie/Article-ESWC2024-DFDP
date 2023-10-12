## Introduction
{:#introduction}

<span class="comment" data-author="RT">The structure of the next sentence is good, but it's too concise. Let's elaborate in much more detail on each part. Also, that should probably come after talking about forms in general.</span>
Current web forms are meant to be used against one endpoint (1), often used for one (web) display (2), with one particular workflow in mind (3), without a means to send and receive the data in another way (4).
<span class="comment" data-author="RT">The following sentence is a bit too informal.</span>
We all use a kind of web form once in a while, that is because you take part in a survey, or maybe because you have to fill in some kind of request. 
When one needs a similar form to one that already exists, they will have to develop a new application from scratch <span class="comment" data-author="RT">Not really, if you use something like google forms.</span>, without the possibility to start from that existing one and adapt it to their needs.
Furthermore, the data will almost always be stored on the server of the service provider, and the user will not be able to access it again or choose to store it somewhere else (footprint).

To tackle this problem, this paper introduces a solution by looking at Solid web forms as a whole of 3 separate parts: *display*, *validation*, and *reasoning*.<span class="comment" data-author="RT">Why these 3 parts?</span>
With the use of [Solid](cite:cites solid) and Linked Data, several solutions have already been proposed, but none of them consider web forms as a whole of 3 separate parts <span class="comment" data-author="RT">Why should other solutions be split up into 3 parts? Instead, I would expect you to have some requirements for forms, and say that these existing solutions do not meet these requirements.</span>, except for the [Design Issue by Berners-Lee](cite:cites berners-lee_linked_2019) and the [blog post on *Shaping Linked Data apps* by Verborgh](cite:cites shapes) <span class="comment" data-author="RT">Reviewers could ask why you write this paper, if the problem has apparently been solved already. You probably want to say that they are only theoretical.</span>.
In addition, to fully decouple the description from the application, schema alignment is required to map the description to the vocabulary of the application <span class="comment" data-author="RT">The need for this is not clear. One could ask why app and form do not just use the same vocab.</span>.
This makes it possible to use the same description for different applications, even if they use different vocabularies.<span class="comment" data-author="RT">Aha, here you make the point. But this need (together with other needs) should come sooner, probably even before you talk about the 3 parts.</span>
This, along with the execution of the footprint tasks, is done using reasoning.<span class="comment" data-author="RT">Reasoning seems like an implementation detail, you probably don't need it here.</span>

Therefore, we propose an architecture that splits the Solid web forms into 3 parts and implements proof-of-concept applications to show how this can be done in practice.
<span class="comment" data-author="RT">Not sure if this is the right place to introduce RQs. Might be better to do that after related work, right before you dive into the details of your approach.</span>
In this paper, the following two research questions are examined:

- RQ1: How can machines be controlled in a declarative way to create forms for producing RDF in **multiple viewing environments** (such as the web and text-based via a command line)?

- RQ2: How can machines be controlled in a declarative way to perform **schema alignment and footprint tasks** by the use of reasoning? <span class="comment" data-author="RT">Not sure I understand the point of this RQ. Schema alignment and footprints are a means to an end, but what end is that? Same for reasoning.</span>

<span class="comment" data-author="RT">Is there no decoupling of storage and app requirement?</span>

Refer to different upcoming sections in paper
{:.todo}
