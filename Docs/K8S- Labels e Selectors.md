# Kubernetes :ferris_wheel: Labels e Selectors 

**Os _labels_ são pares de chave/valor anexados a objetos, como pods**. Os _labels_ devem ser usados ​​para especificar atributos de identificação de objetos significativos e relevantes para os usuários. Os **_labels_ podem ser usados ​​para organizar e selecionar subconjuntos de objetos**. Os _labels_ podem ser anexados aos objetos no momento da criação e, posteriormente, adicionados e modificados a qualquer momento. Cada objeto pode ter um conjunto de rótulos de chave/valor definido. Cada chave deve ser exclusiva para um determinado objeto.

```
metadata:  {
    labels: {
        key1: value1
        key2: value2
    }
}
```

Os _labels_ permitem consultas e são ideais para uso em UIs e CLIs. Informações não identificáveis ​​devem ser registradas usando anotações.


## Motivação
Os _labels_ permitem que os usuários mapeiem suas próprias estruturas organizacionais nos objetos do sistema de maneira pouco acoplada, sem exigir que os clientes armazenem esses mapeamentos.

Deploy de Service e os lotes de processamento de pipelines são entidades multidimensionais (por exemplo, várias partições ou deployments, várias faixas de liberação, várias camadas, vários micro-serviços por camada). O gerenciamento geralmente requer operações transversais, o que quebra o encapsulamento de representações estritamente hierárquicas, especialmente hierarquias rígidas determinadas pela infraestrutura e não pelos usuários.

Example labels:

```
"release" : "stable", 
"release" : "canary"

"environment" : "dev", 
"environment" : "qa", 
"environment" : "production"

"tier" : "frontend", 
"tier" : "backend", 
"tier" : "cache"

"partition" : "customerA", 
"partition" : "customerB"
```

## Sintaxe e conjunto de caracteres

Os _labels_ são pares de chave/valor. 
As **chaves de _labels_ válidas têm dois segmentos: um prefixo opcional e nome, separados por uma barra (/).**

O segmento de **_nome_** é obrigatório.
Deve ter 63 caracteres ou menos, começando e terminando com um caractere alfanumérico ( [a-z0-9A-Z]) com traços (-), sublinhados (_), pontos (.) e alfanuméricos no meio.

O **prefixo** é opcional. 
Se especificado, o prefixo deve ser um subdomínio DNS: uma série de rótulos DNS separados por pontos (.), com no máximo 253 caracteres no total, seguidos por uma barra (/).

Se o prefixo for omitido, presume-se que o rótulo Key seja privado para o usuário. Os componentes de sistema automatizados (por exemplo, kube-scheduler, kube-controller-manager, kube-apiserver, kubectl ou outra automação de terceiros) que adicionam rótulos aos objetos do usuário final devem especificar um prefixo

Os prefixos _kubernetes.io/_ e _k8s.io/_ são reservados para os principais componentes do Kubernetes.

Os valores válidos dos _labels_ devem ter 63 caracteres ou menos e devem estar vazios ou começar e terminar com um caractere alfanumérico ( [a-z0-9A-Z]) com traços (-), sublinhados (_), pontos (.) e alfanuméricos entre.

Por exemplo, aqui está o arquivo de configuração para um Pod que possui dois _labels_ `environment: production` e `app: nginx`:

```
apiVersion: v1
kind: Pod
metadata:
  name: label-demo
  labels:
    environment: production
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80
```

# Label selectors 

Ao contrário de nomes e UIDs (_User Interction Diagrams_), os **_labels_ não fornecem exclusividade. Em geral, esperamos que muitos objetos carregem os mesmos _labels_.**

**Através de um _label seletor_, o cliente/usuário pode identificar um conjunto de objetos.** O _label seletor_ é a primitiva de agrupamento principal no Kubernetes.

