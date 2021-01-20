# Service

É uma maneira de expor uma aplicação em execução em um conjunto de Pods como um serviço da rede.

O Kubernetes fornece aos Pods seus próprios endereços IP e um único nome DNS para um conjunto de Pods, e pode balancear a carga entre eles.

## Motivação
Como os Pods no Kubernetes são efêmeros ao serem recriados eles perdem os endereço IP, desta forma de Pods _fron-end_ que utilizam funcionalidades de Pods _back-end_ perdem os endereços de IP de comunicação.

## Recuros dos _Services_
No Kubernetes, um Serviço é uma abstração que define um conjunto lógico de Pods e uma política pela qual acessá-los (às vezes esse padrão é chamado de microsserviço). O conjunto de Pods segmentados por um Serviço geralmente é determinado por um `selector`.

Por exemplo, considere um back-end de processamento de imagem _stateless_ (sem estado)que esteja executando com três réplicas. Essas réplicas são fungíveis (podem ser substituídos por outros de mesma espécie, qualidade e quantidade) - os front-ends não se importam com o back-end que usam. Embora os Pods reais que compõem o conjunto de back-end possam mudar, os clientes de front-end não precisam estar cientes disso, nem precisam acompanhar o próprio conjunto de back-end.

A abstração de serviço permite esse desacoplamento.

## Definindo um _Service_ 
Um serviço no Kubernetes é um objeto REST, semelhante a um Pod. Como todos os objetos REST, você pode faz um `POST` com a definição de Serviço para o API server criar uma nova instância.

Por exemplo, suponha que você tenha um conjunto de Pods que cada um escuta na porta TCP 9376 e carrega um _label__ `app=MyApp`

```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

(Service)[https://kubernetes.io/docs/concepts/services-networking/service/]