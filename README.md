# NetworkingProject1
A basic chatroom with TCP (server and client) and UDP (peer to peer) implementations

Protocol (TCP):
The program uses port number 2568 as a default and hostname Gunicorn
The first argument is ‘server’ or ‘client’
If client, the next argument is IP address
All integers are sent as a 4 byte integers
Client sends a 1 and then its username as a string 
All strings are sent with a prefix of its length and encoded into byte string
Server sends True as a bool if the username does not already exist
Server sends False as a bool if the username already exists
If the server sent False, the client quits
The server sends up to 10 recent messages to the client prefixing the list of 10 messages with its length. And every list within the list is prefixed with its length before being sent. The length of every sub-list will always be 3 (the time the message was received, the user that sent the message, and the content of the message) .
Clients send a 2 before sending strings
When a client sends a message to the server, the server sends the message as a string to all the connected clients

Protocol (UDP):
The program uses port number 23457 and hostname Gunicorn
The peer broadcasts their username with a 1 concatenated at the beginning as one whole string
All strings are encoded into byte strings
If they receive nothing back, they are the only peer
If a peer receives a 1, they send back the past 10 messages or at least as many as it has all as separate strings with a prefix of 2 for each string. If the username matches theirs they send back False and then the new client is rejected.
The new peer then stores these messages in their message history list.
Peers broadcast messages by sending a 2, the current time, their username, and then the content of the message all as one string.
