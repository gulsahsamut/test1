# BlockChain Protocol

# Table of contents
1. [A](#A)

## Tracker Program
* A tracker is a server in this peer - peer network
* The tracker keeps track of IP address of the active members and their port number
* The  members connect to the tracker with respect to the port number and IP address of the tracker (where the tracker process is actively running).
* When a new member connects to the tracker, 
	* Tracker sends a sublist of the other members that are active and waiting for connection to other members. 
	* The tracker sends a random list of active members connected to it, if there are less than 10 active members.
	* If the number of active members connected to the tracker is greater than 10 then the tracker sends the sublist  that contains at most 10 active members to connect with. 

## Interaction between Tracker and Member Programs
* A tracker-member connection is a TCP connection
* The Tracker listens to the request for connection from the new members by openning its port to accept new connections and this connection is established when the member connects with the port number and the IP address of the tracker 
	* Display message from the server before new connections
		* Tracker waiting for new connection.
	* When new member gets connected to the tracker
		* It displays,
			* Member IP address
			* Member port number
			* Total number of active connections
* Member request tracker to send a list of active members to get connected with and in response the tracker sends a sub-list of active members

```sh
	Request: [IP address, Port number]
	Response: [Member IP address, Port number]
```
* Tracker removes the members from its list if the members are inactive 

## Member Program
* The member gets a sub-list of the peers from the tracker and it gets connected to them and if someone leaves it will get updated automatically
* Member program will be awaiting for connections from other members
* Each member has a copy of cheese stack stored in its hard disk
* Member can update the cheese stack after doing the proof of work .which will be broadcasted to other members on the network.
* Each member of the network agrees on the protocol of the longest valid cheese stack.
* The member program accept and share information (download and upload) at the same time.
* If a member creates new cheese, it has to do the proof of work which includes D**00** (D is the difficulty to find the starting two zeros) to be found at the beginning of the hash it created by using nonce function to make it valid cheese. 

## Interaction between Members
* The members gets the sublist from the tracker and connects to the members and their connection is established through TCP connection
* Member requests for a the cheese to other member
```sh
	Request: [cheese]
	Response: [Parent_Smell,Sequence_Number,Smell,Unit_of_Information,Nonce]
```
* A new member gets a copy a latest valid cheese stack and it gets stored in the hard disk.
* The valid cheese is added to the cheese stack and this cheese stack is validated by the inbuilt function in member program and only longest cheese stack is valid as a global protocol to be followed.
* The member program has a synchronising function that checks the number of the cheeses in the cheese-stack of each member and synchronise it to every member that doesn’t have the latest copy of cheese stack.

## Blue-Cheese
* It is the original cheese with following contents,

| Contents | Meaning |
| ---------|---------|
| Sequence | 0 as predefined value |
| Smell | SHA1 hash generated from the unit of information|
| Unit_of_Information | Information about the transaction of cheese-coin system |
| Nonce | Random number to validate the cheese, which generates the smell starting with two zeros |

## Cheese
* It is a unit of information stored in a distributed database and which is shared between the members in the network
* A cheese contents following Information,

| Contents | Meaning |
| ---------|---------|
| Parent_Smell | The hash of the parent chesse or the smell of the previous cheese|
| Sequence_Number | Unique number representing the number of ancestors |
| Smell | SHA1 hash generated from the unit of information |
| Unit_of_Information | Information about the transaction of cheese-coin system |
| Nonce | Random number to validate the cheese, which generates the smell starting with two zeros |

## Cheese Stack
* It is a collection of Cheese items
* Chees Stack can be represented as follows,

| Cheese_Stack |
|--------------|
| Blue_Cheese |
| Cheese_1 |
| Cheese_2 |
| Cheese_3 |
| Cheese_n |





