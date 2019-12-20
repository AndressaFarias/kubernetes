Projetos reaizados conform acompanhamento dos vídeio de Kuberntes do Canal Future Cloud


Vídeos

Canal: **Future Cloud**

### **Mais Relevantes**

- Kubernetes na IBM Cloud (K8s - Parte 3) - Deploy da Aplicação (https://www.youtube.com/watch?v=EOE-d9_9Jek)
- Kubernetes na IBM Cloud (K8s - Parte 5) - Arquivo YAML (https://www.youtube.com/watch?v=lMXfZqBNrq4)
- Kubernetes na IBM Cloud (K8s - Parte 6) - AutoScaling (https://www.youtube.com/watch?v=97LqJiPJcDs)
- Kubernetes na IBM Cloud (K8s - Parte 7) - Persistent Volumes (https://www.youtube.com/watch?v=uOlOQlR0Mpk)
- Kubernetes na IBM Cloud (K8s - Parte 8) - Self Healing - (https://www.youtube.com/watch?v=o73uX2SvXxc)
- Kubernetes (K8s - Parte 15) - Como usar o Readiness e o Liveness Probe no seu projeto de devops - (https://www.youtube.com/watch?v=brQh8bjXL9Q)

### **Interesantes**
- Kubernetes na IBM Cloud (K8s - Parte 4) - Container Registry (https://www.youtube.com/watch?v=MiWVZNWVqOw)







**Persistent Volumes**
* Criar o yaml
* `kubectl apply -f myvol.yaml`
* `kubectl get pvc`
    * Aguardar o pv ficar com status _Bound_
* criar o yaml do Pod
* `kubectl apply -f itiro.yaml`
* `kubectl get pods`
* `kubectl describe <nomeDoContainer>`


**AutoScaling**
Criando a aplicação principal php-apache e determinando os paramêtros para _autoscale_;

`kubectl run php-apache --image=gcr.io/google_containers/hpa-example --requests=cpu=200m --expose --port=80`

`kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10`
<!-- 
php-apache : é o nome do deployment criado 
--cpu-percent=50 : limite que ao ser atingido deve gerar um novo pod
--min=1 : quantidade minima de pods
--max=10 : quantidade máxima de pods 
-->

`kubectl get hpa`
<!--retorna o estado atual do hpa -->


Criar container que vai gerar carga para a aplicação

`kubectl run -i --tty load-generator --image=busybox bin/sh`

Será habilitado o shell do container. Criamos então o cript para gerar o load.

`while true; do wget -q -O- http://php-apache.default.svc.cluster.local; done`

aguarde algun minutos (1-3). finalize a execução do comando com `ctrl-c` em seguida sai do hel `exit`ao verifcar o estado do hpa é preciso ver qu o numero de pods tenha aumentado.

`kubectl get hpa`


**Arquivo Yaml**

1. Clone do repositório no Git -  `git clone git@github.com:itirohidaka/K8s_yaml.git`
2. kubectl create -f guestbook1.yaml
3. kubectl get pods
4. kubectl get deployments
5. kubectl get services (para obter o IP e porta em que está sendo executado o front)
6. kubectl delete -f guestbook1.yaml (para deletar todos os componentes)

**Deploy da Aplicação**

```
kubectl run mongo --image=mongo --port=2017

kubectl expose deployment mongo --type=NodePort

kubectl run myemp --image=kavisuresh/employee --port=80

kubectl expose deployment myemp --type=nodePort --port=80 --targetPort=8888

kubectl proxy

Acesso pelo IP público do Nó

```
