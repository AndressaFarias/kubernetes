
## *Pre-Requisitos*
* Haver um cluster;
    * Pode ser feito o deploy de um cluster utilizando o _Minikube_
* Ter um _Ingress controller_ em execução

## Habilitando o Ingress Contoller

* Para habilitar o controlador NGINX Ingress, execute o seguinte comando:
    `minikube addons enable ingress`

* Verifique se o controlador NGINX Ingress está em execução
    `kubectl get pods -n kube-system`
