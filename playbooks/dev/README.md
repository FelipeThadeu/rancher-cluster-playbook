# Hosts / DNS local

No /etc/hosts do seu lab-node:
```
127.0.0.1   lab-node lab-rancher.local
```

Isso garante que o hostname usado pelo Rancher e TLS resolva.

# Rodar os playbooks

No seu nó único:
```
ansible-playbook -i ../../inventories/lab/hosts.yml playbooks/dev/bootstrap.yml
ansible-playbook -i ../../inventories/lab/hosts.yml playbooks/dev/rke2.yml
ansible-playbook -i ../../inventories/lab/hosts.yml playbooks/dev/rancher.yml
```

# Validar RKE2
```
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
/var/lib/rancher/rke2/bin/kubectl get nodes
```

# Saída esperada (single node):
```
NAME       STATUS   ROLES                  AGE   VERSION
lab-node   Ready    control-plane,master  1m    v1.24.9+rke2r1
```

# Validar Rancher

Acesse:

https://lab-rancher.local


⚠️ No lab você pode usar self-signed cert, então o browser vai avisar.

🔹 Dicas para lab

1. Não precisa desabilitar firewall, só abrir portas 6443 e 443

2. Pode usar 127.0.0.1 para simplificar

3. Ideal para testar playbooks antes de usar em cluster real

4. Pode adicionar --check no Ansible para simular execução sem aplicar:
```
ansible-playbook -i inventories/lab/hosts.yml playbooks/rke2.yml --check
```