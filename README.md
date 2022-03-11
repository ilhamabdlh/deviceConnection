# VPN Tunnel

[![Ask a question](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://github.com/ilhamabdlh)

Im trying to build a network with VPN Tunnel, let's look the topology, there is a server is the control for networks that will communicate. In topology, I set PC B as a server to control the connection between clients. Then, and I set PC C to be Client1, I liken PC C to Atop device. and I set PC A to be Client2, as a User who want to access the device.

## Topology
![image](https://user-images.githubusercontent.com/72017753/157813568-a9213801-44b9-464f-88b8-e4b6cf4f6982.png)

## Study VPN
First, before i build a tunnel from vpn, i try to study and explore VPN network. I try it with simplest thing, which is Telnet. Because telnet has a network concept similar to SSH and VPN. Then, telnet can be build in go language without any libraries, only use "net" package from golang. [You can see the code here](https://github.com/ilhamabdlh/deviceConnection/blob/master/server.go)

Here I found some uses of telnet which are almost similar to vpn. Through telnet, various public services can be accessed easily, such as logging in to a computer to internet and various services connected to internet, such as online device catalogs and access databases.

here, I assemble a Telnet connection according to topology that has been made by Alan. so that clients can communicate with each other. You can see it below.

## Telnet Capture

![telnet](https://user-images.githubusercontent.com/72017753/157822629-4b3f4841-3157-4871-9895-73edb76ef86f.png)


### PC B as Server
IP Private: 192.168.254.152
IP Public: 103.164.99.6

### PC A as Client 1
IP Private: 192.168.43.55
IP Public: 116.206.13.170

### PC C as Client 2
IP Private: 172.20.10.2
IP Public: 112.215.65.92

## Work

### PC B as Server
I open Port 24 on the server, that clients can connect to each other.
first, Server must be running:
```bash
go run .
```
and then, the server will open port 24 and waiting for a client to connect.

### PC A as User Client

First, "PC A" must be connected to the server via Command Prompt. I require client to communicate with the server's IP Public.
on command prompt "PC A" input:  
```bash
telnet 103.164.99.6 24
```
- After that on the server side an incoming notification will appear, that PC A has successfully connected to the server.
- On pc A, the user must create a username, like "/user examplename":
```bash
/user liham
```
- After that, PC C must create a ROOM which is a place to communicate with PC C as a device or client. example like "/join okraRoom"
```bash
/join okraRoom
```

### PC C as Device Client

- Same as "PC A", first thing to do with "PC C" is connect to IP Public server.
```bash
telnet 103.164.99.6 24
```
- On PC C, the user must create a Device name, like "/user Swith1234":
```bash
 /user liham
```
- then, device must input the room that has been created by PCA, like "/join okraRoom" with the same room name.
```bash
/join okraRoom
```
On the server you will see that there are two connected clients.

Clients will communicate with each other because they are in the same room.
Telnet that I made, can load connections with many clients. can accommodate hundreds of client connections and ROOM made. so communication between User and Device can be made without being disturbed by different types of devices.
