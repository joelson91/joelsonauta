---
title: "O básico do Cisco IOS"
slug: "o-basico-do-cisco-ios"
date: "2026-01-31T12:21:51-03:00"
tags: ["cisco"]
categories: ["tutorial"]
draft: false
disableShare: false
searchHidden: false
---

Um dos pontos importantes sobre equipamentos de rede gerenciáveis é o **Sistema Operacional**. Em equipamentos Cisco temos o **IOS** (Internetwork Operating System).

O manuseio deste sistema operacional funciona através de uma interface de linha de comando (CLI). Por meio dela, podemos definir um nome para o equipamento, configurar senhas, endereço IP e outras opções.
## Conectando-se ao equipamento
Em swiches e roteadores a conexão inicial se dá através do **cabo console**. Por meio dele, podemos acessar a interface de linha de comando e definir todas as preferências.

## Modos de execução
O Cisco IOS possui 3 modos de execução para garantir um controle mais seguro.

### Modo Usuário (User EXEC Mode)
Apresenta informações básicas sobre o equipamento, mas não é capaz de mudar suas configurações.

Para identificá-lo, o nome do equipamento termina com `>`

```
switch>
```

### Modo Privilegiado (Privileged EXEC Mode)
É possível ver todas as configurações detalhadas, mas ainda não é possível modificá-las.

Para identificá-lo, o nome do equipamento termina com `#`

Comando para entrar: `enable`

```
switch#
```

### Modo de Configuração Global (Global Configuration Mode)
É o modo capaz de modificar as configurações do equipamento, tanto configurações gerais quanto as de interfaces específicas.

Para identificá-lo, o nome do equipamento termina com `(config)#`

Comando para entrar: `configure terminal` (ou apenas `conf t`)

```
switch(config)#
```


## Comandos de navegação
Comandos de navegação auxiliam usuários a preencher comandos e pedir ajuda.

- Digite `?` em qualquer lugar para ver quais comandos estão disponíveis naquele momento.

- Comece a digitar um comando e aperte a tecla `Tab` para autocompletar.

- `show running-config` Mostra tudo o que está configurado e rodando no equipamento agora.

- `exit` Volta um nível para trás.


## Checklist de Segurança Inicial
Ao inicializar um equipamento Cisco pela primeira vez, não há configurações de identificação e segurança definidas. É importante definir essas configurações para facilitar a identificação do equipamento e evitar que pessoas não autorizadas assumam o controle.

### Nomeando o equipamento
Para dar um nome ao equipamento, utilize o comando `hostname [nome_do_equipamento]`.

```
switch(config)# hostname SW_Secretaria
```

É importante que o nome do equipamento siga as seguintes regras:
- Comece com a função do equipamento (`RTR` para roteadores, `SW` para switches).
- Utilize letras maiúsculas para facilitar a legibilidade.
- Use *underscores* (`_`) para separar palavras, evitando espaços.
- Mantenha o nome abaixo de 30 caracteres, se possível.

### Protegendo o Modo Privilegiado
Para criar uma senha para o **Modo Privilegiado**, use o comando `enable secret [minha_senha_segura]`. Esse comando cria uma senha e a criptografa no arquivo de configuração para que outros usuários não possam visualizá-la.

```
switch(config)# hostname SW_Secretaria
```

### Protegendo o acesso via Console
Para definir uma senha de acesso via console, siga os seguintes passos:

```
switch(config)# line console 0
switch(config-line)# password senha_console
switch(config-line)# login
```

### Criando Banner de aviso
O banner de aviso serve para informar aos usuários do equipamento que o acesso é permitido apenas para pessoas autorizadas.

Para definir uma mensagem, utilize o comando `banner motd # [ACESSO RESTRITO! APENAS PARA PESSOAS AUTORIZADAS.] #`

Lembre-se que a mensagem deve estar entre `# #`.

### Criptografando todas as senhas
Por padrão, algumas senhas podem aparecer como texto comum no arquivo de configuração.

Use o comando `service password-encryption` para encriptar todas as senhas.

```
switch(config)# service password-encryption
```

### Salvando as configurações
É importante lembrar que as configurações feitas não ficam salvas automaticamente no arquivo de inicialização. Isso significa que ao reiniciar o equipamento, todas as configurações ficam perdidas caso não estejam salvas no arquivo de configuração.

Para salvar as configurações, use o comando `copy running-config startup-config`

```
switch# copy running-config startup-config
```
