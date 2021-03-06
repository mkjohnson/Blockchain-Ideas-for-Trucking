# DDSAP
**Decentralized Data Standards Adoption Protocol - How to avoid the "EDI-ification" of the blockchain in transportation.**

**NOTE:** Everything in this set of documents will refer to specific scenarios in the transportation industry involving the use of EDI but this same methodology could be used in any industry. This is a work in progress and any part is subject to change. This set of documents assumes the reader to have a basic understanding of transportation and how a blockchain works.

**Background**

In transportation, we communicate with our shippers, receivers, and drivers through a never-ending variety of methods but the most prominent and problematic one is EDI. EDI is what I like to call the "Non-standard Standard." I often describe EDI as an agreed upon alphabet where everyone makes up their own words and sentence structure and then have translators in the middle. One of the reasons for this is what I call "Standards Drift". EDI includes a way to create a "mutually defined" qualifier and this is one of many areas where the problems come from. Where one transportation partner may transmit the pickup time in a G62 segment, another may create a mutually-defined qualifier "PT" and include the time as the reference comment in an N9 segment. Time formats, coordinate formats, even if a decimal value can contain a leading zero or not, are all dictated by the party requesting the data. This drift occurs because as an industry's needs change, and new data is needed to be passed between parties, the agreed upon standards cannot keep up. How can we allow new data standards to be created, and adopted at a speed that keeps up with the needs of the industry?

The problem in EDI is that it is up to the trading partners to specify how they want to receive that data and it is up to the carrier to comply with their customer's format. This happens because of a variety of reasons, poor programming, mis-trained end-users, or simply the datapoint didn't exist before the EDI standard was defined. Enter the blockchain.

**Solution**

Any agreed upon set of standards will obviously be baked into the protocol of the blockchain. A "starter set" of "datapoints" would be defined. For instance, if I were to want to record the temperature data of a refrigerated trailer, I would need some element to say, "Hey, this value is a temperature." By having an initial set of datapoint definitions, with a broad scope, and by leveraging the democratization of adoption of new standards, while at the same time, ensuring the uniformity of said standards, the problem of "Standards Drift" and the "EDI-ification" of any proposed blockchain protocol for transportation data can be avoided.

So, if we, as an industry, can come together and define an initial set of datapoints, we have a starting point. If there is an entity that says, "Hey, we need to define a new datapoint because this new technology needs to have a different definition that the others!" (let's say that we find out that now we need to track moisture in dry vans) an operating node (expand on this later) would be able to start signaling, "Hey, I have a new datapoint that I need to use and I want to call it 'DryVanHumidity' does everyone agree to this?" Then a broadcast is sent to all nodes, and now they are alerted to the request and can choose to either support adoption of the new data type or they can ignore the request. If a certain percentage of the hashing power on the network signals support, the new data type standard is adopted and everyone now knows the rules for that data type. No more mapping and, most importantly, no more "user defined" qualifiers.

**Defining Data**

To define a set of standards for data, we first must define what data is. Data is 5 things: Who, what, when, where, why. "How" is arguable, but if this protocol is created properly, the "how" can be reconstructed from all the datapoints related to the action the "how" would describe but let's get back to the 5 things:

  1) Who: What entity is recording this data? (Public key of sensor)
  2) What: What kind of data is this? (Number, text, etc)
  3) When: Timestamp of when data was entered into the blockchain.
  4) Where: The location the data was recorded.
  5) Why: The purpose of the data. (Temperature, speed, pressure, time, location, etc)

**Privacy Concerns**

To maintain privacy but still allow for the decentralization of the data and to define the purpose of the data, two more layers will need to be added: an ownership layer and an instruction (or intent) layer.

**Ownership Layer**

The ownership layer is what provides both the encryption of the data on the blockchain and the proof of ownership of the data. The ownership layer also will define a sub-set of visibility permissions for the public keys of other entities in the transaction and define what they can view and what they can add.

