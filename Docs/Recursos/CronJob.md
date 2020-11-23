# CronJOB

**concurrencyPolicy**[1]
O campo .spec.concurrencyPolicy é opcional. Ele especifica como tratar execuções simultâneas de um job criado por este cronJon.

* Allow (padrão): o trabalho cron permite a execução simultânea de jobs

* Forbid: o cron job não permite execuções simultâneas; se estiver na hora da execução de um novo job e a execução anterior ainda não tiver sido concluída, o ccronjob ignora a nova execução;

* Replace: Se estiver na hora de uma nova execução do job e a execução anterior ainda não tiver sido concluída, o cronJob substituirá a execução atualmente em execução por uma nova execução.

**successfulJobsHistoryLimit** e **failedJobsHistoryLimit**[1]
É um campo opcional.
Esses campos especificam quantos trabalhos concluídos e com falha devem ser mantidos.
Por padrão, eles são definidos como 3 e 1, respectivamente. Definir um limite como 0 corresponde a não manter o tipo de trabalho correspondente após a conclusão.


**backoffLimit** [2]
Política de falha de backoff do pod. 
Há situações em que você deseja falhar em um trabalho após algumas tentativas devido a um erro lógico na configuração etc. Para fazer isso, defina `.spec.backoffLimit` para especificar o número de tentativas antes de considerar um Job  com falha. O _back-off limit_ default é 6.

**schedulerName** [3]
Um aspecto importante a ser observado aqui é que o nome do _scheduler_ especificado como argumento para o comando do _scheduler_ especificação do contêiner deve ser exclusivo.

Referencias:

[1] https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/
[2] https://kubernetes.io/docs/concepts/workloads/controllers/job/

