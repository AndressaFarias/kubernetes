# Atribuindo Pods a nós

Você pode restringir um Pod para poder executar apenas em nós específicos ou preferir executar em nós específicos. Existem várias maneiras de fazer isso, e as abordagens recomendadas usam seletores de etiqueta para fazer a seleção. Geralmente, essas restrições são desnecessárias, pois o agendador fará automaticamente um posicionamento razoável (por exemplo, espalhe seus pods pelos nós, não o coloque em um nó com recursos livres insuficientes etc.), mas há algumas circunstâncias em que você pode querer ter mais controle sobre um nó no qual um pod chega, por exemplo, para garantir que um pod termine em uma máquina com um SSD conectado a ele ou para co-localizar pods de dois serviços diferentes que se comunicam muito na mesma zona de disponibilidade

## nodeSelector
`nodeSelector` é a forma mais simples recomendada de restrição de seleção de nós. `nodeSelector` é um campo do PodSpec. Ele especifica um mapa de pares de chave-valor. Para que o pod seja elegível para execução em um nó, ele deve ter cada um dos pares de chave-valore indicados como rótulos (também pode ter rótulos adicionais). O uso mais comum é um par de chave-valore. Vamos examinar um exemplo de como usar o `nodeSelector`.


### Step Zero : Prerequisitos
Este exemplo pressupõe que você tenha um conhecimento básico dos pods do Kubernetes e que configurou um cluster do Kubernetes.

### Step Um : Anexar rótulo ao nó
* Execute o comando `kubectl get nodes` para obter os nomes dos nós do cluster. 
* Escolha o que você deseja adicionar um rótulo e execute o comando `kubectl label node <node-name> <label-key> = <label-value>` para adicionar um rótulo ao nó que você escolheu. _Por exemplo_, se o nome do nó for `kubernetes-foo-node-1.ca-robinson.internal` e o rótulo desejado for `disktype = ssd`, pode ser executado o comando: `kubectl label nodes kubernetes-foo-node-1.ca -robinson.internal disktype=ssd`

Você pode verificar se funcionou reexecutando o comando `kubectl get nodes --show-labels` e verificando se o nó agora possui um rótulo. Também pode usado o comando `kubectl describe node "nodename"` do kubectl para descrever a lista completa de rótulos do nó especificado
