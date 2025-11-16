# Full-Stack Cilium on VCF/NSX-T: A Brownfield Zero-Trust Blueprint

## The Problem
Enterprise who are leveraging VCF as their private cloud platform, with its native NSX-T integration, want integration between the North-South Distributed Firewall (DFW) and Cilium's Kubernetes-native networking without having to perform a rip-and-replace. This project shows exactly how to layer **Cilium** in an **NSX-T** world and get to zero-trust fast.

## The Details
Teams need a proven pattern to:
- advertise Kubernetes routes/services upstream without hacky-workarounds
- enforce **zero-trust** between environments -- dev vs stage vs prod
- keep a central **GitOps control plane** (ArgoCD) that can deploy into isolated clusters
- maintain strict least-privilege

### Logical Diagram

![alt text](images/eBPF%20Hackathon%20Diagram.png)