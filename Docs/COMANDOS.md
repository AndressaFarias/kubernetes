> Lista todos os cronJobs do cluster

kubectl get cronjob --all-namespaces




kubectl get pods --all-namespaces | grep Terminating | while read line; do pod_name=$(echo $line | awk '{print $2}' ) name_space=$(echo $line | awk '{print $1}' ); 

kubectl delete pods $pod_name -n $name_space --grace-period=0 --force; done





ALL EVICTED
===========
kubectl get pods --all-namespaces | grep Evicted | awk '{print $2 " --namespace=" $1}' | xargs -n 2 -d '\n' bash -c 'kubectl delete pod $0 $1'


[Ontem 16:55] Vitor Chaves de Oliveira
    
kubectl logs <pod-name> -c <conatiner_name>
​[Ontem 16:59] Andressa Fernanda Idalgo de Farias
    no caso seria o container Id ?
​[Ontem 17:01] Vitor Chaves de Oliveira
    pra pegar o nome dos containers ->
​[Ontem 17:02] Vitor Chaves de Oliveira
    kubectl get pods POD_NAME_HERE -o jsonpath='{.spec.containers[*].name}'
 


retornar imagem que está sendo executada no container 
kubectl get pods POD_NAME_HERE -o jsonpath='{.spec.template.spec.image}'


verificar a porta que o container está respondendo para fazer o port-forward
kubectl -n monitoring get pod prometheus-prometheus-kube-prometheus-prometheus-0 --template='{{(index (index .spec.containers 0).ports 0).containerPort}}{{"\n"}}'

kubectl -n kubecost get pods --all-namespaces -o jsonpath="{.items[*].spec.containers[*].image}" |\
tr -s '[[:space:]]' '\n' |\
sort |\
uniq -c


## resourceVersion
listar todos os resourceVersion dos pods em execução

`kubectl get pods -o custom-columns=NAME:.metadata.name,RSRC:.metadata.resourceVersion --all-namespaces`


kubectl get deploy myapp -o jsonpath='{.metadata.annotations.deployment\.kubernetes\.io/revision}'



{"metadata":{"annotations":{"kubectl.kubernetes.io/last-applied-configuration":"{\"apiVersion\":\"v1\",\"kind\":\"Service\",\"metadata\":{\"annotations\":{\"kubernetes.io/change-cause\":\"kubectl apply --filename=apps/fiscal/kubernetes/stg/ --record=true\"},\"labels\":{\"app\":\"fiscal-grpc\"},\"name\":\"fiscal-grpc\",\"namespace\":\"fiscal\"},\"spec\":{\"ports\":[{\"name\":\"grpc-port\",\"port\":50051,\"targetPort\":50051},{\"name\":\"http-transcoder\",\"port\":8051,\"protocol\":\"TCP\",\"targetPort\":8051}],\"selector\":{\"app\":\"fiscal-grpc\"}}}\n"},"creationTimestamp":null,"resourceVersion":null,"uid":null},"spec":{"$setElementOrder/ports":[{"port":50051},{"port":8051}],"clusterIP":null,"clusterIPs":null,"ipFamilies":null,"ipFamilyPolicy":null,"ports":[{"port":50051,"protocol":null},{"$patch":"delete","port":50443}],"sessionAffinity":null,"type":null},"status":null}
