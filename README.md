# network analysis with wireshark

## Description
Analyzing pcaps with wireshark

## Activities
###Pcap1
 1.  Which protocol was used over port 3942? 
   **Process:** Go to Statistics > Endpoints > UDP > Right click on the line with port 3942 > apply as filter > selected.Go back to the main screen of wireshark and check the protocol.
    **Ans:** SSDP

2.  What is the IP address of the host that was pinged twice?
 **Process**:Ping works by sending an Internet Control Message Protocol (ICMP) Echo Request to a specified interface on the network and waiting for a reply. When a ping command is issued, a ping signal is sent to a specified address. When the target host receives the echo request, it responds by sending an echo reply packet.

Type icmp on the display filter.
We can see two ping requests that were sent to 8.8.4.4.
**Ans:** 8.8.4.4.

3.  How many DNS query response packets were captured?
**Process**:Type dns in the display filter. Select the first packet that says “standard query response.”
Go to the frame display on the lower left-hand side of wireshark. Click on Domain Name System > Flags > Right click the entry that says “response: message is a response” > apply as filter > selected.
Check the displayed packets in the lower right-hand side of wireshark.
**Ans**: 90

4.  What is the IP address of the host which sent the most number of bytes?
**process**:Go to Statistics > Endpoints > IPv4 > click Tx Bytes (transmit bytes) to display the results in descending order.
**Ans**: 115.178.9.18

### pcap2

1.  What is the WebAdmin password?
**Process**: I decided to check HTTP traffic. Typed in http in display filter.
Packet 4121 looks promising because of a GET request for a password.txt. Right click on packet > followed HTTP stream.
**Ans**:sbt123

2.  What is the version number of the attacker’s FTP server?
**Process**:Based on the previous question, we can infer that the device used to get the password.txt file is the attacker. Type in “ftp and ip.src == 192.168.56.1” in the display filter.
Checked the frame display section of packet 4243.
A brief google search on pyftpdlib shows that it is a python FTP server library.
**Ans**:1.5.5

3.  Which port was used to gain access to the victim Windows host?
**Process**:I decided to look at all the traffic coming from the compromised host 192.168.56.1. Type in “ip.src == 192.168.56.1” in the display filter.

I reviewed the results and found the HTTP traffic when the attacker downloaded the password.txt file. I checked packet 4128 which is the first packet after the HTTP traffic. I followed the TCP stream by right clicking the packet > Follow > TCP stream.
The attacker moved to the desktop and listed the files in the location. It then created a txt file which contains commands to connect to the server using anonymous FTP and download a binary called malware.exe.

I went back to the main screen and looked for the destination port.
Ans:8081

4.  What is the name of a confidential file on the Windows host?
**Process**:I followed the TCP stream of packet 4128. I checked the files in the Desktop directory and found a file called Employee_Information_CONFIDENTIAL.txt.

**Ans**:Employee_Information_CONFIDENTIAL.txt

5.  What is the name of the log file that was created at 4:51 AM on the Windows host?
**Process**: Same process as before, I followed TCP stream of packet 4128. A log file was created on 7/16/2019 at 4:51 AM called LogFile.log.

**Ans**:LogFile.log
