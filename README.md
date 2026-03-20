# 2c.SIMULATING ARP /RARP PROTOCOLS
## Name: S Madhumitha
## Reg no:212225040217
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
~~~
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("ARP Server is listening on port 8000...")
c, addr = s.accept()

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()
    print(f"Received IP: {ip}")
    mac = address.get(ip, "Not Found")
    c.send(mac.encode())
~~~
client
~~~
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter Logical Address (IP): ")
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())
~~~
## OUPUT - ARP
server
![cn ex 2c arp server](https://github.com/user-attachments/assets/3c6a2f03-2c4b-47fb-8bac-b320aeec6f24)

client
![cn ex 2c arp client](https://github.com/user-attachments/assets/483fb49b-d267-4057-abd3-7f474b48f155)

## PROGRAM - RARP
server
~~~
import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)
print("RARP Server is listening on port 8001...")
c, addr = s.accept()

address = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()
    print(f"Received MAC: {mac}")
    ip = address.get(mac, "Not Found")
    c.send(ip.encode())
~~~
client
~~~
s = socket.socket()
s.connect(('localhost', 8001))

while True:
    mac = input("Enter Physical Address (MAC): ")
    s.send(mac.encode())
    print("IP Address:", s.recv(1024).decode())
~~~
## OUPUT -RARP
server
![cn ex 2c rarp server](https://github.com/user-attachments/assets/e3032219-2505-4027-93c6-5508fab81faf)

client
![cn ex 2c client](https://github.com/user-attachments/assets/e96a2681-ff88-471f-a044-50e35c7d321d)

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
