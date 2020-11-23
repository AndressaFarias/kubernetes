# O que o serviço DNS do Kubernetes fornece?

Funcionamento: 

* Um serviço chamado `kube-dns` e um ou mais pods são criados.
* O serviço `kube-dns` escuta por eventos **service** e **endpoint** da API do Kubernetes e atualiza seus registros DNS quando necessário. Esses eventos são disparados quando você cria, atualiza ou exclui serviços do Kubernetes e seus pods associados.
* O kubelet define a opção `nameserver` do `/etc/resolv.conf` de cada novo pod para o IP do cluster do serviço `kube-dns`, com opções apropriadas de `search` para permitir que nomes de host mais curtos sejam usados:




# Referencias 
https://www.digitalocean.com/community/tutorials/uma-introducao-ao-servico-de-dns-do-kubernetes-pt