# Lab 1 - Cloud and Mobile Computing

## Overview
Lab 1 covers fundamentals of virtualization, containers, and hypervisors in cloud computing environments.

## Topics Covered
- Virtualization technologies (KVM, Hyper-V)
- Hypervisor types and capabilities
- Docker and container runtime
- Virtual machines vs containers comparison
- Performance metrics and resource utilization

## Terminal Outputs
The lab includes execution of various commands demonstrating:
- Docker initialization and setup
- Virtual machine snapshots and filesystem management
- CPU and memory resource analysis
- Network interface configuration
- System performance metrics

## Key Findings

### Data Center Design Sketch
```
Internet
   |
Load Balancer
   |
Core Switches
   |
Fat Tree Network
   |
Rack 1        Rack 2
   |            |
Servers      Servers
   |            |
Hypervisor
Docker Runtime
Containers
   |
Cooling + Power Units
```

## VM Outputs
Demonstrates:
- Virtualization features (Hypervisor vendors: KVM, Full virtualization)
- LID and IOMMU configurations
- Memory and CPU allocation (1.96L, 67mL utilized)
- System capabilities and vulnerabilities

## Final Write-Up Answers

### Q1: Which architecture is better for microservices?
Containers are better because they are lightweight, fast to start, scalable, portable, and consume fewer resources than VMs.

### Q2: Why does AWS split Nitro into hardware components?
To improve security, performance, and offload virtualization tasks from CPU to dedicated hardware.

### Q3: When use VMs over containers?
Use VMs when stronger isolation, multiple operating systems, or legacy software support is required.

### Q4: How does tail latency change with more parallel calls?
As concurrency increases, slow responses become more frequent, increasing tail latency.

## Conclusion
Lab 1 provides foundational knowledge of cloud infrastructure components and the trade-offs between different virtualization approaches.
