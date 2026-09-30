# Let's begin: Mock Interview 1

Question 1 of 12

Resume deep dive

## Explain the architecture of a custom iOS framework you developed.

Imagine you're speaking to an Expedia Group senior iOS engineer.

You mentioned building custom frameworks for reuse across multiple OTT applications.

Cover these points in your answer:

* What problem did the framework solve?

* How did you divide the framework into components or modules?

* How did the host application communicate with it?

* How did you manage dependencies and avoid tight coupling?

* How did you test it and handle versioning?

Answer based on a real framework you worked on. You don't need to cover every point immediately; I'll ask follow-up questions.

## Answer :- 
"While developing multiple OTT-based learning applications, I identified several features that were common across projects. Instead of implementing and maintaining the same functionality separately in every application, we developed custom iOS frameworks to promote code reuse and maintainability.
We created reusable modules for features such as Search, VideoPlayer, and Test Attempt. These modules could be integrated into different applications, reducing duplicated implementation effort and making it easier to maintain common functionality.
On the host application side, we used dedicated manager classes to simplify integration and provide a convenient way for the application to interact with these modules.
The overall goal was to make common features reusable, simplify integration across projects, and improve long-term maintainability."

## 2. Area what Need to be look out for above Answer ?
- What the interviewer needs to hear
- Problem statement : What specific duplication or maintenance problem did the framework solve?
- Architecture : How were responsibilities divided within the framework?
- Public API : How did the host app use the framework's functionality?
- Dependencies : How did you manage dependencies between the framework and host app?
- Testing : How did you verify that the framework worked across different applications?
- Versioning : How did you manage changes without breaking existing integrations?
- 
The last three areas weren't covered in your answer. That doesn't mean you haven't done them; we just need to establish the details.

## 3. A stronger interview answer

Here is a polished version based only on the experience and examples you've shared. I've kept the implementation details general rather than inventing technical decisions.

Sample answer

"While developing multiple OTT-based learning applications, I identified several features that were common across projects. Instead of implementing and maintaining the same functionality separately in every application, we developed custom iOS frameworks to promote code reuse and maintainability.

We created reusable modules for features such as Search, VideoPlayer, and Test Attempt. These modules could be integrated into different applications, reducing duplicated implementation effort and making it easier to maintain common functionality.

On the host application side, we used dedicated manager classes to simplify integration and provide a convenient way for the application to interact with these modules.

The overall goal was to make common features reusable, simplify integration across projects, and improve long-term maintainability."

Copy sample answer

This is a clearer answer, but for a Senior iOS Engineer interview, we need to go beyond the benefits and explain the actual technical design.

## Question 2

Technical follow-up

## How did your VideoPlayer framework communicate with the host application?

Suppose the VideoPlayer framework is integrated into three different OTT applications. Each application may have its own UI, navigation, and playback-related requirements.

Explain how you designed the interaction between the framework and the host app.

Consider these points:

* How did the host application initialize the player?

* How did it pass video URLs or playback configuration?

* How did the framework communicate events such as playback started, paused, completed, or failed?

* Did you use delegate protocols, closures, callbacks, or manager classes? Why?

## Answer :
"We developed a reusable VideoPlayer framework to support multiple OTT applications with different UI requirements, video URLs and product-specific configurations.
Each product has its own Organization ID. We use enums to represent the relevant product configurations, while the other required data is passed through models. The host application uses the manager and router classes provided by our framework to simplify initialization and integration.
We keep the playback event-handling logic inside the framework so that the host applications do not need to manage the internal player implementation. We expose only the necessary delegate methods, such as callbacks for updating the last playback information.
We also use closures where callback-based communication is useful. For example, when playback progress or viewing time needs to be reported periodically, a closure can provide the updated information to the relevant component.
This approach keeps the framework's responsibilities separate from the host application's responsibilities, reduces duplicated integration logic, and allows us to reuse the same playback functionality across different products."
