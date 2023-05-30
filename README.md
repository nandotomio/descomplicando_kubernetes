# descomplicando_kubernetes

Repositório criado para o curso de Descomplicando o Kubernetes da LinuxTips.

## Criar o cluster com kind:

```bash
kind create cluster --config kind-3nodes.yaml --name kind-multinodes

# Remover o cluster:
kind delete cluster --name kind-multinodes
```

## Criar o template de um pod:

```bash
kubectl run meu-nginx --image nginx --port 80 --dry-run=client -o yaml > pod-template.yaml

# Para aplicar o template:
kubectl apply -f pod-template.yaml

# Para deletar o pod:
kubectl delete -f pod-template.yaml
```

## Expor do pod para o mundo externo:

```bash
# Para expor utilizando o tipo ClusterIP:
kubectl expose pod meu-nginx

# Para expor utilizando o tipo NodePort:
kubectl expose pod meu-nginx --type=NodePort

# Para remover o serviço:
kubectl delete service meu-nginx
```

# Listar todos os recursos do cluster:

```bash
kubectl get all
```