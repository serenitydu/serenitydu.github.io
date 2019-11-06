### Flow control and Congestion control
<pre>Date: 2019-11-06 17:20:00            Tag: Networking</pre>

#### Error Control

Forward Error Correction

- Error Detection
    Performed in each layer of the TCP/IP stack by means of header checksums, and errored packets are dropped. And a ACK wil be send for this segment.
    Selective acknowledgment (SACK) is used to report multiple lost segments.
- TCP Re-transmission
    Value of retransmission timer: TCP continuously measure the RTT and updates the retransmission timer value, defined as Retransmission TimeOut (RTO), dynamically.

#### Flow Control

Sliding Windows, receiver notifies sender:
- ACK number
- WIN size

#### Congestion Control

SOURCE QUENCH信息以前用来节制发送太多报文的主机。当主机接收到该信息，它预计将放缓发送报文。现在很少使用，因为当拥塞发生时，这类报文会起到火上浇油的作用，而且也不清楚如何做出回应。Internet中的拥塞控制现在大部分在传输层完成，使用报文丢失作为拥塞信号。
The sender can infer congestion when a retransmission timer goes off. 
The receiver reports congestion implicitly by sending duplicate acknowledgements.

- **Receiver provides:**
**awnd:** Advertised window size
**MSS:** Maximum segment Size 
- **Sender provides:**
**cwnd:** Congestion window size
**ssthresh:** Slow start threshold

- Slow Start and Congestion Avoidance
    ```
    if(cwnd <= ssthresh){
        //Slow start
        each time receive an ACK:
            cwnd = cwnd + MSS
    }else{
        //Congestion Avoidance, increase linearly
        each time receive an ACK:
            cwnd = cwnd + segsize x segsize / cwnd + segsize / 8
    }

    when a congestion occurs:
        ssthresh = max [ 2 segsize, min (cwnd, awnd)/2 ]   
        cwnd = 1 segsize 
    ```
- Fast retransmit
    - After receive three duplicate ACKs, the sender retransmits the segments without waiting for retransmission timer; then perform congestion avoidance.
- Fast Recovery
    - After receive three duplicate ACKs:
        ssthresh = max [ 2 segsize, min (cwnd, awnd)/2 ]
        cwnd = ssthresh + 3 segment
    - For each additional duplicate ACK:
        cwnd = cwnd + segsize
    - When new ACK for retransmitted segment received:
        cwnd = ssthresh + segsize
