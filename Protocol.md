# BlockChain Protocol

## Tracker
* A tracker is a server in this peer - peer network
* The tracker keeps track of IP address of the active member and their port number
* The  members connect to the tracker with respect to the port number and the tracker IP address (where the tracker process is stored).
* When a new member connects to the tracker, 
	* Tracker sends a sublist of the other members that are active and waiting for connection to other members. 
	* The tracker sends a random list of active members connected to it, if they are less than 10 active members.
	* If the number of active members connected to the tracker is greater than 10 then the tracker sends the sublist  that contains at most 10 active members to connect with. 



