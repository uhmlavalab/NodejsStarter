# NodejsStarter

Minimum(kinda) amount of files to start a node webserver.

This repo contains the following files:
	README.md 		-	This file.
	package.json 	- 	Contains meta data for the webserver and lists the node library dependencies.
	server.js 		- 	The server file.

And folders:
	node_modules 	- 	Contains node libraries.
	src 			- 	Contains additional support files for the server.
	public 			- 	Contains :
							favicon.ico 	- 	Image that shows up in the browser tab / bookmark.
							index.html 		- 	The "main" page that is served.
							src 			- 	Folder containing additional .js files for index.html
												websocket.io.js 	- 	Library to setup websocket communication from client to server.
												index-wsio.js 		- 	Holds the page functions to data trasnfer over websockets.


##To run the server
Install Nodejs
Get this repo
Open cmd/terminal/etc and navigate to folder containing server.js
Use command "node server.js"

Server should be started and by default is listening on port 9001.
Use a webbrowser and connect to "localhost:9001" to double check.
Other computers can connect to you server using ip.

The page is setup with a basic example of websocket data sending.
Type into the text box, click send, and the server will get the text.
After getting the text it should send back a packet to confirm what it got.

##Next steps

Want to add more pages?
 - Drop more stuff in the public folder.

Want to change the port?
 - Open the server.js file. At the top of the file is a line with:
 	webVars.port 		= 9001;
 	Simply change the number on the right.
 	Keep in mind that typically you should not use port 1024 or below, they are commonly used by the system.

The interesting stuff, how to use websockets?
 - Take a look at the server.js file. Search for comment "//create ws listener"
 	That starts the websocket listener
 	Whenever a connection is attempted, the function openWebSocketClient() is called.
 	There are a variety of ways to establish a websocket, so that function, will setup one listener, "addClient"
 	A client must send a packet marked as "addClient" to do further communication.
 	When the client does so, it activates the wsAddClient() function on the server, which establishes the next of listeners.
 	As of this writing there is only the "consoleLog" listener setup.
 	Should the client send a packet marked as "consoleLog" the wsConsoleLog() function will be called.
 	To add more websocket functionality first start with the consoleLog format.

 - On the client side, there are two things to consider. What should trigger a data send, and how should it be labeled.
 	For example, if clicking a button should send data, the button needs to be implemented.
 	But if there are three buttons that each send data, they not only need to be implemented (probably through html tags) but the contents of the data must be considered as well. Are they distict and independent? Or are they related? Depending on how the data relates, you may need to send packets with different labels, or packets with the same label, but different data.
 	As of this writing, the index.html page has one button implemented through tags, and when clicked will call the sendInbox() function.
 	The sendInbox() function will make a web socket packet labled consoleLog and include the value of the div as packet data. Then sends it to the server.
 	










