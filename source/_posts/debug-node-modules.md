---
title: VS Code - Debugando módulos instalados em node_modules
date: 2018-04-22 13:41:30
tags: 
    - VScode
    - Editors
    - Tools
    - NodeJS
header-img: img/vscode-debug.png
subtitle: Como incluir suas libs no contexto do debugger
author: Humberto Machado
comments: true
permalink: debug-vscode-node-modules
---

# VSCode: Debugando módulos instalados em node_modules

Para debugar códigos que estão na pasta node_modules, basta informar no **launch.json**, na propriedade **outFiles**, o caminho dos arquivos que o debugger deve colocar no seu escopo.

Pode exemplo, se quizermos que o debugger pare em algum breakpoint no módulo express:

```json
{
    // Use IntelliSense to learn about possible Node.js debug attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "program": "${workspaceRoot}/dist/main.js",
            "sourceMaps": true,
            "outFiles": [
                "${workspaceRoot}/node_modules/express/lib/**/*.js"
            ],
            "console": "integratedTerminal"
        }
    ]
}
```

O trecho abaixo faz com que o debugger do node inclua todos arquivos javascript da pasta lib do módulo express, assim podemos colocar breakpoints neles.

```json
{
    ...
    "outFiles": [
        "${workspaceRoot}/node_modules/express/lib/**/*.js"
    ],
    ...
}
```