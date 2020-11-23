# Nomes e Id de Objetos
Cada objeto em seu cluster tem um _Nome_ que é exclusivo para aquele tipo de recurso. Cada objeto Kubernetes também tem um _UID_ que é único em todo o cluster.

Por exemplo, você só pode ter um Pod denominado `myapp-1234` no mesmo namespace, mas pode ter um Pod e um Deployment, cada um denominado `myapp-123`.

Para atributos não exclusivos fornecidos pelo usuário, o Kubernetes fornece __labels__ e __annotations__.

## Nomes

Um string fornecida pelo client que se refere a um objeto em recurso URL pode ser `/api/v1/pods/some-name`

Apenas um objeto de determinado tipo pode ter um determinado nome por vez. No entanto, se você excluir o objeto, poderá criar um novo objeto com o mesmo nome.

Abaixo estão três tipos de restrições de nome comumente usadas para recursos.

### DNS Subdomain Names 

A maioria dos tipos de recursos exige um nome que pode ser usado como um nome de subdomínio DNS, conforme definido no RFC 1123. Isso significa que o nome deve:
* conter no máximo 253 caracteres 
* conter apenas caracteres alfanuméricos minúsculos, '-' ou '.' 
* comece com um caractere alfanumérico 
* termine com um caractere alfanumérico


### DNS Label Names 

Alguns tipos de recursos exigem que seus nomes sigam o padrão de rótulo DNS, conforme definido no RFC 1123. Isso significa que o nome deve:
* conter no máximo 63 caracteres 
* conter apenas caracteres alfanuméricos minúsculos ou '-' 
* comece com um caractere alfanumérico 
* termine com um caractere alfanumérico


### Nomes de segmento de caminho

Alguns tipos de recursos requerem que seus nomes possam ser codificados com segurança como um segmento de caminho. Em outras palavras, o nome não pode ser "." ou ".." e o nome não pode conter "/" ou "%".

Aqui está um exemplo de manifesto para um pod chamado `nginx-demo`.

~~~yaml
    apiVersion: v1
    kind: Pod
    metadata:
    name: nginx-demo
    spec:
    containers:
    - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
~~~

Nota: Alguns tipos de recursos têm restrições adicionais em seus nomes

## UIDs 
Uma string gerada pelos sistemas Kubernetes para identificar objetos de forma exclusiva.

Cada objeto criado ao longo de toda a vida de um cluster do Kubernetes tem um UID distinto. Destina-se a distinguir entre ocorrências históricas de entidades semelhantes.



# Referencias
 https://raiadrogasil.zoom.us/j/661394191?pwd=bjkrTVBEK0hBMEd6QW1sUTQ3Y0VNQT09