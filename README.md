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
## Server:
~~~
import socket

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 5000

server.bind((host, port))
server.listen(1)

print("ARP Server is waiting for connection...")

conn, addr = server.accept()
print("Connected to client:", addr)

ip_address = conn.recv(1024).decode()
print("Received IP:", ip_address)

mac_address = arp_table.get(ip_address, "IP Address not found in ARP Table")

conn.send(mac_address.encode())

conn.close()
server.close()
~~~
## Client:
~~~
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 5000

client.connect((host, port))

ip = input("Enter IP Address: ")

client.send(ip.encode())

mac = client.recv(1024).decode()

print("MAC Address:", mac)

client.close()
~~~
# OUPUT - ARP
## Server - Output:
<img width="764" height="313" alt="image" src="https://github.com/user-attachments/assets/7d70ee05-739e-4e5b-836e-6bdd78e2c587" />

## Client - Output:
<img width="678" height="283" alt="image" src="https://github.com/user-attachments/assets/6df0a2ed-6e6e-4cc7-8f34-3fb3832a164f" />


# PROGRAM - RARP
## Server:
~~~
import socket

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

server.bind((host, port))
server.listen(1)

print("RARP Server is waiting for connection...")

conn, addr = server.accept()
print("Connected to client:", addr)

mac_address = conn.recv(1024).decode()
print("Received MAC:", mac_address)

ip_address = rarp_table.get(mac_address, "MAC Address not found in RARP Table")

conn.send(ip_address.encode())

conn.close()
server.close()
~~~
## Client:
~~~
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

client.connect((host, port))

mac = input("Enter MAC Address: ")

client.send(mac.encode())

ip = client.recv(1024).decode()

print("IP Address:", ip)

client.close()
~~~
# OUPUT -RARP

## Server:
~~~
import socket

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

server.bind((host, port))
server.listen(1)

print("RARP Server is waiting for connection...")

conn, addr = server.accept()
print("Connected to client:", addr)

mac_address = conn.recv(1024).decode()
print("Received MAC:", mac_address)

ip_address = rarp_table.get(mac_address, "MAC Address not found in RARP Table")

conn.send(ip_address.encode())

conn.close()
server.close()
~~~

## Client:
~~~
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

client.connect((host, port))

mac = input("Enter MAC Address: ")

client.send(mac.encode())

ip = client.recv(1024).decode()

print("IP Address:", ip)

client.close()
~~~

# Output:

## Server:
<img width="740" height="320" alt="Screenshot 2026-02-12 162621" src="https://github.com/user-attachments/assets/44cf2b4e-3830-40f5-8ebb-97e84f7acd13" />

## Client:
<img width="648" height="297" alt="Screenshot 2026-02-12 162651" src="https://github.com/user-attachments/assets/88f6dad6-b269-4e20-9f6b-ac633827abe1" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
