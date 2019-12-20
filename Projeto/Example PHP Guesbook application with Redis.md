

# Iniciando o Redis

O aplicativo de livro de visitas usa o Redis para armazenar seus dados. Ele grava seus dados em uma instância principal do Redis e lê dados de várias instâncias escravas do Redis.

## Criando a implantação Redis Master


## Criando a implantação Redis Slave

As implantações são dimensionadas com base nas configurações definidas no arquivo de manifesto. Nesse caso, o objeto Deployment especifica duas réplicas

Se não houver réplicas em execução, essa implantação iniciará as duas réplicas no cluster de contêineres. Por outro lado, se houver mais de duas réplicas em execução, ela será reduzida até que duas réplicas estejam em execução.


---
application/guestbook/redis-slave-deployment.yaml 

apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: redis-slave
  labels:
    app: redis
spec:
  selector:
    matchLabels:
      app: redis
      role: slave
      tier: backend
  replicas: 2
  template:
    metadata:
      labels:
        app: redis
        role: slave
        tier: backend
    spec:
      containers:
      - name: slave
        image: gcr.io/google_samples/gb-redisslave:v3
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
        env:
        - name: GET_HOSTS_FROM
          value: dns
          # Using `GET_HOSTS_FROM=dns` requires your cluster to
          # provide a dns service. As of Kubernetes 1.3, DNS is a built-in
          # service launched automatically. However, if the cluster you are using
          # does not have a built-in DNS service, you can instead
          # access an environment variable to find the master
          # service's host. To do so, comment out the 'value: dns' line above, and
          # uncomment the line below:
          # value: env
        ports:
        - containerPort: 6379
--


## Configurar e expor o frontend do Gestbook

O aplicativo de _guestbook_ possui um front-end da web que atende às solicitações HTTP escritas em PHP. Ele está configurado para conectar-se ao serviço redis-master para solicitações de gravação e ao serviço redis-slave para solicitações de leitura.

### Criando a implantação do frontend do Guestbook

# Criando o Service do Frontend

Os serviços _redis-slave_ e _redis-master_ que foram aplicados só podem ser acessados ​​no cluster de contêineres porque o tipo padrão para um Serviço é ClusterIP.

Para que os visitantes possam acessar seu guestbook, configure o Service frontend  para ser visível externamente, para que um cliente possa solicitar o Service de fora do cluster de contêineres

# Acessar o Service Frontend

**VIA NODEPORT**

Se o deploy da aplicação fio feito o Mikikube ou um um cluster local, precisamos encontrar o endereço IP para acessar o Guestbook.

* Execute o seguinte comando para obter o endereço IP do serviço de front-end.

    minikube service frontend --url

    A resposta deve ser semelhante a esta: 

    http://192.168.99.100:31323

**VIA LOADBALACER**

Se o deploy do frontend-service.yaml foi feito com o tipo: LoadBalancer, será preciso encontrar o endereço IP para visualizar o Guestbook.

* Execute o seguinte comando para obter o endereço IP do serviço de front-end.

    kubectl get service frontend


