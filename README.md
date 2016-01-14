# NodejsStarter<br>
<br>
Minimum(kinda) amount of files to start a node webserver.<br>
<br>
This repo contains the following files:<br>
	README.md 		-	This file.<br>
	package.json 	- 	Contains meta data for the webserver and lists the node library dependencies.<br>
	server.js 		- 	The server file.<br>
<br>
And folders:<br>
	node_modules 	- 	Contains node libraries.<br>
	src 			- 	Contains additional support files for the server.<br>
	public 			- 	Contains :<br>
							favicon.ico 	- 	Image that shows up in the browser tab / bookmark.<br>
							index.html 		- 	The "main" page that is served.<br>
							src 			- 	Folder containing additional .js files for index.html<br>
												websocket.io.js 	- 	Library to setup websocket communication from client to server.<br>
												index-wsio.js 		- 	Holds the page functions to data trasnfer over websockets.<br>
<br>
<br>
##To run the server<br>
Install Nodejs<br>
Get this repo<br>
Open cmd/terminal/etc and navigate to folder containing server.js<br>
Use command "node server.js"<br>
<br>
Server should be started and by default is listening on port 9001.<br>
Use a webbrowser and connect to "localhost:9001" to double check.<br>
Other computers can connect to you server using ip.<br>
<br>
The page is setup with a basic example of websocket data sending.<br>
Type into the text box, click send, and the server will get the text.<br>
After getting the text it should send back a packet to confirm what it got.<br>
<br>
##Next steps<br>
<br>
Want to add more pages?<br>
 - Drop more stuff in the public folder.<br>
<br>
Want to change the port?<br>
 - Open the server.js file. At the top of the file is a line with:<br>
 	webVars.port 		= 9001;<br>
 	Simply change the number on the right.<br>
 	Keep in mind that typically you should not use port 1024 or below, they are commonly used by the system.<br>
<br>
The interesting stuff, how to use websockets?<br>
 - Take a look at the server.js file. Search for comment "//create ws listener"<br>
 	That starts the websocket listener<br>
 	Whenever a connection is attempted, the function openWebSocketClient() is called.<br>
 	There are a variety of ways to establish a websocket, so that function, will setup one listener, "addClient"<br>
 	A client must send a packet marked as "addClient" to do further communication.<br>
 	When the client does so, it activates the wsAddClient() function on the server, which establishes the next of listeners.<br>
 	As of this writing there is only the "consoleLog" listener setup.<br>
 	Should the client send a packet marked as "consoleLog" the wsConsoleLog() function will be called.<br>
 	To add more websocket functionality first start with the consoleLog format.<br>
<br>
 - On the client side, there are two things to consider. What should trigger a data send, and how should it be labeled.<br>
 	For example, if clicking a button should send data, the button needs to be implemented.<br>
 	But if there are three buttons that each send data, they not only need to be implemented (probably through html tags) but the contents of the data must be considered as well. Are they distict and independent? Or are they related? Depending on how the data relates, you may need to send packets with different labels, or packets with the same label, but different data.<br>
 	As of this writing, the index.html page has one button implemented through tags, and when clicked will call the sendInbox() function.<br>
 	The sendInbox() function will make a web socket packet labled consoleLog and include the value of the div as packet data. Then sends it to the server.<br>
 	<br>
<br>
<br>
<br>
<br>
