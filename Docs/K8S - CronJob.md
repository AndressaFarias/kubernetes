# CronJob

## Como especificar quando o CronJob é executado [1]

O campo `spec.schedule` define quando e com que frequência o CronJob é executado, usando o formato crontab padrão do Unix. Todos os horários do CronJob estão em UTC: Há cinco campos, separados por espaços. Esses campos representam:

   1. Minutos (entre 0 e 59)
   2. Horas (entre 0 e 23)
   3. Dia do mês (entre 1 e 31)
   4. Mês (entre 1 e 12)
   5. Dia da semana (entre 0 e 6)
É possível usar os caracteres especiais a seguir em qualquer um dos campos `spec.schedule`:

* `?` é um valor de caractere curinga que corresponde a um único caractere.
* `*` é um valor curinga que corresponde a zero ou mais caracteres.
* `/` permite que você especifique um intervalo para um campo. 
Por exemplo, se o primeiro campo (o campo minutos) tem um valor de */5, significa “a cada 5 minutos”. Se o quinto campo (o do dia da semana) estiver definido como 0/5, significa “a cada cinco domingos”.

`schedule: "* */1 * * *" `

# Referencia:
[1] https://cloud.google.com/kubernetes-engine/docs/how-to/cronjobs?hl=pt-br#schedule