***IMPORTANT!** An immutable ledger cannot be edited, only added to. Mistakes could be corrected through transactions linked to the mistake that are appropriately signed by all parties involved and a transaction correcting the mistake could be added in a later block.*

**Instruction Layer**

The instruction layer is what defines the purpose of the transaction. "Payment", "Temperature Data", "Satisfying a condition of a smart contract," would all reside in this layer. It would say, "Hey, this temperature reading is just a datapoint." or "Hey, this payment sends the defined funds from wallet A to wallet B" or "Set the condition of Z smart contract - input 1 to 'true'." Nodes that are receiving these instructions would verify the signatures on the transactions and execute whatever action specified in the instruction through creation of a new transaction. (A EOF transaction may be needed here)

**Impact**

Now we're in a situation where the TMS is essentially a wallet. The shipper opens their wallet, enters their load as a transaction that engages a smart contract and waits until the conditions of the smart contract have been satisfied. The carriers would also have a wallet TMS interface but the functions of their wallet would be different (dispatch, loadboard, bidding, brokers, etc), all enabled by the ownership and intent layers. 

**Securing The Chain**

See [Proof-of-Transport](https://github.com/mkjohnson/DDSAP/blob/master/Proof-of-Transport.md)

Trucks will run miners. The only fair way I can think of to distribute hashing power and prevent a 51% (or 70%) attack on the network would be to "permission" hash power on the blockchain by having each vehicle's VIN be a validation key of some kind. The hashing power on the network would be controlled by trucking capacity and nothing else. Having a miner in a truck would require a constant internet connection. Most trucks already have this through their on-board telematics or ELD platform (or smart phone even). Because the TMS would signal that a tractor was under active dispatch, and both the shipper and receiver both confirm this, the hashing power of the miner in the tractor begins receiving transactions and running a PoW algorithm. A combination of sensors in the tractor, which have digital identities that are owned by the tractor (which has a digital identity) could provide additional proofs to be able to add a block and achieve consensus.

If every tractor runs a miner and must be under active dispatch, verified by a 3-way signature, for their hashing power to count, the hashing power of the network, and therefore security, is assured. The nodes will be able to check if the tractor solving the block was under dispatch through a mechanism similar to zcash (to be defined later, point is that the nodes can't be gamed) and if so, it can validate blocks. If not, any block solutions submitted from the tractor (linked to the parent node run by the company who owns the tractor) it will simply be ignored (and invalidated so that it can't be replayed).

If an attacker were to try to compromise the security of the chain, the attacker would have to purchase enough tractors with valid VIN#s to own at least 51% of all tractors, create fake loads that the attacker would have to get both the shipper and receiver to sign, dispatch these trucks and then they would have to actually drive them to the proscribed origins and destinations in the fake orders so try and fake a single transaction, which would be detected immediately. The point is, attacking the chain would be ridiculously expensive for little to no effect.

**Power Consumption Concerns**

PoW uses a lot of power, but tractors also produce a lot of wasted energy. A 120V DC-to-AC power inverter that is capable of supplying 1500W of power is standard in most tractors. Due to the nature of DC-to-AC conversion, the power is being consumed by the inverter if the 120V outlet has a load on it or not. Because of this, powering miners off of the diesel power plant, AKA engine, while a tractor is under dispatch and going down the road, instead o this PoW scheme wasting energy, it in fact captures normally wasted energy and puts it to use. I believe that if we powered the miners to secure the network with tractors, not only is this PoW scheme carbon-neutral, one could argue it is greener as computing power normally residing in individual data centers could be off-loaded to the tractors that are producing excess energy that is not currently being captured or used.

**Potential Issues**

A blockchain for recording data at this scale could potentially create trillions of datapoints. How to keep the size of the chain manageable.

 Thoughts include:
- Storing a hash of the data in the chain then sending the data over conventional means (FTP, AS2, etc). The receiving party could hash the same data and check it against the hash of the same data in the blockchain for a match. 
- A "pruning of the chain by consensus" by agreeing to establish a new coinbase at an agreed upon block height, then purge older records that are no longer neeed. 
