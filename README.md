TO RUN PYTHON FILE IN TERMINAL USE **python filename.py** command
# INDEX
### <a href = https://github.com/secaids/cn/#exp-1---stop-and-wait-protocol>Stop & Wait protocol</a>
### <a href = https://github.com/secaids/cn/#exp---2---sliding-window-protocol>Sliding Window protocol</a>
### <a href = https://github.com/secaids/cn/#exp---3---socket-programming>Socket Programming</a>
### <a href = https://github.com/secaids/cn/#exp---4---simulate-arp>Simulate ARP</a>
### <a href = https://github.com/secaids/cn/#exp---5---simulate-rarp>Simulate RARP</a>
### <a href = https://github.com/secaids/cn/#exp---6---simulating-ping-command>Simulating Ping Command</a>
### <a href = https://github.com/secaids/cn/#exp---7---simulating-traceroute-command>Simulating Traceroute Command</a>
### <a href = https://github.com/secaids/cn/#exp---8---echo-client-and-echo-server>Echo client & server</a>
### <a href = https://github.com/secaids/cn/#exp---9---chat-using-tcp-sockets>Chat using TCP sockets</a>
### <a href = https://github.com/secaids/cn/#exp---10---file-transfer-using-tcp-sockets>File transfer using TCP</a>

# Exp-1 - STOP AND WAIT PROTOCOL
## Algo 
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
6. Stop the program
## Client
```py
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
while True:
  i=input("Enter a data: ")
  c.send(i.encode())
  ack=c.recv(1024).decode()
  if ack:
    print(ack)
    continue
  else:
    c.close()
```
## Server
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
  print(s.recv(1024).decode())
  s.send("Acknowledgement Recived".encode())
```

![image](https://user-images.githubusercontent.com/118756330/205697276-08ecbc2d-3aeb-4ca6-ad52-6cb441d9fad3.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 2 - SLIDING WINDOW PROTOCOL
## Algo
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
6. Stop the program
## Cliet
```py
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
size=int(input("Enter number of frames to send : "))
l=list(range(size))
s=int(input("Enter Window Size : "))
st=0
i=0
while True:
    while(i<len(l)):
        st+=s
        c.send(str(l[i:st]).encode())
        ack=c.recv(1024).decode()
        if ack:
            print(ack)
