# Peer to Peer BlockChain Protocol

**This is the protocol for the implementation of peer to peer blockchain with proof-of-work.**

**The goal of the project is to implement a blockchain peer-to-peer system inspired by Bitcoin called CheeseCoin System.**

**The building blocks of the protocol includes the following elements.**

# Table of contents
1. [Tracker Program](#tracker-program)
2. [Member Program](#member-program)
3. [Interaction Between Tracker and Member Programs](#interaction-between-tracker-and-member-programs)
4. [Interaction Between Members](#interaction-between-members)
5. [Blue-Cheese](#blue-cheese)
6. [Cheese](#cheese)
7. [Cheese-Stack](#cheese-stack)
8. [Proof-Of-Work](#proof-of-work)
9. [Data-Format](#data-format)

## Tracker Program
* A tracker is a server in this peer to peer network.
* The tracker keeps track of IP address of the active members and their port numbers.
* The  members connect to the tracker with respect to the port number and IP address of the tracker (where the tracker process is actively running).
* When a new member connects to the tracker, 
	* Tracker sends a sublist of the other members that are active and waiting for connection to other members. 
	* The tracker sends a random list of active members connected to it, if there are less than 10 active members.
	* If the number of active members connected to the tracker is greater than 10 then the tracker sends the sublist  that contains at most 10 active members to connect with. 

## Member Program
* A member gets a sub-list of the peers(other members) from the tracker and it gets connected to them and it will get updated automatically if anyother peers disconnects from the network.
* Member program will be awaiting for connections from other members
* Each member has a copy of [cheese-stack](#cheese-stack) stored in its hard disk.
* Member can update the cheese-stack after doing the [proof-of-work](#proof-of-work).which will be broadcasted to other members in the network.
* Each member of the network agrees on the protocol of the longest valid cheese-stack.
* The member program accepts and shares information (download and upload) at the same time.
* If a member creates new [cheese](#cheese), it has to do the proof of work which includes D**00** (D is the difficulty to find the starting two zeros) to be found at the beginning of the hash it created by using nonce function to make it a valid cheese. 

## Interaction Between Tracker and Member Programs
* A tracker-member connection is a TCP connection.
* The Tracker listens to the request for the connection from the new members by openning its port to accept new connections and this connection is established when a member connects with the port number and the IP address of the tracker.
	* Display message from the tracker before new connections
		* Tracker waiting for new connection.
	* When new member gets connected to the tracker
		* It displays,
			* Member IP address.
			* Member port number.
			* Total number of active connections.
* Member requests tracker to send a list of active members to get connected with and in response the tracker sends a sub-list of active members.

```sh
	Request: [IP address, Port number]
	Response: [Member IP address, Port number]
```

* Tracker removes the members from its list if the members are inactive. 

## Interaction Between Members
* Each member gets a sublist from the tracker and it connects to other members and their connection is established through TCP connection.
* Member requests for a the cheese to other member
```sh
	Request: [Cheese]
	Response: [Parent_Smell,Sequence_Number,Smell,Unit_of_Information,Nonce]
```
* A new member gets a copy of the latest valid cheese and it gets stored in the hard disk.
* The valid cheese is added to the cheese stack and this cheese stack is validated by the inbuilt function in member program and only longest cheese stack is valid as a global protocol to be followed.
* The member program has a synchronising function that checks the number of the cheeses in the cheese-stack of each member and synchronise it to every other member that doesn’t have the latest copy of cheese stack.

## Blue-Cheese
* It is the original cheese with following contents,

| Contents | Meaning |
| ---------|---------|
| Sequence_Number | 0 as predefined value |
| Smell | SHA1 hash generated from the unit of information|
| Unit_of_Information | Information about the transaction of CheeseCoin system |
| Nonce | Random number to validate the cheese, which generates the smell starting with two zeros |

## Cheese
* It is a unit of information stored in a distributed database and which is shared between the members in the network.
* A cheese contents following information,

| Contents | Meaning |
| ---------|---------|
| Parent_Smell | The hash of the parent chesse or the smell of the previous cheese|
| Sequence_Number | Unique number representing the number of ancestors |
| Smell | SHA1 hash generated from the unit of information |
| Unit_of_Information | Information about the transaction of CheeseCoin system |
| Nonce | Random number to validate the cheese, which generates the smell starting with two zeros |

## Cheese-Stack
* It is a collection of Cheese items.
* Cheese Stack can be represented as follows,

| Cheese_Stack |
|--------------|
| Blue_Cheese |
| Cheese_1 |
| Cheese_2 |
| Cheese_3 |
| Cheese_n |

## Proof-Of-Work
* It is a procedure to validate a cheese upon previous valid cheese in the cheese-stack.
* This process is carried out by finding a correct nonce for the unit_of_information in the cheese so that the hash of the smell starts with 00 (two zeros).

## Data-Format
| Contents | Data-Format |
| ---------|---------|
| Parent_Smell | String(20 Bytes)|
| Sequence_Number | Integer |
| Smell | String(20 Bytes) |
| Unit_of_Information | String |
| Nonce | Integer |
| IP_Address | String (4 Bytes) |
| Port_Number | Integer (2 Bytes) |
