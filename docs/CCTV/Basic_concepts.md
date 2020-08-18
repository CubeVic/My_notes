This is the initial draft 2020/08/18 Later with the addition of more information i will segment this in different parts or notes

## I-P-B Frames

![I-P-B_Frames.jpg](images/I-P-B_Frames.jpg){: .center}

**I-FRAME** or Intra-coded picture, least compressible of all frames but it doesn't required other frames to be decoded, it is a complete image, similar to `.jpg`, compress just I-Frames will result in a good quality but heavy file.

**P-Frame** or Predicted picture,more compressible than the I-FRAME, it use information of the previous frame to decompress. It only holds the part of the image that change comparing with the last frame.

**B-Frame** or Bidirectional predicted picture, can use both previous and forward Frame to get the highest amount of date compression, use the difference between the current frame and both  the preceding and following frame to specify its content.

![I-P-B_Frames_01.png](images/I-P-B_Frames_01.png){: .center}  

## Throughput vs Bandwidth

In the nutshell, **Throughput tells you how much data was transferred from a source at any given time** and **bandwidth tells you how much data could theoretically be transferred from a source at any given time.**

![Bandwidth-and-Throughput_001.jpg](images/Bandwidth-and-Throughput_001.jpg){: .center}

### Throughput

The network throughput refers to how much data can be transferred from source to destination withing a frame of time. **Throughput measures how many packets arrive at their destinations successfully.**
Packet loss, latency, and jitter are all related to slow throughput speed. Latency is the amount of time it takes for a packet to make it from source to destination, and jitter refers to the difference in packet delay.

### Bandwidth

although a bit confusing, the bandwidth definition will be **Network bandwidth is defined as the maximum transfer throughput capacity of a network** it measure how much data can be sent and receive at the same time. 
It is important to know bandwidth doesn’t actually increase the speed of a network, it just appears to make the network faster.

>Let’s say 1 Mbps is the equivalent of a single-lane freeway. Let’s also say you want to download a 5 Mb image. If you had a connection with a bandwidth of 1 Mbps (one lane) it would take you about five seconds to download that image. Now, if you were operating with a 5 Mbps bandwidth connection (five lanes)

![Bandwidth-and-Throughput_002.jpg](images/Bandwidth-and-Throughput_002.jpg){: .center}