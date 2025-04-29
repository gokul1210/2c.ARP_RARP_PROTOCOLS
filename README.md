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
## PROGRAM - ARP
CLIENT:
```
import socket

c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")

c.close()
```
SREVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break
    try:
        mac = address[ip]
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())

c.close()
s.close()
```
## OUPUT - ARP
CLIENT:
![Screenshot 2025-04-29 202041](https://github.com/user-attachments/assets/932e4a68-2eaa-4d6e-98d8-fda636c389a7)

SERVER:
![Screenshot 2025-04-29 202056](https://github.com/user-attachments/assets/e4559c8f-5003-4429-877e-783cbaadedfb)


## PROGRAM - RARP
CLIENT:
```
import socket

c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")

c.close()
```

SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
     "6A:08:AA:C2":"165.165.80.80",
    "8A:BC:E3:FA" :"165.165.79.1"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break
    try:
        mac = address[ip]
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())

c.close()
s.close()
```
## OUPUT -RARP
CLIENT:
![Screenshot 2025-04-29 202359](https://github.com/user-attachments/assets/32cd6886-a4e3-4b85-8aa8-922d9c858f35)
SERVER:
![Screenshot 2025-04-29 202415](https://github.com/user-attachments/assets/4db23633-1a2f-4cbe-95ac-eb67949ee4c9)

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
