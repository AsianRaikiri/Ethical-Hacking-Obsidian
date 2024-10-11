nmap is a good CLI Tool to scan the target machine for available Ports. It is capable of differentiating between open, closed and filtered Ports.
There are scripting capabilities for nmap, with which the Tool can use exploits and do the actual exploit itself. 

## Basic Scans 
nmap has a lot of different scan types it can do, but the most basic scans are:
* TCP Connect Scan `nmap -sT`
* SYN "Half-Open" Scan ```nmap -sS```
* UDP Scan ```nmap -sU```
* TCP Null Scan ```nmap -sN```
* TCP FIN Scan ```nmap -sF```
* TCP Xmas Scan ```nmap -sX```

### TCP Connect Scan
![[TCP Connection Request.png]]
A TCP Connect Scan starts a TCP Request to the target Machine, which involves a three way handshake. 
* If the Port is open, the Server will respond with a SYN/ACK Response.
* If the Port is closed, the Server will respond with the RST Flag set.
* If the Port is protected by a firewall, it might drop the request and won't send any response. Or depending on the firewall configuration, it might send back a packet with the RST Flag set. 
### SYN Scan
![[SYN Scan.png]]
The difference between a normal TCP Request and a SYN Request is, that the Client in case of the SYN Request sends a packet with the RST Flag set in the end, instead of a packet with ACK Flag. That makes the request more stealthy, since most services only log if a successful connection is established between a client and a target. 
But to create a SYN request in a Linux environment, the user will need sudo permissions, since nmap need to create raw packets. 

### UDP Scan
Since UDP Connections are inherently stateless, there is no acknowledgement from the server if a port is open or behind a firewall, if the request itself isn't an actual request. 
nmap categorizes all request that get no response as open|filtered.
If there is a ICMP Response, the port can be marked as closed and if there is any other response, then the port is considered as open.

