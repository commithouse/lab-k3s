# 1. Instalar k3s 

Vide documentação
https://docs.k3s.io/

```shell
# Acessar usuário root
sudo su
# Instalar K3S com kubectl
curl -sfL https://get.k3s.io | sh -
# Habilitar permissão para usuário ubuntu obter configuração de acesso ao K8S
echo K3S_KUBECONFIG_MODE=\"644\" >> /etc/systemd/system/k3s.service.env
# Restart do serviço k3s para carregar nova config
systemctl restart k3s
```

# 2. Verificar status do cluster
```shell
su ubuntu

kubectl get nodes
```

# 3 Criar deployment

Comandos de deployment obtidos em:
https://kubernetes.io/docs/tutorials/hello-minikube/

```shell
# Lista os nós do cluster
kubectl get nodes

# Cria um deployment chamado hello-node com a imagem especificada
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080

# Lista os deployments existentes
kubectl get deployments

# Lista os pods em execução
kubectl get pods

# Mostra os eventos recentes do cluster
kubectl get events

# Exibe a configuração atual do kubectl
kubectl config view

# Expõe o deployment hello-node como um serviço do tipo LoadBalancer na porta 8080
kubectl expose deployment hello-node --type=LoadBalancer --port=8080

# Lista os serviços disponíveis no cluster
kubectl get services
```

# 4 Validando deploy e serviço

```shell
# Obtenha o <EXTERNAL-IP>
kubectl get services

# teste a chamada com curl
curl http://<EXTERNAL-IP>:8080

# verifique a saida retornada
```

Com isso você terminou seu primeiro lab de k8s! 👍