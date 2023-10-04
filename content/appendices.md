## Appendices

### User Experience Scenarios
{:#scenarios}

The following scenarios were given to the participants to measure the user experience of the implemented applications. They explain how the participants should use the applications and what they should do.

#### Scenario 1: The Form Generator

> You have a restaurant and you would like to offer customers the opportunity to leave a **review** on the dishes they have eaten. 
> To do this, you create a **form** where the customer can enter the **name of the dish** along with the **date of visit**. 
> The review consists of a score between 1 and 3 ( 1★ - I didn't like it, 2★★ - It was tasty or 3★★★ - It was excellent). 
> In addition, provide an option to **substantiate their choice**.
> 
> At the top right, it is free to choose between SHACL, Solid-UI and RDF-Form. 
> This has no further importance in the construction of the form.
> 
> Since Linked Data is being used in the background, each field and also the form itself must contain a **binding** to link everything to existing data.
> This is done through the **binding** field.
> Below is a list of existing bindings that can be used.
> 
> - schema:Rating or http://schema.org/Rating 
> 
> - dc:title or http://purl.org/dc/elements/1.1/title 
> 
> - schema:ratingExplanation or http://schema.org/ratingExplanation 
> 
> - schema:ratingValue or http://schema.org/ratingValue
> 
> - ex:NotLikedIt or http://example.org/NotLikedIt 
> 
> - ex:LikedIt or http://example.org/LikedIt
> 
> - ex:LovedIt or http://example.org/LovedIt 
> 
> - schema:orderDate or http://schema.org/orderDate 
> 
> After the customer saves the review you want an **HTTP request** of **type PUT** to be sent to https://solid.smessie.com/thesis/forms/antwoord-x.ttl, for this the **text/turtle** Content-Type is used.
> Finally, you also want to redirect the customer to a **website of your choice** after completing the form.

#### Scenario 2: The Form Renderer

> You went to eat at a restaurant where they asked you to leave a review about the dish you ate. 
> In the form, enter a review about a dish of your choice (e.g., what you ate today or yesterday). 
> Then submit the form by choosing a subject URI of your choice for the data.
