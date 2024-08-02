***
## **TCPWRAPPED**

- When Nmap labels something tcpwrapped , it means that **the behavior of the port is consistent with one that is protected by tcpwrapper**. Specifically, it means that a full TCP handshake was completed, but the remote host closed the connection without receiving any data


***
***


## **REDIS DB**
- ==TCP 6379==
- In-memory data structure store that is often used as a database, cache, and message broker


***
****



## **RSYNC**
- ==TCP 873==
- a fast, versatile, remote (and local) file-copying tool
- efficiently transfers and synchronizes files between two different systems over a network



***
***

## **WinRM**
- ==Port 5985==
- **Windows Remote Management**
- a Windows-native built-in remote management protocol that basically uses Simple Object Access Protocol to interact with remote computers and servers, as well as Operating Systems and applications. WinRM allows the user to: 

→ Remotely communicate and interface with hosts 
→ Execute commands remotely on systems that are not local to you but are network accessible. 
→ Monitor, manage and configure servers, operating systems and client machines from a remote location.

***
***

## SSTI

[[1. STARTING POINT#BIKE]]
https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#what-is-ssti-server-side-template-injection

Server-side template Injection
- Vulnerability that occurs when an attacker can inject malicious code into a template that is executed on the server. This vulnerability can be found in various technologies, including Jinja. IN this case, NODE JS and Express web stack


***

## PostgreSQL

[[1. STARTING POINT#**PostgreSQL**]]

- Port 5432
- RDBS
- `psql` - CLI tool
- TOP PostgreSQL Commands to know: 
https://hasura.io/blog/top-psql-commands-and-flags-you-need-to-know-postgresql

***
***

### SSH Tunneling

[[1. STARTING POINT#==SSH Tunneling==]]
- Interacts with services running internally on a remote host otherwise invisible to anyone else

==`ssh -L 1234:localhost:5432 christine@10.129.228.195 -f -N`==


***
***

