# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## Program:
client
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

print("Connected. Type any network command (ipconfig, ping, etc.) or 'exit'.")

while True:
    cmd = input("Enter command: ").strip()
    if not cmd:
        continue

    s.send(cmd.encode('utf-8'))
    
    if cmd.lower() == "exit":
        print("Exiting...")
        break

    output = s.recv(65536).decode()
    print("\n----- RESULT -----")
    print(output)
    print("------------------\n")

s.close()
```
server
```
import socket
import subprocess
import platform

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server listening on port 8000...")
c, addr = s.accept()
print("Connected:", addr)

while True:
    command = c.recv(1024).decode().strip()
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:
        # Run ANY command the client sends
        completed = subprocess.run(
            command, 
            capture_output=True, 
            text=True, 
            shell=True
        )
        output = completed.stdout + (completed.stderr or "")
    except Exception as e:
        output = f"Command failed: {e}"

    c.sendall(output.encode('utf-8'))

c.close()
s.close()
```
## Output

### netstat
<img width="1220" height="625" alt="image" src="https://github.com/user-attachments/assets/209b8328-aea3-406d-bb84-f9cccc5cf7d4" />

### ipconfig
<img width="907" height="821" alt="Screenshot 2025-11-13 102710" src="https://github.com/user-attachments/assets/c9fba767-9092-4acf-a7b1-82b579f21d2a" />

### ping
<img width="941" height="472" alt="Screenshot 2025-11-13 102824" src="https://github.com/user-attachments/assets/b6b43aeb-3c3d-4cd0-98c9-13c3503f34ae" />


### tracert
<img width="913" height="534" alt="Screenshot 2025-11-13 102845" src="https://github.com/user-attachments/assets/095d987b-bd79-4fc8-b04b-713bee68c0f1" />

### nslookup
<img width="915" height="838" alt="Screenshot 2025-11-13 104148" src="https://github.com/user-attachments/assets/4554e5e3-c89e-445f-9d47-f2ffc85ea8e1" />

### getmac
<img width="933" height="253" alt="Screenshot 2025-11-13 104239" src="https://github.com/user-attachments/assets/d7f13d63-f648-413a-adf5-33e5caa25e8f" />

### hostname
<img width="647" height="303" alt="image" src="https://github.com/user-attachments/assets/fe46b536-4cc7-4f18-a491-74344e41c5d6" />

### nbtstat

<img width="919" height="684" alt="Screenshot 2025-11-13 104427" src="https://github.com/user-attachments/assets/ff5e7728-8fbe-430f-821c-e5986a4ea3b5" />

### arp
<img width="911" height="828" alt="Screenshot 2025-11-13 104510" src="https://github.com/user-attachments/assets/33faa729-dd8e-4e06-a237-fb98dd3624ef" />

### systeminfo
<img width="937" height="1073" alt="image" src="https://github.com/user-attachments/assets/83d0c42e-fbf2-431a-b405-8982ba39127e" />

## Result
Thus Execution of Network commands Performed.
