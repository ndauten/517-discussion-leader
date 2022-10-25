# Review

## Info

Reviewer Name: Youhan Wu

Paper Title: Disco: running commodity operating systems on scalable multiprocessors

## Summary

Hardware innovations advanced while the exsiting commodity OSes couldn't leverage the expected hardware functionality. To reduce the gap between hardware innovations and the adaptation of system software, this paper presents an economical way to develop system software for scalable shared memory multiprocessor without massive development efforts. That is to insert an additional layer between the hardware and OSes, served as a Virtual Machine Manager. This implementation put a lot of effort into minimizing the virtualization overhead, hiding NUMA-ness, and also enhancing resource sharing across the VMs.

### Problem and why we care

- Existing commodity OSes are not suited for a scalable multiprocessor.
- Hardware development faster than system softwares.
- Extensive modifications to OS are required to efficiently support scalable machines.

People are looking for a new way to run multiple commodity operating systems on a scalable multiprocessor, with a small implementation effort.

### Gap in current approaches

- Gap between hardware innovations and the adaptation of system software.
- Old OSes cannot leverage the potential of new hardwares, but exising investments in old OSes make people cannot get rid of them easily.
- Customizations on old OSes are time-consuming, incompatible, and possibly buggy.

### Hypothesis, Key Idea, or Main Claim

We can have an additional software layer sitting between the hardware architecture and operating systems. This layer acts like a virtual machine monitor in that multiple copies of commodity OSes can be run on a single scalable computer.

Some noval ideas were introduced to minimize the overhead of virtual machines and enhances the resource sharing between virtual machines running on the same system. The monitor also hides NUMA-ness from non-NUMA aware OSes, allowing these commodity OSes to efficiently utilize system resources.

### Method for Proving the Claim

Detailed breakdown of overheads and performance improvements. The experimental results show that overhead is indeed low when using Disco, so the system achieves its goals.

### Method for evaluating

Evaluated the Execution overhead, Memory overhead, Scalability, and NUMA overhead by analyzing the execution breakdown on different workloads.

### Contributions: what we take away

- VMWare was born out of this paper.
- Bringed VMs back to people's attention.
- Proved modest overhead of virtualization is possilble.
- Nowadays VMs are wildly used in enterprise and cloud platforms.
- Introduced innovative ideas to cover the NUMA-ness.

## Pros (3-6 bullets)

- Minimized the overhead of virtualization.
- Flexibility to support a wide variety of workloads efficiently.
- Compatible to older versions of OS to keep legacy applications running.
- Hide hides NUMA-ness from non-NUMA aware OSes.
- Low development cost.

## Cons (3-6 bullets)

- The performance evaluation were based on a simulation because the FLASH Multiprocessor was not yet available, which made the results less convincing.
- A certain amount of overhead is required during TLB misses and dynamic page migration/replication.
- Still a little hard for VMM to dynamically schedule hardware resources with only little knowledge about the runtime information of the gusting OSes.

### What is your analysis of the proposed?

Overall, this paper is very detailed and easy to read with many examples. The execution breakdown and the deliberate selection of tested workloads both make the evaluation results more clear and convincing. And some of the innovative ideas are seem inspiring today. 

## Details Comments, Observations, Questions

Disco balances the trade-off between development cost and perfect resource management of the underlying multiprocessor system. The benefits of the system seem quite good at that time with little cost.

This paper puts a lot of effort into eliminating the virtulization overhead, and hidng the NUMA-ness. I am really impressed by the optimization in the virtual memory translation, and NUMA Memory Management.

## Discussion Debrief
### What new insights came out of the discussion?
Why are the OSes back in 90s not scalable?
- hardware innovations (NUMA, distributed resource) require for new system softwares
- Even old Oses can live on NUMA arch, they can suffer from huge memory/IPC overhead

### Was there disagreement? Why?
Is bare-metal hypervisor more secure than hosted hypervisor in general?
- Yes side: A bare-metal hypervisor is bult directly on hardwares, the footprint area is less compared with a hosted hypervisor, so there are fewer vulnerabilities.
- No side: A hosted hypervisor has 2 protection layers, one is from the hypervisor itself, and the other is from the OS level. With multiple lines of defense, it will be hard to penetrate into the OS running in a VM. 

### What was the consensus about the work?
- A bare-metal hypervisor has an edge over a hosted hypervisor from the perspective of Performance and Resource Utilization.
- NUMA is a more scalable pattern compared with UMA, but it requires more effort in software-level optimization to leverage its potential.