```
## Server
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    print(s.recv(1024).decode())
    s.send("acknowledgement recived from the server".encode())
```
![image](https://user-images.githubusercontent.com/118756330/205697374-68980d18-f7eb-4d67-808e-eabf7f13bb9c.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 3 - SOCKET PROGRAMMING
## ALGO
### Server:
1. Create a server socket and bind it to port.
2. Listen for new connection and when a connection arrives, accept it.
3. Send server‟s date and time to the client.
4. Read client‟s IP address sent by the client.
5. Display the client details.
6. Repeat steps 2-5 until the server is terminated.
7. Close all streams.
8. Close the server socket.
### Client
1. Create a client socket and connect it to the server‟s port number.
2. Retrieve its own IP address using built-in function.
3. Send its address to the server.
4. Display the date & time sent by the server.
5. Close the input and output streams.
6. Close the client socket.
7. Stop.
## Client
```py
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA"};
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## Server
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
print(s.getsockname())
print(s.recv(1024).decode())
s.send("acknowledgement recived from the server".encode())
```
![image](https://user-images.githubusercontent.com/118756330/205697438-ab435383-b6d9-469c-bb9b-16c944626537.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 4 - Simulate ARP
## ALGO
### Client
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
### Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
## Client
```py
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA"};
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## Server
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
```
![image](https://user-images.githubusercontent.com/118756330/205697517-df25b447-c107-45c3-8462-23ad679d7c6b.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 5 - Simulate RARP
### Client:
1. Start the program
2. Using datagram sockets UDP function is established.
3. Get the MAC address to be converted into IP address.
4. Send this MAC address to server.
5. Server returns the IP address to client.
### Server:
1. Start the program.
2. Server maintains the table in which IP and corresponding MAC addresses are stored.
3. Read the MAC address which is send by the client.
4. Map the IP address with its MAC address and return the IP address to client.
## Client:
```py
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA"};
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## Server
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
```
![image](https://user-images.githubusercontent.com/118756330/205698076-97ec58e3-09bf-4739-a50a-9c68ae5406f9.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 6 - SIMULATING PING COMMAND
## Algo
1. start the program.
2. Include necessary package in java.
3. To create a process object p to implement the ping command.
4. declare one Buffered Reader stream class object.
5. Get the details of the server
    1. length of the IP address.
    2. time required to get the details.
    3. send packets, receive packets and lost packets.
    4. minimum, maximum and average times.
6. print the results.
7. Stop the program.
## Client
```py
import socket
from pythonping import ping
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
while True:
    hostname=c.recv(1024).decode()
    try:
        c.send(str(ping(hostname, verbose=False)).encode())
    except KeyError:
        c.send("Not Found".encode())
```
## Server
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter the website you want to ping ")
    s.send(ip.encode())
    print(s.recv(1024).decode())
```
![image](https://user-images.githubusercontent.com/118756330/205698135-737919b6-0710-442e-aa45-a3b96f8a7c8f.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 7 - SIMULATING TRACEROUTE COMMAND
## Algo
1. Start the program.
2. Get the frame size from the user.
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server, it will send ACK signal to client otherwise it will send NACK signal to client.
6. Stop the program
## Prgm
```py
from scapy.all import*
target = ["www.google.com"]
result, unans = traceroute(target,maxttl=32)
print(result,unans)
```
![image](https://user-images.githubusercontent.com/118756330/205698416-e373d6b0-6cb8-4705-bf3a-416fa86a6ed3.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 8 - ECHO CLIENT AND ECHO SERVER
## Algo
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server, it will send ACK signal to client otherwise it will send NACK signal to client.
6. Stop the program
## Client
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
  msg=input("Client > ")
  s.send(msg.encode())
  print("Server > ",s.recv(1024).decode())
```
## Server
```py
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
while True:
  ClientMessage=c.recv(1024).decode()
  c.send(ClientMessage.encode())
```
![image](https://user-images.githubusercontent.com/118756330/205698474-cbbc26a7-e4bf-4e26-b0b2-56dea0fcff50.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
# Exp - 9 - CHAT USING TCP SOCKETS
## Algo
1. Start the program.
2. Get the frame size from the user.
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server, it will send ACK signal to client otherwise it will send NACK signal to client.
6. Stop the program
## Client
```py
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
  msg=input("Client > ")
  s.send(msg.encode())
  print("Server > ",s.recv(1024).decode())
```
### Server
```py
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
while True:
ClientMessage=c.recv(1024).decode()
print("Client > ",ClientMessage)
msg=input("Server > ")
c.send(msg.encode())
```
![image](https://user-images.githubusercontent.com/118756330/205698555-18f55da3-60cb-4ea0-8312-c55162d99974.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
#  Exp - 10 - FILE TRANSFER USING TCP SOCKETS
## Algo
1. Start the program.
2. Get the frame size from the user.
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server, it will send ACK signal to client otherwise it will send NACK signal to client.
6. Stop the program
## Client
```py
import socket
s = socket.socket()
host = socket.gethostname()
port = 60000
s.connect((host, port))
s.send("Hello server!".encode())
with open('received_file', 'wb') as f:
  while True:
    print('receiving data...')
    data = s.recv(1024)
    print('data=%s', (data))
    if not data:
      break
  f.write(data)
f.close()
print('Successfully get the file')
s.close()
print('connection closed')
```
## Server
```py
import socket
port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)
while True:
conn, addr = s.accept()
data = conn.recv(1024)
print('Server received', repr(data))
filename='mytext.txt'
f = open(filename,'rb')
l = f.read(1024)
while (l):
  conn.send(l)
  print('Sent ',repr(l))
  l = f.read(1024)
f.close()
print('Done sending')
conn.send('Thank you for connecting'.encode())
conn.close()
```
![image](https://user-images.githubusercontent.com/118756330/205698620-3123ce3b-3b4d-410a-871c-58e5cd647094.png)
### <a href = https://github.com/secaids/cn/#INDEX>Index</a>
