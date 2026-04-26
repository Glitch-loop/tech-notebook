API implies the effort of planning your API, here you standardize the responses of the API and creates the endpoint in such way that helps the team to develop easily while leverage the usage with the client.

### What do you standardize?
- Endpoints
- Methods
- Resources.

### What do you achieve if you standardize your API?
You get an API:
- Easy to use.
- Adaptable.
- Testable.
- Well-documented.

In addition, take the time for standardize your API helps you to build a an effective ***API governance strategy***.

## Approaches for the API design

### Inside-out API

Refers to create an API for an existing backend, this approach is useful when you already have work done, the downside is that you "expose" the service from the backend approach which in some cases, this can be problem with regarding to the clients, ending up with coupled applications.

### Outside-in API
This is the opposite of _inside-out approach_, in this approach you take first the perspective of the client, prioritizing the ease of use and flexibility. Although in both approaches you define the purpose of the service, in this one, you take into account "what the client needs" instead of just "offering a solution". At the end, with this approach you get a loosely coupled API, easier to maintain and evolve.

### Agile API design
This encourages to take the _outside-in approach_ for designing, and implementing using the Agile philosophy. In this approach you accept to work with an incomplete spec, having in mind that each iteration you might have changes.
This approach emphasize on flexibility, collaboration and responsiveness.


### Key stages of API design
**1. Determine what the API is intended to do.**
Here you define what the API will do. What is the purpose and the value it will bring to the clients.

**2. Define the API contract with a specification.**
Once you have defined the purpose of the API it's moment of defining the contract, how the API should respond? The level of abstraction and encapsulation.

**3. Validate your assumptions with mocks and tests.**
This step is specially important, basically it is to test the "idea" before implementing, in this way you ensure you are creating the right thing. Saving time and resources. 

**4. Document API.**
Document design decisions, considerations and why this was built in that way.


### Design patterns
- ***Request-response:*** Client sends a request, server responds with a response.
- ***Pagination:*** Sent the information in chunks and providing a way to retrieve more information as needed.
- ***Rate limit:*** Limit the usage to the client.
- ***API authentication:*** Have an authentication, restrict access to unauthorized user.
- ***Webhooks:*** Allows APIs to push real-time updates to client.

### Best practices
- ***Prioritize consistency***
This means to have conventions in the API. For instance, having a naming convention for endpoints and resources.

- ***Gather input from every stakeholder***
This encourage to have communication with stakeholders, this prevents misunderstandings, ambiguities and helps to build an API that actually solves the problem. 

- ***Understand the API's context and constraints***
Basically, be aware of the context on which the project is being developed, from the limitations until current context of the client, the team should be aware of the context that surround them. This helps to take better decisions.



Links:
- https://www.postman.com/api-platform/api-design/
- https://mayurashinde.medium.com/mastering-api-design-patterns-best-practices-for-building-robust-apis-ef950da4f169
- 
