---
name: Adicionando novos recursos ao SDK
about: Guia para adicionar novos recursos ao SDK
title: ''
labels: ''
assignees: ''

---

Para que sejam incluídos novos recursos no SDK Java, deve ser criado um *client* (caso não exista), classes para que sejam montadas as requisições e interpretadas as respostas, além de testes unitários e integrados.
Segue abaixo guia de como contribuir com o nosso SDK:

### Criar *client* 
Deve-se criar um *client* para o recurso desejado caso ainda não exista.
Deve ser criado uma pasta com o nome do *client* dentro de **main/java/com/mercadopago/client**.
A nova classe deve extender a classe `MercadoPagoClient`, conter dois construtores (padrão e recebendo `MPHttpClient`), e os métodos pertinentes.
> Classe de exemplo: ***PaymentClient.java***.

### Criar arquivos para montar requisições
Dentro da mesma pasta devem ser criados os arquivos *builder* com sufixo `Request`, que serão utilizados para que as requisições sejam construídas.
O nome da classe deve ser formado pelo nome do client seguido pelos nomes dos nós e com o sufixo `Request`.
A classe deve ter as anotações `@Getter` e `@Builder`, e todos os atributos devem ser private final.
Consulte quais campos devem ser mapeados na [referência de API oficial do Mercado Pago](https://www.mercadopago.com.br/developers/pt/reference).
> Classe de exemplo: ***PaymentAdditionalInfoPayerRequest.java***.

### Criar arquivos de recursos para lidar com as respostas
Essas classes são os *DTOs* para interpretação e manipulação das respostas das APIs.
Deve ser criada uma pasta com o nome da feature dentro de **main/java/com/mercadopago/resources**.
A classe principal da resposta deve extender a classe `MPResources`.
Todas essas classes devem ser anotadas com `@Getter` e todos os atributos devem ser privados.
Consulte quais campos devem ser mapeados na [referência de API oficial do Mercado Pago](https://www.mercadopago.com.br/developers/pt/reference).
> Classe de exemplo: ***Payment.java***.

### Testes
Devem ser criados testes unitários e de integração de todas as features adicionadas.
Os testes devem ser criados dentro de **test/java/com/mercadopago/client**.
Os testes de integração deverão ter o sufixo `IT` e os unitários deverão ter o sufixo `Test`.
Para os testes de integração deve-se *mockar* as respostas das APIs. Essas respostas devem ser geradas fazendo uma chamada à API desejada com sua chave de testes.
Na [referência de API oficial do Mercado Pago](https://www.mercadopago.com.br/developers/pt/reference) terá o exemplo de requisição.
> Classe de exemplos de testes: ***PaymentClientIT.java*** e ***PaymentClientTest.java***.
