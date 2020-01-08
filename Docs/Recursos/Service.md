# Serviços

* No Kubernetes, um serviço é um componente que atua como um balanceador de carga básico interno e um embaixador para os pods. 

* Um serviço agrupa coleções lógicas de pods que executam a mesma função para apresentá-las como uma entidade única.

* Um serviço pode ser implantado para que possa rastrear e rotear todos os containers de backend de um determinado tipo. 

* Os consumidores internos precisam apenas saber o endpoint estável fornecido pelo serviço. 

* O endereço IP de um serviço permanece estável, independentemente das alterações nos pods para os quais ele é encaminhado. 

* Sempre que for preciso fornecer acesso a um ou mais pods para outro aplicativo ou para consumidores externos, é preciso configurar um serviço. 
    Por exemplo, se você tiver um conjunto de pods executando servidores web que devem ser acessíveis pela Internet, um serviço fornecerá a abstração necessária. Da mesma forma, se seus servidores web precisarem armazenar e recuperar dados, você deverá configurar um serviço interno para fornecer acesso aos seus pods de banco de dados.

* Serviços, por padrão, só estão disponíveis usando um endereço IP roteável internamente, eles podem ser disponibilizados fora do cluster, escolhendo uma das várias estratégias. 
    
    * **ClusterIP:** O IP válido fornecido é válido dentro do cluster
    
    * **NodePort:** disponibiliza uma porta estática na interface de rede externa de cada node. O tráfego para a porta externa será roteado automaticamente para os pods apropriados usando um serviço IP de cluster interno. portas diponibiizadas fiam o range 3000-32767

    * **LoadBalancer:** cria um balanceador de carga externo para rotear para o serviço usando a integração do balanceador de carga do Kubernetes do provedor de nuvem. O cloud controller manager criará o recurso apropriado e o configurará usando os endereços de serviço interno.




[Serviços](https://www.digitalocean.com/community/tutorials/uma-introducao-ao-kubernetes-pt#componentes-do-servidor-mestre)