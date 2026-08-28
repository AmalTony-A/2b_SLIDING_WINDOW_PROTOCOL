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
## client:
``` PY
import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    data = s.recv(1024).decode()

    if not data:
        break

    print(data)
    s.send("acknowledgement received from the server".encode())

s.close()
```
## server:
``` PY
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)

c, addr = s.accept()

size = int(input("Enter number of frames to send : "))
l = list(range(size))

s = int(input("Enter Window Size : "))

i = 0

while i < len(l):
    c.send(str(l[i:i+s]).encode())

    ack = c.recv(1024).decode()

    if ack:
        print(ack)
        i += s

c.close()
```
## OUPUT

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/614f1c6b-0517-4518-8e19-ff8575a3fd17" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
