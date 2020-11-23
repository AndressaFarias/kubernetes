kubectl get pods --all-namespaces | grep Terminating | while read line; do pod_name=$(echo $line | awk '{print $2}' ) name_space=$(echo $line | awk '{print $1}' ); kubectl delete pods $pod_name -n $name_space --grace-period=0 --force; done

 

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
 
