# BlockChain Protocol

## Tracker
* A tracker is a server in this peer - peer network
* The tracker keeps track of IP address of the active members and their port number
* The  members connect to the tracker with respect to the port number and IP address of the tracker (where the tracker process is actively running).
* When a new member connects to the tracker, 
	* Tracker sends a sublist of the other members that are active and waiting for connection to other members. 
	* The tracker sends a random list of active members connected to it, if there are less than 10 active members.
	* If the number of active members connected to the tracker is greater than 10 then the tracker sends the sublist  that contains at most 10 active members to connect with. 

## Tracker - Member
* A tracker-member connection is a TCP connection
* The Tracker listens to the request for connection from the new members by openning its port to accept new connections and this connection is established when the member connects with the port number and the IP address of the tracker 
	* Display message from the server before new connections
		* Tracker waiting for new connection.
	* When new member gets connected to the tracker
		* It displays,
			* Member IP address
			* Member port number
			* Total number of active connections
* Member request tracker to send a list of active members to get connected with and in response the tracker sends a sub-list of active member
<!-- 
| Request | Response |
| --------| -------- |
| IP, Port| IP, Port |
 -->
	
	Request: [ <Member IP address>, <Port number>]
	Response: [<Member IP address>, <Port number>]
	


