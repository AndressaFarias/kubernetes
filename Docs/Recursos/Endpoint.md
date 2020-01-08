# Criando Endpoints para Gluster

Uma definição de _endpoint_ define o cluster GlusterFS como **EndPoints** nclui os endereços IP dos seus servidores Gluster.

O valor da porta pode ser qualquer valor numérico dentro do intervalo de portas aceito. Opcionalmente, você pode criar um serviço que persista os endpoints.

_Exemplo 1. Definição de serviço Gluster:_

```yaml
apiVersion: v1
kind: Service
metadata:
  name: glusterfs-cluster  #1
spec:
  ports:
  - port: 1
```

#1 Esse nome deve ser definido no _endpoint_ para combinar o endpoint a esse serviço.

Verificar que o service foi criado

`kubectl get service`

Devemos definir então o Gluster endpoints
_Exemplo 2. Definição de endpointss do Gluster_

```yaml
apiVersion: v1
kind: Endpoints
metadata:
  name: glusterfs-cluster       #1
subsets:
  - addresses:
      - ip: 192.168.122.221     #2
    ports:
      - port: 1
  - addresses:
      - ip: 192.168.122.222     #2
    ports:
      - port: 1                 #3
```
#1 - Este nome deve corresponder ao nome do serviço do Exemplo 1.
#2 - Os valores de **ip** devem ser os endereços IP reais de um servidor Gluster, não os nomes de host.
#3 - O número da porta é ignorado.


# Criando o volume persistente

Em seguida, defina o PV em uma definição de objeto antes de criá-lo:

_Exemplo 3. Definição de objeto de persistent volume usando o GlusterFS_

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: gluster-default-volume      #1
spec:
  capacity:
    storage: 2Gi        #2
  accessModes:          #3
    - ReadWriteMany
  glusterfs:            #4
    endpoints: glusterfs-cluster    #5 
    path: myVol1                    #6
    readOnly: false
  persistentVolumeReclaimPolicy: Retain     #7
```

#1 - O nome do volume. É assim que é identificado por meio de declarações de volume persistentes ou de pods.

#2 - A quantidade de armazenamento alocado para este volume.

#3 - **accessMode** são usados ​​como etiquetas para combinar com um PV e um PVC. Atualmente, eles não definem nenhuma forma de controle de acesso.

#4 - O tipo de volume que está sendo usado, neste caso, o plug-in glusterfs.

#5 - O nome dos endpoints que define o cluster do Gluster criado no Exemplo 1.

#6 - O volume do Gluster que será acessado, conforme mostrado no comando `gluster volume status`

#7 - A política de reciclagem atualmente não é suportada pelo glusterfs





