# Full-Stack Cilium on VCF/NSX-T: A Multi-Layered Zero-Trust Blueprint

## Ansible Playbooks and Galaxy Collections

Install the necessary Ansible Galaxy Collections:
```bash
ansible-galaxy collection install vmware.nsxt
```

## Ansible Vault for repostitory
Create the Ansible Vault file for the NSX-T credentials:
```bash
cd ansible
ansible-vault create ../../vars/nsxt_credentials.yml
```

```yaml
nsxt_password: "YOUR_NSXT_PASSWORD"
```

## Playbook Execution
Create the zero-trust security policies for each segment (dev, stage, prod):
```bash
ansible-playbook -i inventories/inventory.ini playbooks/nsx/dfw-zero-trust-policy.yml --ask-vault-pass
```

## Cilium BGP and Load Balancer IP Pool
Modify and apply the YAML files within each cluster (dev, stage, prod) to configure the Kubernetes cluster and prepare them for the full-stack integration.
```bash
kubectl apply -f k8s/<ENV>/bgp/01_ip_pool.yaml
kubectl apply -f k8s/<ENV>/bgp/02_bgp_advertisements.yaml
kubectl apply -f k8s/<ENV>/bgp/03_bgp_peer_config.yaml
kubectl apply -f k8s/<ENV>/bgp/04_bgp_cluster_config.yaml
```

## Deploy a smoke-test application
Validate the Gateway API and BGP implementation is fully working across the network stack.
```bash
kubectl apply -f k8s/99_smoke_test.yaml
```

Verify a VIP was allocated from the IP pool and the pods are running:
```bash
kubectl get all
```
