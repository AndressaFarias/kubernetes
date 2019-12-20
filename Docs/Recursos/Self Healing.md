# Self Healing

É uma propriedade do K8s de autorecuperação do K8s. O K8S fica constantemente monitorando os componentes da aplicação e se um desses  componentes vier a falha ee é restartado ou recriado.

Na prática, é feita a definição de um deploymente e dentro dele deve haver a indicação de quantos Pos deves haver daquele componente. 

## Funcionamento 
Por exemplo, é definido que a camada Web de uma aplciação deve ter 3 pods. Então é criado um deployment chamado frontend onde é definido que devem existir os três Pods dessa aplicação. Esse estado é passdo dentro do nó master pelo _ replication controller_, e então ele envia essa informação ele envia para o kubelet dentro dos workers. Então kubelet fica monitorando os pod que estão dentro dos workers. E se um dos componentes falhar é feita a recuperação do componente.


## Referencia 
Kubernetes na IBM Cloud (K8s - Parte 8) - Self Healing - https://www.youtube.com/watch?v=o73uX2SvXxc