A API suporta atualmente dois tipos de _selectors_: _equality-base_ e _set-based_. Um _label selector_ pode ser composto de vários requisitos separados por vírgula. No caso de vários requisitos, todos devem ser satisfeitos para que o separador de vírgulas atue como um operador lógico AND (&&).

A semântica de _seletors_ vazios ou não especificados depende do contexto, e os tipos de API que usam _seletors_ devem documentar a validade e o significado deles.

> **Nota**: Para alguns tipos de API, como ReplicaSets, os _selectors_ de rótulo de duas instâncias não devem se sobrepor em um espaço para nome ou o controlador pode ver isso como instruções conflitantes e falhar ao determinar quantas réplicas devem estar presentes.

## Equality-based
Os _equality-based_ ou _unequality-based_ (requisitos de igualdade ou de desigualdade) permitem a filtragem por valores e chaves. Os objetos correspondentes devem satisfazer todas as restrições de rótulo especificadas, embora também possam ter rótulos adicionais. Três tipos de operadores são admitidos **=**, **==**, **!=**. Os dois primeiros representam igualdade (e são simplesmente sinônimos), enquanto o segundo representa desigualdade . Por exemplo:

```
environment = production
tier != frontend
```

O primeiro seleciona todos os recursos com chave _environmente_ com valor igual a _production_. O segundo seleciona todos os recursos com chave igual _tier_ e com valor diferentes de _frontend_ todos os recursos sem rótulos com a tierchave. Pode-se filtrar por recursos ao productionexcluir o frontenduso do operador de vírgula:environment=production,tier!=frontend

Um caso de uso para _labels equality-based_ necessitamos que os Pods especifiquem os critérios de seleção de nós. Por exemplo, o Pod abaixo seleciona nós com o rótulo “_accelerator=nvidia-tesla-p100_”.

```
apiVersion: v1
kind: Pod
metadata:
  name: cuda-test
spec:
  containers:
    - name: cuda-test
      image: "k8s.gcr.io/cuda-vector-add:v0.1"
      resources:
        limits:
          nvidia.com/gpu: 1
  nodeSelector:
    accelerator: nvidia-tesla-p100
```

## Set-based

_Labels set-based_ permitem filtrar as chaves de acordo com um conjunto de valores. Três tipos de operadores são suportados: **in**, **notin** e **exists** Por exemplo:

```
environment in (production, qa)
tier notin (frontend, backend)
partition
!partition
```

* **environment in (production, qa)**: seleciona todos os recursos com chave _environmente_ igual a _productionou_ ou _qa_. 

* **tier notin (frontend, backend)**: seleciona todos os recursos com chave _tier_ diferentes de _frontende_ and _backend_, e todos os recursos sem rótulos com a chave _tier_.

* **partition**: seleciona todos os recursos que possuem a _label_ com a chave _partition_; nenhum valor é verificado. 

* **!partition**: seleciona todos os recursos sem um _label_ com chave _partition_; nenhum valor é verificado. 

Os requisitos _set-based_ podem ser combinados com os requisitos _equality-base_. Por exemplo: 

`partition in (customerA, customerB), environment != qa`

# API

## Filtragem LIST e WATCH

As operações LIST e WATCH podem especificar _labels selectors_ para filtrar os conjuntos de objetos retornados usando um parâmetro de consulta. Ambos os requisitos são permitidos:

Os dois estilos de seletor de etiqueta podem ser usados ​​para listar ou observar recursos por meio de um cliente REST. 


`kubectl get pods -l environment=production, tier=frontend`

ou usando requisitos baseados em conjunto :

`kubectl get pods -l 'environment in (production), tier in (frontend)'`

Como já mencionado, os requisitos baseados em conjuntos são mais expressivos. 
Por exemplo, eles podem implementar o operador OR nos valores:

`kubectl get pods -l 'environment in (production, qa)'` 

ou restringindo a correspondência negativa via operador _exists_:

`kubectl get pods -l 'environment, environment notin (frontend)'`


#### Referencia
https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/ 