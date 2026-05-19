# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP:
## SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is waiting for connection...")
c, addr = s.accept()
print("Connected with", addr)
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    mac = address.get(ip, "Not Found")
    c.send(mac.encode())
c.close()
s.close()
```
## CLIENT:
```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    ip = input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())
    if ip.lower() == "exit":
        break
s.close()
```
## OUPUT - ARP
<img width="1116" height="947" alt="image" src="https://github.com/user-attachments/assets/06d01b73-7af9-4796-84e4-0f9326bec5c0" />

## PROGRAM - RARP
## SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("Client is waiting for connection...")
c, addr = s.accept()
print("Connected with", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}
while True:
    mac = c.recv(1024).decode()
    if not mac:
        break
    if mac in address:
        c.send(address[mac].encode())
    else:
        c.send("Not Found".encode())
c.close()
s.close()
```
## CLIENT:
```
import socket
s = socket.socket()
s.connect(('localhost', 9000))
while True:
    mac = input("Enter MAC Address: ")
    s.send(mac.encode())
    print("Logical Address:", s.recv(1024).decode())
```
## OUPUT -RARP
<img width="895" height="333" alt="image" src="https://github.com/user-attachments/assets/b076a6ab-ef07-4187-8c05-2d95663af5fb" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
