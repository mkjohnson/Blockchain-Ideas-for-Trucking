# Comparing Enumerated to Logical Models for Blockchain Data Storage and Retrieval


# Definition of Terms

Enumeration - An enumeration is a complete, ordered listing of all the items in a collection. The term is commonly used in mathematics and computer science to refer to a listing of all of the elements of a set. Source: https://en.wikipedia.org/wiki/Enumeration

Logical - In a general business sense, logistics is the management of the flow of things between the point of origin and the point of consumption in order to meet requirements of customers or corporations. Source:https://en.wikipedia.org/wiki/Logistics

# Enumerated Model

Relies on pre-defined, ordered lists of specific elements
Elements may or may not be relevant to different industry sectors as all elements must be present in the set
Changes to the set would require updates and versioning
Devices and softwares writing to the blockchain would need to know the full set of elements in advance

In an enumerated model, all potential “states” would need to be known in advance by all parties writing to the blockchain. The enumerated set of elements (data) would require maintenance by an official body and as changes in business, technology, and customer demands may neccesitate changes in the enumerated sets. The enumerated model would require little change to existing back-end systems as the data comsumed is already purposed. Pre-determined “states” are recorded to the blockchain and no linking of transactions is required beyond tracing the historical recorded “states.”

# Logical Model

Relies on interpretation of cryptographically-linked data points as they happen
Meanings of elements are interpreted at the consumer level
Only the elements that are relevant to the consumer is consumed
Devices and softwares can write any kind of data to the blockchain and only need to follow a common data format standard

In a logical model, any device writing to the blockchain would only need to follow simple set of rules in how the entity records its data in the chain. Changes in business, technology, or customer demands would only affect interested parties (i.e. a truckload carrier does not need to know about changes in air freight or rail) and only the data format would need to be maintained. 

The logical model would likely require a complete re-write of most back-end systems as these systems will need to be able to consume data directly from the blockchain, linking many individual data points through the transaction structure of the blockchain to derive the current or historical “state” of the system.

