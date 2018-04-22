---
title: TypeScript - Declarando propriedades de uma classe direto no construtor
date: 2016-12-02 22:27:51
tags: 
    - TypeScript
header-img: img/mineconstructor.jpg
author: Humberto Machado
comments: true
permalink: typescript-construtor
---

No TypeScript é possivel declarar as propriedades de uma classe direto no construtor. Vamos entender melhor no exemplo.

O que normalmente faríamos assim:

```javascript
class Task {
    public title: string;
    public done: boolean;
    public creationDate: Date;
    public finishDate: Date;

    constructor(title: string, done: boolean, creationDate: Date, finishDate: Date) {
        this.title = title;
        this.done = done;
        this.creationDate = creationDate;
        this.finishDate = finishDate;
    }

}

var task: Task = new Task('My Task', false, new Date(), new Date());
console.log(task.title); //> My Task
```

Podemos fazer assim:
```javascript
class Task {
 constructor(public title: string, public done: boolean, public creationDate: Date, public finishDate: Date) {}

}

var task: Task = new Task('My Task', false, new Date(), new Date());
console.log(task.title); //> My Task
```

Simples! Resumimos o conteudo da classe em uma linha de código.

*Obrigado [Plínio Naves](https://twitter.com/plinionaves) pela dica!*