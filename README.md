[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: FU Yunfei
### Student Id: 21110224
### Email: yfubp@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    **Measurement tool**: Phoronix Test Suite

    **CPU test**: Compression rating / Decompression rating

    - The Compression rating and Decompression rating tests measure the performance of the CPU in handling compression and decompression tasks, which are common in many applications.
    
    **Memory test configuration**: Copy interger

    - The Copy integer test measures the memory bandwidth by copying integer values, which is a fundamental operation that affects overall system performance.

    **Measurement Results**: 

    - The values obtained from the measurement results represent the performance of the instances in terms of Million Instructions Per Second(MIPS) for CPU tests and MB/s for memory tests.


2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | 3657 MIPS / 3092 MIPS | 10939.05 MB/s |
    | `t2.medium`  | 9758 MIPS / 5815 MIPS | 18908.41 MB/s |
    | `c5d.large` | 7791 MIPS / 5154 MIPS | 13879.00 MB/s|

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

    **Analysis**:
   
   - The performance of EC2 instances generally increases with the increase in the number of vCPUs and memory resources. But the increase may not always be linear due to differences in instance architecture and other factors.
   
   - `t2.micro` instance has the lowest performance. `t2.medium` having the highest CPU performance. `c5d.large` having a balanced performance in both CPU and memory tests.



## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 3.95k          |  0.206   |
    | `m5.large` - `m5.large`   |   4.96k        |  0.219   |
    | `c5n.large` - `c5n.large` |    4.95k       |   0.176  |
    | `t3.medium` - `c5n.large` |    4.44k       |  0.241   |
    | `m5.large` - `c5n.large`  |   4.90k        |    0.210 |
    | `m5.large` - `t3.medium`  |   4.16k        |  0.261   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

    **Analysis**: Instances of the same type generally show high TCP bandwidth and low RTT, indicating good network performance.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |    34.1k       |  61.154  |
    | N. Virginia - N. Virginia |    4.65k       |  0.208   |
    | Oregon - Oregon           |    4.68k       |  0.190   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.

    **Analysis**: Instances within the same region generally exhibit better network performance with higher TCP bandwidth and lower RTT compared to instances deployed in different regions.