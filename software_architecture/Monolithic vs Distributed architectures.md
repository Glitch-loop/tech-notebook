As a way to compare monolithic and distributed architectures, there was created a list comparing aspects of a system using both types of architectures.
This comparison was condensed into fallacies, to let know to the reader the concerns implied when a system change from monolithic to distributed system.

> ***Stamp coupling***: This type of coupling is presented in distributed architectures and refers when the communication of the services overhead the bandwidth this due to the amount of sent information. 
> 
> For instance, imagine a service that needs the information of user's profile (500kb), just the name (200bytes), and then it calls to another service having as result the entire profile, now imagen that this happens 2,000 times per second, that means each interservice call take 1GBps of bandwidth.


### Fallacy #1 The network is reliable

This refers to the confidence that the architecture has in the network, since the apparition of networks, the industry has improved in such way that we consider as a matter of fact that there will always be a connection available for our system.

This is a problem because that not true, and in any moment the network can fail.
![[Pasted image 20260223081421.png]]

***The more a system relies on the network (as microservices), the more potential it has to become unreliable.**
### Fallacy #2 Latency is Zero

This might be true in `monolithic systems` on which time of response can be measured in micro even in nano seconds (all the process is happening in the same machine), but for `distributed systems` this is a fallacy.
![[Pasted image 20260223081445.png]]

In these fallacy, the author says that calls takes time to responded between services adding latency in the process, and this can be worse if the workflow of the request takes more time because of poorly implementations or even a heavy-duty petition.

This delay in response can create bottlenecks in the services.

### Fallacy #3 Bandwidth is infinite

How to solve it?
- Creating private RESTful API endpoints.
- Using field selectors in contracts.
- Using GraphQL to decouple contracts
- Using value-driven contracts with consumer-driven contracts.
- Using internal messaging endpoints.

The best way to solve this problem in distributed system is to ensure the services are transmitted only the necessary data.

### Fallacy #4 Network is secure

This fallacy points to those architects that believe the network is secure and it encourages that the architect put attention and effort for securing the service.
![[Pasted image 20260223082504.png]]

### Fallacy #5 The topology never changes

This refers to the overall network topology, including network devices (hub, firewall, switches, etc.).
Although nowadays, it seems the different providers of networking works seamlessly, the architect should take into account this aspect of the system and this become relevant if you are on distributed systems.

![[Pasted image 20260223083236.png]]

The author put as example an scenario on which the system was breaking because services were timing out in production, the application was working as it used, but the problem resided into a ***minor upgrade in the network.***

### Fallacy #6 There is only one administrator

This refers that in organizations (big companies) there is not only one administrator for all.  

![[Pasted image 20260223083440.png]]

To mitigate this concern, author suggests that the architect should be concern of the structure of the company what who is in charge of key positions.

### Fallacy #7 Transport Cost is Zero
This refers to the believe that API calls doesn't have any transport cost, this is in part thanks to the efficiency that network has reached, but in reality, there is a hidden cost that implies network devices, standards and other concerns that in a glimpse it seems that doesn't affect `directly` to the cost, but that it an `indirect` has impact in how the system works.

![[Pasted image 20260223084539.png]]

### Fallacy #8 Network is homogenous

This fallacy points to the believe that the network is built in the same way (same topology, same provider, same devices and same standards) but the truth is that there is a big fallacy.

![[Pasted image 20260223084723.png]]

It's true that over time providers has standardized many aspects of how networks should operate and connect to each other, but at the end, devices are manufactured by different providers.

### Fallacy #9 Versioning is easy

This refers to how your team and you will handle the versions of the project. Being specific, in the case of distributed systems, how you will handle the versioning of the services.
Here the author shows question to deep in the topic:

- Should the team version at the individual service level or for the whole system?
- How far should the versioning reach? What portion of the architecture will need to support it?
- How many versions should the team support at any given time? (Some teams accidentally find themselves honoring dozens of different versions for different purposes).
- Should the team deprecate older versions at the system level or services by service?

### Fallacy #10 Compensating updates always work

> ***Compensating updates***: This is an **architectural pattern** in which some mechanism (like an Orchestrator service) make sure that several related services all update jointly. If they don't, the orchestrator reverses the update.

Many architects consider that compensating updates always will work, ignoring that this service can fail or changes inside the project may affect on how the pattern could behave.

### Fallacy #11 Observability is option (for distributed architectures)

Observability (logging) can be useful in monolithic architectures but in distributed systems it's vital to ensure the traceability of how the system behaves.

Having the ability of seeing how the system behave is critical for understanding bugs, problems at moment of connection, and above all, to understand how the system behave.


