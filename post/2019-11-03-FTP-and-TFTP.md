### FTP and TFTP
<pre>Date: 2019-11-03 21:11:00            Tag: Networking</pre>

Trivial File Transfer Protocol (TFTP): A file transfer Protocol based on **UDP** which allows a client to get a file from or put a file onto a remote host. **Today, TFTP is virtually unused for Internet transfers.** A transfer request is always initiated targeting port 69, but the data transfer ports are chosen independently by the sender and receiver during the transfer initialization.

File Transfer Protocol (FTP): A protocal based on TCP to transfer file between client and server.</p>
  
##### Why FTP is faster than TFTP?

TFTP use a a stop-and-wait flow window control algorithm. It stop for ACK before sending the next data packet, a lost packet causes timeout and retransmission.


For FTP, it has three modes to tranfer file:
- Stream mode: Data is sent as a continuous stream, all processing is left up to TCP.
- Block mode: FTP breaks the data into several blocks (block header, byte count, and data field) and then passes it on to TCP.
- Compressed mode: Data is compressed using a simple algorithm.
Data can keep transfer as long as the receiver can handle it.
