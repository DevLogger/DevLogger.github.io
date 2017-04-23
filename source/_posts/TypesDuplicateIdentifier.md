---
title: TypeScript - Resolvendo o Duplicate Identifier Error
date: 2016-11-16 21:59:42
tags: 
    - TypeScript
header-img: img/duplicate-identifier.png
subtitle: Se livre de uma vez por todas do Duplicate Identifier Error
author: Humberto Machado
comments: true
permalink: typescript-duplicate-identifier
---

# TypeScript - Resolvendo o Duplicate Identifier Error

Um dos problemas mais chatos que você pode encontrar quando for usar TypeScript é:

```bash
Duplicate identifier...
```

Isto acontece quando o compilador tenta carregar o mesmo módulo ou definição (.d.ts) mais de uma vez, identificando que este está duplicado. Quando se instala uma dependência via ***npm install***, o ***npm*** já identifica se o módulo está baixado evitando duplicação, mas, se você esta usando módulos locais com ***npm link***, é quase certo que terá este problema.


Este erro não impede que o JavaScript seja gerado, mas aqui pra nós, é muito chato ver milhares de erro no seu console quando mandamos executar ou compilar algo.

## Resolução

#### Atualize a versao do TypeScript 
```bash
npm install typescript -g
```

#### Configuração do compilador
Coloque esta configuração do seu **tsconfig.json**:

```json
"compilerOptions" {
     ....
    "baseUrl": "./",
    "paths": {
        "*": [ "node_modules/@types/*", "*"]
    }
   ...
}
```

Isto informará ao compilador que quando ele for resolver um módulo qualquer, procure primeiro em  ```.\node_modules\@types\``` e so depois nos demais locais, evitando a duplicidade do carregamento.

## Referências
- https://www.typescriptlang.org/docs/handbook/module-resolution.html
- https://github.com/Microsoft/TypeScript/issues/11916#event-853609143   

*Obrigado [@mhegazy](https://github.com/mhegazy) pela dica!!*