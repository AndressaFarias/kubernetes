# Atividade

Na demonstração para verificar o autoscaling será utiliada uma aplicaçaõ com PHP e Apache, será então criada um novo conteiner para que gere loadna aplicação, paa que seja testado o AutoScaling (HPA) no Kubernetes.

o K8s fica monitorando a CPU do Container Apache e quando o limite determiando for alcançado, novo pods serão criados, de forma a escalonar horizontalmente o cluster.

## Pasos Realizados

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