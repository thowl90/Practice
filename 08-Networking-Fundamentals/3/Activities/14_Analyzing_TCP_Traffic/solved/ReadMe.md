## Solution Guide: Analyzing TCP Traffic 

This activity was designed to introduce the Layer 4 protocol, TCP and practice identifying how TCP uses a three-way handshake to establish a connection with a remote host.  

Completing this activity required the following steps:

   - Loading a TCP packet capture with Wireshark.

  - Find all establishing TCP handshakes in the packet capture.

  - Find all TCP terminations in the packet capture. 

   - Determining what websites were visited by analyzing the TCP traffic.
   
---

In Wireshark, open the packetcapTCPclass.pcapng file. 

Find all the TCP handshakes for establishing a connection.
 
- There are three three-way handshakes in the packet capture. 

To find them, do the following:

- To view only the three SYN requests, run:  

  `tcp.flags.syn ==1 && tcp.flags.ack == 0`

- To view only the three SYN/ACK responses, run: 

  `tcp.flags.syn ==1 && tcp.flags.ack == 1`

- To view only the three ACK responses, run: 

  `tcp.flags.syn == 0 && tcp.flags.ack == 1`
  
  **Note**: This may show some extra packets, including the FIN packet. To isolate only the three packets, run:

  `tcp.flags.syn ==1 && tcp.flags.ack == 1 && tcp.flags.fin == 0`


Find any TCP terminations.

- In the packet capture, there is one TCP termination from `Src: 209.202.133.24`. 

- To filter for terminations, run: 

  `tcp.flags.fin==1`
  
#### Bonus  

 Use your findings to determine what the employee is doing during their first week of work.
  
 - One of the IPs belong to the travel website Trivago with the following website:
     - https://whatismyip.live/ip/8.35.179.200

Based on this result, we could assume that the new employee is already planning a vacation.

---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
