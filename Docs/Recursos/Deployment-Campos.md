Kubernetes

**progressDeadlineSeconds:** Usado para auxiliar dacausa de possivis falhs no momento do deploy.
Indica o número de segundos que o Controller do Deployment aguarda antes de indicar (no status do Deployment ) que o progresso do Deployment foi interrompido.

**revisionHistoryLimit:** Esse campo pode ser definido em um Deployment para especificar quantos _ReplicaSet_ antigos por _Deploymente_ devem ser mantidos.


**.spec.strategy** 
specifies the strategy used to replace old Pods by new ones.
PORTUGUÊS
especifica a estratégia usada para substituir os Pods antigos por novos


**.spec.strategy.type** 
can be “Recreate” or “RollingUpdate”. “RollingUpdate” is the default value.
PORTUGUÊS
pode ser "Recreate" ou "RollingUpdate". "RollingUpdate" é o valor padrão.


**Recreate Deployment**
All existing Pods are killed before new ones are created when .spec.strategy.type==Recreate.
PORTUGUÊS
Todos os Pods existentes são eliminados antes da criação de novos quando
`.spec.strategy.type==Recreate`

**Rolling Update Deployment**
The Deployment updates Pods in a rolling update fashion when `.spec.strategy.type==RollingUpdate`. You can specify maxUnavailable and maxSurge to control the rolling update process.
PORTUGUÊS
A Implantação atualiza os Pods de maneira contínua quando `.spec.strategy.type==RollingUpdate`. Podem ser especificados os campos `maxUnavailable` e `maxSurge` para controlar o processo de atualização sem interrupção.

**Max Unavailable**
É um campo opcional que especifica o número máximo de Pods que podem estar indisponíveis durante o processo de atualização. O valor pode ser um número absoluto (por exemplo, 5) ou uma porcentagem de Pods desejados (por exemplo, 10%). O número absoluto é calculado a partir de porcentagem, arredondando para baixo. O valor não pode ser 0 se `.spec.strategy.rollingUpdate.maxSurge` for 0. 

O valor padrão é 25%.

**Max Surge**
É um campo opcional que especifica o número máximo de Pods que podem ser criados sobre o número desejado de Pods. 

O valor padrão é 25%.

**selector** 
O campo `selector`define como o Deployment encontra quai Pods deve gerenciar.

**imagePullPolicy**
Refere-se a politica de atualização da imagem. Por padrão é utilizado `IfNotPresent` que faz com que o _Kubebelet_ pule a extração de uma imagem se ela já existir. Se for necesário sempre forçar o pull da imagemm definir o `imagePullPolicy`contêiner como `Always`.

**stdin**
É um campo booleano.
Se este contêiner deve alocar um buffer para stdin no tempo de execução do contêiner. Se isso não estiver definido, as leituras de stdin no contêiner sempre resultarão em EOF. O padrão é falso.

[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.10/]

**terminationMessagePath**
O Kubernetes recupera mensagens de finalização do arquivo de mensagens de finalização especificado no `terminationMessagePath` de um Contêiner, que como valor padrão de /dev/termination-log. Ao personalizar esse campo, você pode dizer ao Kubernetes para usar um arquivo diferente. Os Kubernetes usam o conteúdo do arquivo especificado para preencher a mensagem de status do Contêiner em caso de êxito e falha

[https://kubernetes.io/docs/tasks/debug-application-cluster/determine-reason-pod-failure/#customizing-the-termination-message]

**terminationMessagePolicy**
lém disso, os usuários podem definir o terminationMessagePolicycampo de um contêiner para personalização adicional. Esse campo é padronizado como “ File”, o que significa que as mensagens de encerramento são recuperadas apenas do arquivo de mensagens de encerramento. Ao definir terminationMessagePolicycomo “ FallbackToLogsOnError”, você pode dizer ao Kubernetes para usar o último pedaço da saída do log do contêiner se o arquivo de mensagem de encerramento estiver vazio e o contêiner sair com um erro. A saída do log é limitada a 2048 bytes ou 80 linhas, o que for menor.

[https://kubernetes.io/docs/tasks/debug-application-cluster/determine-reason-pod-failure/]
