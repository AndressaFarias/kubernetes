Canal: **Future Cloud**



-  Kubernetes na IBM Cloud (K8s - Parte 3) - Deploy da Aplicação (https://www.youtube.com/watch?v=EOE-d9_9Jek)
- 
-  Como usar o Readiness e o Liveness Probe [vídeo 15]- https://www.youtube.com/watch?v=brQh8bjXL9Q



- Kubernetes na IBM Cloud (K8s - Parte 4) - Container Registry (https://www.youtube.com/watch?v=MiWVZNWVqOw)




**Deploy da Aplicação**

```
kubectl run mongo --image=mongo --port=2017

kubectl expose deployment mongo --type=NodePort

kubectl run myemp --image=kavisuresh/employee --port=80

kubectl expose deployment myemp --type=nodePort --port=80 --targetPort=8888

kubectl proxy

Acesso pelo IP público do Nó

```

