# Full-Stack Cilium on VCF/NSX-T: A Multi-Layered Zero-Trust Blueprint

## The Problem
Enterprise who are leveraging VCF as their private cloud platform, with its native NSX-T integration, want integration between the North-South Distributed Firewall (DFW) and Cilium's Kubernetes-native networking without having to perform a rip-and-replace. This project shows exactly how to layer **Cilium** in an **NSX-T** world and get to zero-trust fast.

## The Details
Teams need a proven pattern to:
- advertise Kubernetes routes/services upstream without hacky-workarounds
- enforce **zero-trust** between environments -- dev vs stage vs prod
- keep a central **GitOps control plane** (ArgoCD) that can deploy into isolated clusters
- maintain strict least-privilege

### Logical Diagram

![logical diagram](images/eBPF%20Hackathon%20Diagram.png)

### What we've built
A reference architecture that **coexists**, not replaces:

**NSX-T (north-south):**
- Three NSX segments (dev, stage, prod) with DFW rules that block inter-segment traffic; only automation and HTTP(S) ingress are allowed.

**Cilium (east-west + app layer):**
- Cilium BGP Control Plane peering worker nodes to NSX-T T0 to advertise Pod/Service/LB routes.
- Gateway API for ingress/egress, owned by Cilium.
- eBPF-backed L3 - L7 policies (CiliumNetworkPolicy/Clusterwide) to enforce namespace/identity isolation.
- Hubble for real-time flow visibility.

**Automation plane:**
- ArgoCD in the prod cluster deploys to dev & stage over tightly scoped access to :6443.
- Ansible is the only SSH/API actor permitted into dev/stage segments.