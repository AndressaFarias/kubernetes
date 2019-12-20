# Instalação 

**Windows**
* Realizar o download nesse link: https://storage.googleapis.com/minikube/releases/v0.22.1/minikube-windows-amd64.exe

* Uma vez que o Download for concluído, ir até o local onde o arquivo foi salvo e o renomeie para _minikube.exe_

* Feito isso, adicione esse caminho do arquivo para as variáveis de ambiente de seu computador.
    * Clique com o botão direito do mouse em _Este computador_ e depois em _Propriedades_

    * Na sequência, clique em _Configurações avançadas do ambiente_;

    * Posteriormente, clique em _Variáveis de ambiente_

    * Na opção _variáveis do sistema_, escolha a opção _Path_ e depois clique no botão _Editar_ para adicionar o caminho no qual o minikube está localizado;

**Utilizando o chocolatery**
__*Baixando o chocolatery*__

* No Power Shell como Adm executar o comando:

    Set-ExecutionPolicy Bypass -Scope Process -Force; iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex

__*Instalando o minikube*__
* No Power Shell como Adm executar o comando:
    
    `choco install minikube`


_*Subindo o Minikube*_

* No _Power Shell_ como Administrador executar o comando:

    `minikube start`


# Referencia:
 Instalando o chocolatery: [https://chocolatey.org/docs/installation]
 Instalando o minikube: [https://kubernetes.io/docs/tasks/tools/install-minikube/]



# OBS
* Usamos o _minikube_ para testar localmente o _Kubernetes_ ;
* O _minikube_ usa alguma virtualzção por baixo dos panos