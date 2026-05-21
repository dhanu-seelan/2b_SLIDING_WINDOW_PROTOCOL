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
s.bind(('localhost',8002))
s.listen(5)
c, addr = s.accept()
ListSize = int(input("Enter the number of frames to send : "))
List = list(range(ListSize))
WindowSize = int(input("Enter Window Size : "))
st, i = 0, 0
while True:
    while(i < ListSize):
        st += WindowSize
        c.send(str(List[i:st]).encode())
        Acknowledgment = c.recv(1024).decode()
        if Acknowledgment:
            print(Acknowledgment)
            i+=st
```

##Server side
```
import socket
s = socket.socket()
s.connect(('localhost', 8002))
while True:
    print(s.recv(1024).decode())
    s.send("Acknowledgement received from the server".encode())

```
## OUPUT

##Client Side
<img width="525" height="391" alt="image" src="https://github.com/user-attachments/assets/ea8d5785-c706-4c20-9d6f-b4cf4c713da7" />

##Server Side
<img width="537" height="353" alt="image" src="https://github.com/user-attachments/assets/880d79a9-0fa5-4518-9bf1-2e7adf56ca18" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
