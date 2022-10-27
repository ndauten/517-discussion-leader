# Review

## Info

Reviewer Name: Yudi Yang

Paper Title: ReVirt: Enabling Intrusion Analysis through Virtual-Machine Logging and Replay

## Summary

This paper describes a method to do system-level logging and replay through building the logger on top a VMM (UMLinux) and
placing the logged software under a Virtual Machine.  The author argues that the kernel may contain a bug so that
if the logger is placed under the same system as the logged application, intruder may utilize the kernel bug, thus
interfere with the logger so that incorrect log could be recorded.

The paper argues that the VMM (UMLinux) has a smaller TCB than a kernel so that the VMM is more unlikely to be invaded, which
protects the logger.  The paper also summarizes the detailed methodology of the logging and interference with UMLinux.

### Problem and why we care

With logging and replay, developers could understand how and why the attack could happen; and the exact location and trigger of
the bug so that it could be fixed.  The integrity and availability of the logger is crucial to provide such feature.  Thus,
we require that the logger be placed in a secure domain.

### Gap in current approaches

Currently, the logger is placed under the same operating system as the logged program.  Thus, if the kernel of the OS is invaded,
the logger would not be able to provide the service developers require it to do as the intruder may utilize the kernel bug to
control the behaviour of the logger (both integrity and availability would not exist).

### Hypothesis, Key Idea, or Main Claim

The author claims that placing the logger on top of a VMM can solve this problem as the VMM is harder to be intruded.  Thus,
the logger would be less likely affected by an incorrect setup of software / kernel, and correctly logs the events which
can be later replayed.

### Method for Proving the Claim

The author implements the logger over UMLinux, a VMM, and demonstrates ReVirt, the logger.

### Method for evaluating

The author lists several host components for UMLinux to emulate for the purpose of logging.

### Contributions: what we take away

We now have the logger that is independent of the tested system, so that every event (non-deterministic ones suffice according
to the paper) can be recorded and replayed for demonstrating bugs when an intrution occurs.

## Pros (3-6 bullets)

* The logger is independent of the software system, integrity of the logger and availability of the logger are kept.
* There is an actual VMM (UMLinux) and the logger (ReVirt) implemented upon it. Thus it is demonstrated to be possible.
* There is a low virtualization overhead for the logger.

## Cons (3-6 bullets)

* Some environment cannot be realized in a virtual machine. Eg.: a dedicated hardware that interface is emulated in a virtual machine.
* Although overhead is low, in a productive environment, latency is important, and those overhead leads to real budget spending.
* The author argues that VMM has smaller TCB, but bugs and memory vulnerabilities exist in VMMs. One famous example is Spectre and
Meltdown. Intrusion to the VMM and logger still exists in theory.

### What is your analysis of the proposed?

Summarize and justify what your evluation of the paper is. 

## Details Comments, Observations, Questions

* Is UMLinux type I or type II hypervisor? (5 min)
  * Type II
* Which type better suits ReVirt? (5 min)
  * Result of class discussion: both should be fine; not a significant difference.
* Container or VM based is better (Ben's question source) (5 min)
* Is ReVirt actually more secured? (5 min + 5~10 min)
  * Host OS may be compromised.
  * Rely on Host OS to allocate memory / signal 
  * capture the logger
  * processing mechanism
  * “The avenues a villain can use to attack the host differ greatly between the two structures”
* Time and External Input (non-deterministic event), are they enough? Anything else matters? (5 min)
  * Randomness: OS may read memory from a random address and use it as a random seed.
* Problem with Cooperative Logging (5 min)
  * Transmission Error
  * Man-in-the-middle Attack
