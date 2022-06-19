# Intalação Minikube

# Instalação Kubectl

# Comandos Minikube

**Comandos de Inicializaão**
| Comando                                       | Descrição               |
| --------------------------------------------- | ----------------------- |
| minikube start                                | Inicializa o _minikube_ | 
| sudo minikube start --vm-driver=none          | Quando não é utilizado um hyprvisor  |
| minikube stop                                 | Para parar o cluster |
| minikube delete                               | Para limpar e apagar |
| minikube dashboard                            | Mostra o dashbard o nosso cluster Kubernetes |
| minikube service <nomeDoArquivoService> --url | Retorna o IP e a porta do serviço  



# Comandos Kubectl

**Comandos de configuração do ambiente**

| Comando                             | Descrição               |
| ----------------------------------- | ----------------------- |
| kubectl config use-context minikube | Para especidifcar o conteto que queremos tratabalhar, quando estamos trabalhando com diferentes clusters |

**Comandos relacionados ao ambiente**
`kubectl get nodes` | retorna os nodes existentes do cluster |
`kubectl get all`   | Retorn todas as informações do cluster | 

**Comandos relacionaos aos PODs**

| Comando                           | Descrição                                                     |
| --------------------------------- | ------------------------------------------------------------- |
| kubectl create -f <arquivo>       | Configura o objeto de acordo com o que fizemos no <arquivo>   |
| kubectl get pods                  | Verificar se/quais pods estão em execução                     | 
| kubectl delete pods <nomePod>     | Remove o Pod                                                  |
| kubectl describe pods             | Motra vários detalhes sobre os pods (como endereo de ip)      |

**Comandos relacionados aos Deployments**
| Comando                 | Descrição                                   |
| ----------------------- | ------------------------------------------- |
| kubectl get deployments | Retorna quais Deployments estão em execução |


kubectl get pod -l app.kubernetes.io/name=kube-state-metrics --all-namespaces


