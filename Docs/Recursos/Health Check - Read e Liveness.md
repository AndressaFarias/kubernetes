# Health Check

Tipos:
* Readness
* Liveness

Métodos para verificar se o pod está Read e/ou Live (Probes)
* HTTP
* Comando
* TCP

## Readness
É mais utilizado no momento em que um pod está sendo criado.
Como nesse momento ele não tem capacidade de receber e processar um REQUEST. É necessário aguardar um tempo até ue o pod esteja em estado "OK" para receber o REQUESTs e repassar aos serviços. 

## Liveness
É o prcesso pra verificar se o pod está vivo ou morto.

# HTTP
Envia um REQUEST HTTP para o _Pod_;
Recebe uma resposta e se a resposta estiver entre 200 e 400 o estado está OK.

# Comando
Um determinado comando é definido dentro do yaml file.
O comando definido é executado dentro container. se o retorno de status for igual a zero, o container está OK, caso qualquer outro status seja recebido o container está NOK.

## TCP
É criada a conexão TCP com o _Pod_ se ela ocorrer com sucesso o _Pod_ está ok.

