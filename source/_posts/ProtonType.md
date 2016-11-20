---
title: Crie sua API REST com ProtonType
date: 2016-11-15 14:22:30
tags: 
    - JavaScript
    - TypeScript
    - Express
    - Sequelize
    - NodeJS
    - REST
header-img: img/proton-1.jpg
subtitle: Express + Sequelize + TypeScript = ProtonType
author: Humberto Machado
comments: true
---

ProtonType
==========

Um simples web framework feito em TypeScript.

O ProtonType tem como objetivo tornar simples e agradável o desensolvimento de APIs REST e criação de modelos de banco de dados. Utilizando [Express](http://expressjs.com/ "") e [Sequelize ORM](http://docs.sequelizejs.com/ "") ajuda na criação de aplicações web robustas.

Configuração do projeto TypeScript
====================================

As seguintes configurações no **tsconfig.json** são necessárias para o
funcionamento.

```json

    {
      "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "emitDecoratorMetadata": true,
        "experimentalDecorators": true
      }
    }
    
```

Instalação
==========
```bash

npm install protontype --save

```

**Obs: será necessário ter instalado o NodeJS 6 ou maior**

Quick Start - Criando uma API Completa em 5 passos
===========

Estrutura de pastas e configurações iniciais
--------

```bash

    mkdir proton-quickstart
    cd proton-quickstart
    npm init
    mkdir src
    npm install protontype --save
    
```

Criar o arquivo tsconfig.json na raiz do projeto

```json

    {
      "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "emitDecoratorMetadata": true,
        "experimentalDecorators": true,
        "outDir": "dist"
      },
      "exclude": [
        "node_modules",
        "dist"
      ]
    }
    
```
 
Model
-------

Criar um arquivo ParticlesModel.ts

```javascript

    import { BaseModel, SequelizeBaseModelAttr, Model, DataTypes } from 'protontype';
    
    @Model({
        name: "Particles",
        definition: {
            name: {
                type: DataTypes.STRING
            },
            symbol: {
                type: DataTypes.STRING
            },
            mass: {
                type: DataTypes.BIGINT
            }
    
        }
    })
    export class ParticlesModel extends BaseModel<Particle> {
    
    }
    
    export interface Particle extends SequelizeBaseModelAttr {
        name: string;
        symbol: string;
        mass: number;
    }
    
```

Router
-------

Criar arquivo ParticlesRouter.ts

```javascript

    import { ParticlesModel } from './ParticlesModel';
    import { BaseCrudRouter, RouterClass } from 'protontype';
    
    @RouterClass({
        baseUrl: '/particles',
        modelInstances: [new ParticlesModel()]
    })
    export class ParticlesRouter extends BaseCrudRouter {
    
    }
    
```

 

Main
-------

Criar arquivo Main.ts

```javascript

    import { ParticlesRouter } from './ParticlesRouter';
    import { ExpressApplication } from 'protontype';
    
    new ExpressApplication()
        .addRouter(new ParticlesRouter())
        .bootstrap();
        
```
 

**Compilando e Rodando Aplicação**
```bash

    tsc
    node dist/Main.ts
    
```
 
Testando a API
-------

Por padrão, a aplicação usará um banco de dados sqlite. 
Será criado um arquivo proton.sqlite na raiz do projeto.

Os endpoints abaixo já estarão disponíveis:
-   **GET /particles** - Lista todos os registos da tabela Particles
-   **POST /particles** - Cria um registro na tabela Particles
-   **GET /particles/:id** - Consulta um registro da tabela Particles
-   **PUT /particles/:id** - Atualiza um registro da tabela Particles
-   **DELETE /particles/:id** - Remove um registro da tabela Particles

Poderá testar através do app [Postman](https://www.getpostman.com/ "") ou outro da sua preferência.

**Código completo do quick start**

https://github.com/linck/proton-quickstart

**Exemplo de uso completo**

https://github.com/linck/protontype-example

**Projeto e guia completo**
https://github.com/linck/protontype
