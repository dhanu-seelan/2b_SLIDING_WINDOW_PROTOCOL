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

##Client Side
```
import socket

s = socket.socket()
s.bind(('localhost', 8002))
s.listen(5)

print("Waiting for connection...")
c, addr = s.accept()
print("Connected to:", addr)

ListSize = int(input("Enter the number of frames to send: "))
frames = list(range(ListSize))

WindowSize = int(input("Enter Window Size: "))

i = 0

while i < ListSize:
    end = min(i + WindowSize, ListSize)

    # Send frames within the current window
    c.send(str(frames[i:end]).encode())

    acknowledgment = c.recv(1024).decode()

    if acknowledgment:
        print("Received:", acknowledgment)
        i = end      # Move to the next window

c.close()
s.close()
```

##Server side
```
import socket

s = socket.socket()
s.connect(('localhost', 8002))

while True:
    data = s.recv(1024).decode()

    if not data:  # Server has closed the connection
        break

    print("Received:", data)

    s.send("Acknowledgement received from the client".encode())

s.close()

```
## OUPUT


<img width="1311" height="338" alt="image" src="https://github.com/user-attachments/assets/0457ea6a-9af6-46cb-b9b7-ef5284916bc6" />



## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
