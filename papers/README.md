# CSE-5095-SDN: Reading Report

## 1. Requirements:

> Write a ~400 word critical response and comments to each required paper. Focus on the following:
>
> - State the problem that they try to solve and the main contributions.
> - Describe the key insight or novelty of their proposed work or approach.
> - What are the limitations of the paper? Write the criticisms.
> - Any improvements or related ideas that you can suggest?

Your most important task is to **demonstrate that you've read the paper and thought carefully about the topic**. **No copy and paste of the original paper text**!

## 2. Reports

### 2.1 Aquila: A Practically Usable Verification System for Production-Scale Programmable Data Planes

**Problem:** P4 gives functionality efficiency and flexibility in industry, however it is challengingto prove the correctness of data plane programs, because of multiple pipelines, many functions, various packet paths, and complex function chains.

1. Intent complexity: Hard to formalize the special context like service-specific properties and multi-pipleline control with traditional verification language.
2. Scalability: Too many network functions and dependencies lead to the exponential growth of states and program branches.
3. Buy localization: Formal verification can output whether there is a bug in P4 program, however it is not trivial to find where is the bug.
4. Reliability of verifier: Verifier might contains bug.

**Key insight & novelty:**

1. Intent language LPI is proposed. A high-level formalization language that you can write 10% lines of code compared with traditional one.
2. Propose a novel sequential encoding algorithm to make verificaiton more efficient that encoding the data plane component into a GCL representation. P4 language uses a state machine models can generate DAG diagram which contains so many paths. The key idea of reduce DAG to line is if many links result in a same state, convert them into a line by adding conditional logic by a ghost indicator. (Is this a common technique in formal verification field?)
3. Narrows down suspect variables and actions based on reported violations and pinpoints the culprit by simulating a fix for each suspect. The root cause is found by finding execution path by counter example  (output of verifier and backward verification (like if A trigger the assertion, then check those operations have ever changed A previously)
4. Build a self validator based on a external tool named refinement proof.

**Limitations:**

1. Only the correctness of P4 programming is verified, however the hardware bugs and the bugs in P4 language itself are not considered.
2. It seems like the verification only works for the single hop behavior? The wrong action order in multi hop network cannot be found here.
3. Some time related error like timeout is not considered. It can might be improved with the timed automata verification.

**Improvements:**

---

### 2.2 OpenFlow: Enabling Innovation in Campus Networks

**Problem:** 

1. No practical way to experiment with new network protocols in practice.
2. How run experiments in campus network is unsure.
3. Commercial switches and routers do not typically provide an open software platform.
4. Existing solutions based on Linux PC have limited performance (<= 1Gbits), other solutions based on specialized hardware are either costly or have inflexible inferface.

**Key insight & novelty:**

1. Propose that equipment vendors to provide open, programmable, standardized platform to let researchers deploy their protocols.
2. Easier implementation of network-wide forwarding policies.
3. Insight: Most of the modern switches contain flow-tables and their is a set of common set of functions in different vendors' flow-tables.
4. Partition and isolation of production flows and research flows.
5. It provides security with a TLS connection to prevent snooping and DoS attacks on the controller and/or the network.

**Limitations:**

1. Even though there is single standard (with four versions), there are many vendor-specific implementation details.

2. Advanced packet classification / processing still done in software. Existing hardware only supports a couple of 1000 entries in hardware forwarding tables (TCAM).

3. OpenFlow will not replace routing protocols; an SDN/OpenFlow controller must reinvent all the wheels (scalability, resilience, reliability, auto-discovery, fast convergence), and provide added value.

**Improvements:**



---

### 2.3 Can the Production Network Be the Testbed?

**Problem:** 

1. Building a large scale realistic network testbed is necessary but hard due to budget and implementation effort.
2. The difficulty of managing and monitoring complex, large-scale networks with multiple users and devices.
3. The challenge of optimizing network performance and efficiency, particularly in dynamic and rapidly changing environments.

**Key insight & novelty:**

1. The ability to virtualize a physical network, allowing it to be divided into multiple logical networks, or "slices."
2. The use of a hypervisor model to create and manage the network slices, similar to the way virtualization software is used in computer systems.
3. The ability to monitor and control the flow of traffic between the slices, allowing network administrators to experiment with new network designs and configurations without disrupting the overall network.
4. The potential to improve network flexibility, scalability, and performance by enabling network administrators to test and implement new network configurations without disrupting existing network traffic.

**Limitations:**

1. The bandwidth isolation is achieved by per-slice queue which might be inefficient. Considering a network with more than thousand experiments requires to maintain thousand queues which may pose a challenge on the switch memory and processing speed.
2. Not able to isolation network into several sub-networks.
3. The complexity of configuring and managing the network slices, which might require specialized training and expertise.
4. The potential for performance degradation or other negative impacts on the overall network if the slices are not configured and managed properly.

**Improvements:**

1. The development of new algorithms and techniques for optimizing the performance and efficiency of the network slices.

2. The integration of machine learning and other advanced technologies to enable FlowVisor to make more intelligent and automated decisions about network traffic flow.

3. The inclusion of additional features and capabilities, such as support for new protocols and network architectures, to make FlowVisor more versatile and useful for a wider range of applications.

---

### 2.4 OmniMon: Re-architecting Network Telemetry with Resource Efficiency and Full Accuracy

**Problem:**

1. Previous methods can only find a trade off between Resource Efficiency and Full Accuracy because each kind of network device has its own bottleneck.
2. No collaboration between different kinds of network devices.

**Key insight & novelty:**

1. Coordinate different entities to get the final statistics by a merge process.
2. Shared memory slots on switches to save memory and separate ingress and egress slots on end hosts to improve efficiency.
3. Hybrid consistency model to deal with the situation when data-plane lack of network-wide synchronization.
4. Linear system with DCN- specific optimizations to design the flow to memory mapping on switches to guarantee the per-switch, per-flow loss interference in common cases.

**Limitations:**

1. Information loss happens in switch failure that some information cannot be merged might cause the catastrophic statistic result to other traffics.
2. The correctness of the hybrid consistency protocol has no formal proof.
3. The mapping algorithm is based on the prior information of packet loss distribution.

**Improvements:**

---

### 2.5 P4: Programming Protocol-Independent Packet Processors

**Problem:**

1. The authors argue that current packet processing frameworks are limited by their dependence on specific protocol implementations, which hinders their ability to adapt to new protocols and requirements.

**Key insight & novelty:**

1. The paper proposes a protocol-independent packet processing framework, which allows packet processors to be programmed using high-level abstractions that are independent of the underlying protocols.
2. The framework gives the system reconfiguraiotn abililty to adapt to new protocols or requirements, or to modify its processing rules or algorithms in real-time. This could be a useful feature for packet processing systems, as it would enable them to adapt to changing network conditions and requirements, and to improve their performance and efficiency.
3. Target independence gives the ability for network to operate on a variety of different target platforms or devices, without being tied to a specific hardware or software implementation. This could be useful for packet processing systems, as it would enable them to run on a wide range of devices, and to adapt to changing hardware or software environments.
4. Protocol independence gives the ability for network to operate on a variety of different protocols, without being tied to a specific protocol implementation. This could be useful for packet processing systems, as it would enable them to adapt to new protocols, or to operate on multiple protocols simultaneously.
5. The P4 framework is based on the idea of functional primitives, which are simple functions that can be combined and composed to perform more complex packet processing tasks.
6. The authors demonstrate the effectiveness of the P4 framework through several case studies, showing that it can be used to implement a variety of packet processing applications, and that it can improve the performance and efficiency of these applications.
7. The paper also discusses the challenges and limitations of the P4 framework, and provides directions for future research in this area.

**Limitations:**

1. The scope of the study may be limited to a specific subset of packet processing applications, which may not be representative of the broader field.
2. The findings of the study may not be generalizable to other contexts or settings, and may be specific to the particular implementation of the P4 framework.
3. The methods used in the study may not be sufficiently rigorous or reliable, and may not adequately control for potential sources of bias or error.
4. The paper may not adequately address potential challenges or limitations of the P4 framework, and may not provide a comprehensive evaluation of its strengths and weaknesses.

**Improvements:**

1. Expanding the scope of the study to include a wider range of packet processing applications, or to evaluate the P4 framework in different settings or contexts.

2. Improving the rigor and reliability of the methods used in the study, for example by using more robust experimental designs or statistical analysis techniques.

3. Addressing potential limitations or challenges of the P4 framework, and providing a more comprehensive evaluation of its strengths and weaknesses.

4. Exploring potential applications or implications of the findings, and providing directions for future research in this area.

---

### 2.6 Offloading Distributed Applications onto SmartNICs using iPipe

**Problem:** 

1. By offloading some of the processing and communication tasks associated with running distributed applications onto a dedicated network interface card (SmartNIC), it may be possible to improve the performance and efficiency of these distributed applications.

2. How efficiently use SmartNICs to maximize offloading benefits for distributed applications to improve the performance, scalability, and flexibility.

**Key insight & novelty:**

1. The key idea behind a SmartNIC is to provide a dedicated and highly-efficient hardware platform for running these applications, which can improve their performance and scalability.
2. The recognition that modern computing environments are increasingly reliant on distributed applications, and that these applications can benefit from dedicated and highly-efficient platforms for running them
3. The development of specialized hardware and software architectures for offloading processing and communication tasks from the host system to the network interface card.
4. The integration of various hardware acceleration engines and other specialized hardware components to support the efficient execution of specific types of tasks.
5. The adoption of open standards and interfaces to enable interoperability and flexibility in the deployment and use of SmartNICs.

**Limitations:**

1. SmartNICs can be expensive, especially when compared to traditional network interface cards. This may make it difficult for some organizations to justify the investment in a SmartNIC, especially for applications with relatively modest performance or scalability requirements.
2. Not all applications can be easily offloaded onto a SmartNIC, and some may require significant modifications or re-engineering to be compatible with a SmartNIC's architecture and capabilities. This can add to the cost and complexity of deploying and using a SmartNIC.
3. While a SmartNIC can improve the performance of some applications, it may not always be the best solution for all applications or workloads. For example, applications that are not well-suited to the parallel processing capabilities of a SmartNIC may not see significant performance improvements when offloaded onto a SmartNIC.

**Improvements:**

1. While a SmartNIC can improve the performance of some applications, it may not always be the best solution for all applications or workloads. For example, applications that are not well-suited to the parallel processing capabilities of a SmartNIC may not see significant performance improvements when offloaded onto a SmartNIC.
2. Improving the compatibility of SmartNICs with a wider range of applications and workloads, through the development of more flexible and adaptable architectures, the adoption of open standards and interfaces, and the use of machine learning and other advanced techniques to optimize performance.
3. Developing new hardware and software technologies that can enable SmartNICs to support a wider range of applications and workloads, and to deliver even higher levels of performance and efficiency. This could include the development of new hardware acceleration engines, the integration of more powerful processors, and the adoption of more advanced networking technologies.

---

### 2.7 
