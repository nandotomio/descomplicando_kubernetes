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

## Listar todos os recursos do cluster:

```bash
kubectl get all
```

## Acessar o pod:

O `attach` cria uma conexão com o pod, mas não abre um terminal. Ele faz o attach no processo principal do pod.
O `exec` cria uma conexão com o pod e abre um terminal.

```bash
kubectl attach meu-nginx -c meu-nginx -it

# Utilizando o comando exec:
kubectl exec -it meu-nginx -c meu-nginx -- /bin/bash
```

## Logs do pod:

```bash
# Para visualizar os logs de todos os containers do pod, de forma contínua:
kubectl logs meu-nginx -f

# Para visualizar os logs de um container específico de pod:
kubectl logs meu-nginx -c meu-nginx
```

## Criar um deployment:

```bash
k create deployment --image nginx --replicas 3 nginx-deployment --dry-run=client -o yaml > deployment.yaml
```

# Para monitorar o deployment:

```bash
kubectl rollout status deployment -n giropops nginx-deployment
```

# Para fazer o rollback:

```bash
# Para ver o histórico de rollout:
kubectl rollout history deployment -n giropops nginx-deployment
# Para ver uma revisão específica:
kubectl rollout history deployment -n giropops nginx-deployment --revision 1
# Para fazer o rollback:
kubectl rollout undo deployment -n giropops nginx-deployment
# Para fazer o rollback para uma revisão específica:
kubectl rollout undo deployment -n giropops nginx-deployment --to-revision 1
# Para pausar o rollout:
kubectl rollout pause deployment -n giropops nginx-deployment
# Para retomar o rollout:
kubectl rollout resume deployment -n giropops nginx-deployment
# Para restartar o rollout:
kubectl rollout restart deployment -n giropops nginx-deployment
# Para escalar o deployment:
kubectl scale deployment -n giropops nginx-deployment --replicas 5
```