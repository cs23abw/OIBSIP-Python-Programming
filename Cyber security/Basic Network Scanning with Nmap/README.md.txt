# Basic Network Scanning with Nmap

## Project Overview

This task was completed as part of the Oasis Infobyte Cyber Security Internship.

The objective of this project is to perform a basic network scan using Nmap, identify open ports and running services, and explain the security meaning of the scan results.

The scan was performed on my own local machine using the localhost IP address:

```text
127.0.0.1
```

This ensured that the scan was carried out safely and only on a system I am authorised to test.

## Tool Used

* Nmap

## Command Used

```bash
nmap -sV 127.0.0.1 -oN nmap_scan_results.txt
```

## Explanation of the Command

* `nmap` starts the Nmap scanning tool.
* `-sV` tells Nmap to detect the service and version running on open ports.
* `127.0.0.1` is the localhost address, meaning the scan was performed on my own computer.
* `-oN nmap_scan_results.txt` saves the scan result into a normal text file.

## Scan Summary

The scan identified that most TCP ports were closed, but a few ports were open and running services.

Some of the important open ports found include:

| Port     | Service Detected         | Explanation                                                                                                    
| -------- | ------------------------ | ------------------------------------------------------------|
| 135/tcp  | Microsoft Windows RPC    | Used by Windows for communication between system components.                                                   |
| 445/tcp  | Microsoft-DS / SMB       | Commonly related to Windows file sharing. This port should be 						protected and not exposed to untrusted networks. 
|
| 2869/tcp | HTTP / Microsoft HTTPAPI | Related to Microsoft network or device discovery services.                                                     |
| 7070/tcp | SSL-related service      | Nmap detected a service but could not fully identify it. Further 					investigation may be required.                
|
| 8000/tcp | Splunkd HTTP             | Related to Splunk web services running on the local machine.                                                   |
| 8089/tcp | Splunkd SSL/HTTP         | Related to Splunk management or API services.                                                                  |
| 8194/tcp | SSL/HTTP Golang service  | A service using HTTP/SSL technology, possibly linked to a local 					application.                                   
|

## Follow-up Investigation

After seeing Splunk-related ports in the Nmap scan, I performed a follow-up check using Windows PowerShell.

The command below confirmed that the Splunk service was running:

```powershell
Get-Service *splunk*
```

Result:

```text
Running  Splunkd  Splunkd Service
```

I also checked which process was using ports 8000 and 8089:

```powershell
netstat -ano | findstr ":8000"
netstat -ano | findstr ":8089"
tasklist /FI "PID eq 7740"
```

The result confirmed that the process using these ports was:

```text
splunkd.exe
```

This means the open Splunk ports were caused by Splunk running locally on my laptop. This does not automatically mean there was an attack. It shows that a local service was active and listening on those ports.

## Security Analysis

This scan shows why network scanning is useful in cyber security. Nmap helps security analysts discover which services are running on a system.

Open ports are not always dangerous, but they should always be reviewed. If a service is not needed, it should be disabled. If it is needed, it should be properly secured with firewall rules, updates, and strong authentication.

For example:

* Port 445 should not be exposed to untrusted networks because it is commonly associated with Windows file sharing.
* Splunk ports such as 8000 and 8089 should be protected because they can provide access to log management and monitoring services.
* Unknown services should be investigated to confirm whether they are expected and safe.

## Files Included

```text
nmap_scan_results.txt
README.md
screenshots/
```

## Screenshots

The screenshots folder contains evidence of the Nmap scan and related outputs.

Example screenshots included:

```text
nmap-version.png
nmap-localhost-scan.png
nmap-results-file.png
```

## What I Learned

Through this task, I learned how to:

* Use Nmap to scan a local machine
* Identify open and closed ports
* Understand the meaning of services running on ports
* Save Nmap results into a text file
* Investigate suspicious or unexpected services
* Use PowerShell commands such as `Get-Service`, `netstat`, and `tasklist`
* Explain scan results from a cyber security perspective

## Conclusion

The Nmap scan successfully identified open ports and services on the local machine. The follow-up investigation confirmed that the Splunk-related ports were caused by the Splunk service running locally.

This task helped me understand how basic network scanning supports security analysis by revealing active services and helping analysts decide whether those services are expected, necessary, and secure.

## Author

Chukwukaima Sam
