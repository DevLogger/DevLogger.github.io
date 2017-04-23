---
title: Fazendo deploy de aplicativo Ionic no Heroku
date: 2017-03-5 13:16:30
tags: 
    - Heroku
    - NodeJS
    - Ionic Framework
    - Tools
header-img: img/octocat_adventure-cat.png
subtitle: Faça o deploy do seu aplicativo de forma rápida e fácil
author: Humberto Machado
comments: true
permalink: deploy-ionic-heroku
---

O Heroku se torna um meio muito útil e free para disponibilizar um build do app Ionic para testes em um servidor na nuvem.
Pra fazer isso basta seguir os passos abaixo:

# Preparando o projeto
- Criar um repositório no github
- Criar um projeto npm com a dependência do express

```cmd
npm init
npm install express --save
```

- Copiar a pasta www do projeto ionic para o projeto criado
- Criar um servidor em node + express para servir o index.html da pasta www
- Crie um arquivo **server.js** na raiz do projeto:

```javascript
var express = require('express'),
    app = express();

app.use(express.static('www'));

// CORS (Cross-Origin Resource Sharing) headers to support Cross-site HTTP requests
app.all('*', function(req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    next();
});

app.set('port', process.env.PORT || 5000);

app.listen(app.get('port'), function () {
    console.log('Express server listening on port ' + app.get('port'));
});
```
- Commit e push seu projeto no repositório criado

# Fazendo Deploy no Heroku

- Crie uma conta no Heroku
- Acesse https://dashboard.heroku.com/
- Vá na opção new > create new app
- Dê um nome pro projeto e clique em "Create new app"
- Na sessão "Deployment method" escolha GitHub
- Escolha o projeto criado nos passos a cima
- Clique em "Automatic Deploy" para fazer o deploy sempre que fizer um push
- Clique em em "Deploy Branch"
- Clique em View

Pronto! Agora é só aproveitar

# Repositório Exemplo

<https://github.com/DevLogger/heroku-github>

