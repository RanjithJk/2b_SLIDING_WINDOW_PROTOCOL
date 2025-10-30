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
# SERVER
```
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break

    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()  
s.close()
```
# CLIENT
```
import socket
c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))

i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  

        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  

    break
c.close()
```  

## OUPUT
# SERVER
<img width="783" height="266" alt="488674541-10077438-c39c-4e7f-8921-bf4dfce10944" src="https://github.com/user-attachments/assets/a73498c7-71c7-4f56-80c4-7fc5131bda80" />

# CLIENT
<img width="792" height="262" alt="488674607-510401d9-319e-4f18-b3e9-e2f92a7a7a77" src="https://github.com/user-attachments/assets/3907d5be-5d5b-4255-8f87-9d5ac2eb19db" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
