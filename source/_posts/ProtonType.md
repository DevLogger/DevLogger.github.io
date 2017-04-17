---
title: Crie sua API REST usando Typescript com ProtonType
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
permalink: crie-api-rest-protontype
---

Protontype é um módulo Node que ajuda na criação de APIs RESTfull. Tem como objetivo facilitar a criação de objetos de banco de dados, rotas, middlewares e autenticação, tudo isso usando Typescript

# Quick Start - Criando uma API em 5 passos

## Estrutura de pastas e configurações iniciais

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
        "target": "es5",
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
 
## Model

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

## Router

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

 

## Main

Criar arquivo Main.ts

```javascript

    import { ParticlesRouter } from './ParticlesRouter';
    import { ProtonApplication } from 'protontype';
    
    new ProtonApplication()
        .addRouter(new ParticlesRouter())
        .bootstrap();
        
```
 

**Compilando e Rodando Aplicação**
```bash

    tsc
    node dist/Main.ts
    
```
 
## Testando a API

Por padrão, a aplicação usará um banco de dados sqlite. 
Será criado um arquivo proton.sqlite na raiz do projeto.

Os endpoints abaixo já estarão disponíveis:

-   **GET /particles** - Lista todos os registos da tabela Particles
-   **POST /particles** - Cria um registro na tabela Particles
-   **GET /particles/:id** - Consulta um registro da tabela Particles
-   **PUT /particles/:id** - Atualiza um registro da tabela Particles
-   **DELETE /particles/:id** - Remove um registro da tabela Particles

Podera testar através do app [Postman](https://www.getpostman.com/ "") ou outro da sua preferência.

**Código completo do quick start**

<https://github.com/linck/proton-quickstart>

## Exemplo

<https://github.com/linck/protontype-example>

## Projeto

<https://github.com/linck/protontype>

## Documentação 

<https://linck.github.io/protontype-docs>
