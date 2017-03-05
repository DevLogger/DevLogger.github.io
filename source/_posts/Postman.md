---
title: Testando APIs REST com Postman
date: 2016-11-20 14:22:30
tags: 
    - Express
    - NodeJS
    - REST
header-img: img/postman/postman-hero.jpg
subtitle: Oh yes, wait a minute mister postman!
author: Humberto Machado
comments: true
permalink: testando-apis-rest-postman
---

Antes de qualquer coisa coloque esta música pra tocar [The Beatles - Mr Postman](https://www.youtube.com/watch?time_continue=15&v=58VIY1gBmns). Caso prefira pode  escutar pelo [Spotify](https://open.spotify.com/track/5IIBY9M2GxHcVja6DA6wsF)

Agora sim, podemos testar nossa API com o este fantástico chrome app: [Postman](https://www.getpostman.com/)

# Instalação

Como já disse ali em cima, o [Postman](https://www.getpostman.com/) é um Chrome App, então, caso esteja usando Windows ou Linux você precisara ter o [Chrome instalado](https://www.google.com/chrome/). Caso esteja usando Mac poderá usar o app feito com o [Electron](http://electron.atom.io/) disponibilizado no site do [Postman](https://www.getpostman.com/). Então:

1. Baixe o Postman aqui: https://www.getpostman.com/
2. Divirta-se

# Levantando API para teste

Vamos usar uma API de exemplo já pronta criada em cima do projeto [ProtonType](https://github.com/linck/protontype). Falei um pouco sobre ele aqui [neste post](http://devlog.com.br/2016/11/15/ProtonType/). 

Você precisará do [NodeJS 6.x](https://nodejs.org/en/) ou maior para usar esta API de exemplo. Claro que poderá usar qualquer API que você tenha controle para testar. Caso queira usar esta sugerida siga os passos abaixo:

**Clone o projeto**
```bash
git clone https://github.com/linck/protontype-example.git
```

**Levante a api**
```bash
cd protontype-example
npm install
npm start
```

Esta API nos possibilita criar, alterar, deletar e consultar Tasks e Users.
Para ver os endpoints disponíveis acesse no seu browser:
```bash
https://localhost:3000
```
# Usando o Mr. Postman!
Nossa API está escutando na porta 3000 e usa https, portanto a base da nossa URL será **https://locahost:3000**

Ao abrir o Postman iremos nos deparar com a tela a baixo:
![Initial](inicial.png)

## Criando um Usuário

Na tela inicial:
- Escolha a opçao ***POST*** 
- Coloque a url: ***https://localhost:3000/users***
- Vá para a aba ***body*** escolha a opção ***raw*** e ***JSON***

No campo de texto a baixo adicione o JSON abaixo:
```json
{
    "name": "DevLog",
    "password": "123456",
    "email": "devlog@devlog.com.br"
}
```
Sua configuração ficará como na figura abaixo:
![Post User](post_user.png)

Depois clique em ***Send*** para cadastrar um usuário.

## Testando Autenticação do Usuário

Agora vamos testar a autenticação deste usuário cadastrado. Nossa API implementa um tipo de autenticação chamada [JWT](https://jwt.io/). Vejamos como fazer isso no Postman.

### Gerando o Token
Primeiro devemos solicitar a um token através da url ***https://localhost:3000/token***.

Coloque esta url no Postman assim como foi feito com o usuário, através do método POST, e enviando o JSON:

```json
{
    "password": "123456",
    "email": "devlog@devlog.com.br"
}
```

Sua configuração ficará assim:
![Token](token.png)

Clique em ***send*** e receberá a resposta com um token:
![Token](token_result.png)

Pronto, agora você está autenticado. Copie este token e guarde para o próximo passo.

## Criando uma Task

Agora vamos criar um task. Usando o método POST envie uma solicitação para url ***https://localhost:3000/tasks*** com o JSON abaixo:

```json
{
	"title": "Task Teste";
}
```

Após clicar em ***Send***, receberemos o resultado:
![Token](add_task_unauth.png)

Isso aconteceu porque não informamos na requisição http o ***token*** de autenticação gerado no passo anterior. Então vamos configurar.
- Vá na aba ***Headers***
- No campo ***key*** digite ***Authorization***.
- No campo value coloque ***JWT [token_gerado]*** (por exemplo: ***JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MX0.otx8FgAk8oHHmqY9-dOKmnF3kXOpm2Fxs5Krl985JKI***)

![Token](add_task_token.png)

Com esta configuração, estamos enviado o ***token*** que geramos no cabeçalho Authorization do http, possibilitando nossa API autenticar sua requisição. 

Agora sim, clique em ***Send*** e teremos uma Task criada!

Com o Postman você terá uma ótima ferramente para testes de sua API. Agora você pode desbravar as suas outras funcionalidades de acordo com sua necessidade. Teste os outros endpoints da API. Faça bom uso!
