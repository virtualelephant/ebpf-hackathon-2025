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
