# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
```python

SERVER

# server.py

import socket

s = socket.socket()
s.bind(('localhost', 12345))
s.listen(1)

print("Server waiting for connection...")

conn, addr = s.accept()
print("Connected to:", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    print("Received Frame:", data)

    ack = "ACK " + data
    conn.send(ack.encode())

conn.close()
s.close()

CLIENT

# client.py

import socket
import time

c = socket.socket()
c.connect(('localhost', 12345))

frames = ['1', '2', '3', '4', '5']
window_size = 3

i = 0

while i < len(frames):

    window = frames[i:i+window_size]

    for frame in window:
        print("Sending Frame:", frame)
        c.send(frame.encode())

        ack = c.recv(1024).decode()
        print("Received:", ack)

        time.sleep(1)

    i += window_size

c.close()
```
## OUPUT

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/ff599c98-e02a-4fd8-81df-b2ed3074b057" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
