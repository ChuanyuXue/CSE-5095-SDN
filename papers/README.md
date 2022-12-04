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

**Improvements:**

---

### 2.2 Aquila: A Practically Usable Verification System for Production-Scale Programmable Data Planes



