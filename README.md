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

## PROGRAM
### client.py
```
import socket
    client = socket.socket()
    host = socket.gethostname()
    port = 9999
    client.connect((host, port))
    print(f"Connected to server {host}:{port}")
    print("Type network commands like: ping google.com, netstat, nslookup google.com, tracert 8.8.8.8")
    print("Type 'exit' to quit.\n")
    
    while True:
        command = input("Client> ")
        client.send(command.encode())
        if command.lower() == 'exit':
            print("Disconnected from server.")
            break
        data = client.recv(4096).decode()
        print(f"\n--- Output ---\n{data}\n")
    client.close()
```
### server.py
```
import socket
import subprocess
server = socket.socket()
host = socket.gethostname()
port = 9999
server.bind((host, port))
server.listen(1)
print(f"Server started on {host}:{port}")
print("Waiting for client...")
conn, addr = server.accept()
print("Connected with:", addr)

while True:
    data = conn.recv(1024).decode()
    if not data or data.lower() == 'exit':
        print("Client disconnected.")
        break
    print(f"Received command: {data}")
    try:
        output = subprocess.getoutput(data)
    except Exception as e:
        output = str(e)
    conn.send(output.encode())
conn.close()
server.close()

```
## Output
PING
<img width="1000" height="397" alt="Screenshot 2025-11-16 124051" src="https://github.com/user-attachments/assets/fa40fded-4025-4c34-a5b5-0f6d0289449c" />

NETSTAT
<img width="972" height="1113" alt="Screenshot 2025-11-16 124647" src="https://github.com/user-attachments/assets/4bb27b76-2c8f-43fc-b296-8f19aa5c8f02" />

NSLOOKUP AND TRACERT
<img width="983" height="1018" alt="image" src="https://github.com/user-attachments/assets/0dd5db94-8f7a-4c18-ac5a-011a55e479e9" />


## Result
Thus Execution of Network commands Performed 
