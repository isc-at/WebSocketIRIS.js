~~~
 This is a coding example working on Cache 2018.1.3  
 It will not be kept in synch with new versions      
 It is also NOT serviced by InterSystems Support !   
~~~  

This is now the version compatible to IRIS unsing *IRIS Native API for Node.js*
Node / JavaScript have wide reputation to work as a WebSocket client.  
By using the IRIS adapter it becomes easy to control it and to consume the results as a   
Client for WebSocket Servers and to collect the replies in Caché, Ensemble, ..   

I used node-v10.15.1-x64.msi and intersystems-iris-native package

You provide a Global for input:

     ^WsockIn="wss://echo.websocket.org/"
     ^WsockIn(0)=6
     ^WsockIn(1)="Hello"
     ^WsockIn(2)="World !"
     ^WsockIn(3)="Robert"
     ^WsockIn(4)="is waiting"
     ^WsockIn(5)="for replies"
     ^WsockIn(6)="exit"

and with this echo server you get back a Global as output

     ^WsockOut(0)=6
     ^WsockOut(1)="Hello"
     ^WsockOut(2)="World !"
     ^WsockOut(3)="Robert"
     ^WsockOut(4)="is waiting"
     ^WsockOut(5)="for replies"
     ^WsockOut(6)="exit"

the server is controlled by ^ZSocketRun from IRIS  
     -1 => stop server and exit  
	     0 => wait for action  
      1 => sent to echo server  
                	^ZSocketRun(0)= echo server => "wss://echo.websocket.org/"  

The webSocket Servis is started vom OS commandline:  

     c:\user>node WeBSockerIRIS.js
          
you can follow the progress n console output

      C:\Program Files\nodejs\cache>node WsockIris.js

        *****************************
        *** no IRIS host defined ****
        Connect to IRIS on: localhost
Successfully connected to InterSystems IRIS.
        echoserver:  wss://echo.websocket.org/
        ** Lines to process: 6 **
        ********* next turn *********
        ******* Startup done ********

        * WebSocket Client connected *
        ****** Client is ready ******
Line: 1 text> 'Hello'
Received: 1 > 'Hello'
Line: 2 text> 'World !'
Received: 2 > 'World !'
Line: 3 text> 'Robert'
Received: 3 > 'Robert'
Line: 4 text> 'is waiting'
Received: 4 > 'is waiting'
Line: 5 text> 'for replies'
Received: 5 > 'for replies'
        *** wait 3sec for request ***
Line: 6 text> 'exit'
Received: 6 > 'exit'

        ******* lines sent: 6 ******
        *** replies received: 6 ****

        *** wait 3sec for request ***
        *** wait 3sec for request ***
        *** wait 3sec for request ***
        *** wait 3sec for request ***
        *** wait 3sec for request ***
        *** wait 3sec for request ***
        *** Client Service closed ***
