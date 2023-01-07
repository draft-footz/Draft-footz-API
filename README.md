<h1 align="center">
  Draft Footz - API
</h1>

<p align = "center">
Este é o backend da aplicação Draft Footz - Uma aplicação para organizar e gerenciar torneios e times de futebol! O objetivo dessa aplicação é conseguir criar um frontend de qualidade em grupo, utilizando o que foi ensinado no terceiro módulo (M3), bem como o desenvolvimento de hard e soft skills.
</p>

## **Endpoints**

A API tem um total de 6 endpoints.

Pode-se usar a url abaixo para utilizar a API ou se quiser, pode fazer o clone do repositório e rodá-la localmente.

ATENÇÃO: Lembrar que a url precisa ser alterada em seu projeto se alternar entre os modos acima.

https://draft-footz.onrender.com/

## ROTAS QUE NÃO PRECISAM DE AUTENTICAÇÃO

<h2 align ='center'> Criar usuário </h2>

`POST /register - FORMATO DA REQUISIÇÃO`

Para requisição de cadastro, envie uma requisição /POST para a rota url/users.

Envie no corpo da requisição:

```json
{
  "email": "email do usuário",
  "password": "senha do usuário",
  "name": "nome do usuário",
  "username": "apelido do usuário",
  "contact": "contato do usuário"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 201`

```json
{
  "email": "admim@mail.com",
  "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
  "name": "Admin",
  "number": 988584074,
  "id": 1,
  "myTeam": null
}
```

<h2 align ='center'> Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`

Para requisição de login, envie uma requisição de /POST para a rota url/login.

Envie no corpo da requisição:

```json
{
  "email": "email do usuário",
  "password": "senha do usuário"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImF1Z3VzdG9AdGVzdC5jb20iLCJpYXQiOjE2NzMwNDEyNjEsImV4cCI6MTY3MzA0NDg2MSwic3ViIjoiMyJ9.i-g61mmYZQA_qDA9Mp67lk5m78YP5AAviNvgUoNJ6Mo",
  "user": {
    "email": "user@test.com",
    "name": "Test User",
    "contact": "127.0.0.1",
    "myTeam": null,
    "id": 3
  }
}
```

<h2 align ='center'> Listar todos os times </h2>

`GET /teams - FORMATO DA RESPOSTA - STATUS 200`

Para obter todos os times, envie uma requisição /GET para a rota url/teams.

Caso bem sucedido o retorno da requisição será um array com todos os times.

<h2 align ='center'> Listar time </h2>

`GET /teams/:id`

Para ler as informações do time do usuário, envie uma requisição /GET para a rota url/teams/:id, onde o ":id" é o id do time do usuário, encontrado no campo myTeam da resposta da requisição de Login.

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "userId": 2,
  "name": "Kenzie FC",
  "logo": "https://imgs.search.brave.com/B9RMHDqmhcs6PqdPKbzkPdzqdx1eZzjjBwq4cuX01SU/rs:fit:474:225:1/g:ce/aHR0cHM6Ly90c2Ux/Lm1tLmJpbmcubmV0/L3RoP2lkPU9JUC5O/QnNGVk1pdzR6Nk9x/Y3VJQm14UWJRSGFI/YSZwaWQ9QXBp",
  "id": 2
}
```

ATENÇÃO: o usuário só terá acesso ao time que ele é dono.

<h2 align ='center'> Listar jogadores do time </h2>

`GET /players?&teamId=:id`

Para obter os jogadores do time, envie uma requisição /GET para a rota url/players?&teamId=:id, onde o ":id" é o id do time.

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "userId": 2,
  "teamId": 2,
  "name": "Luisito Suarez",
  "age": 35,
  "avatar": "url",
  "contact": "519999999",
  "position": null,
  "id": 2
}
```

<h2 align ='center'> Listar todos os torneios </h2>

`GET /tournaments - FORMATO DA RESPOSTA - STATUS 200`

PPara obter todos os torneios, envie uma requisição /GET para a rota url/tournaments.

Caso bem sucedido o retorno da requisição será um array com todos os torneios.

<h2 align ='center'> Listar torneio </h2>

`GET /tournaments?&userId=:id`

Para obter os torneios de um usuário, envie uma requisição /GET para a rota url/tournaments?&userId=:id, onde o ":id" é o id do usuário.

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "userId": 1,
  "name": "Copa Kenzie",
  "type": "Qualifiers",
  "numberOfTeams": 8,
  "inProgress": true,
  "champion": null,
  "id": 1
}
```

ATENÇÃO: o usuário só terá acesso ao torneio que ele é dono.

<h2 align ='center'> Listar partidas de um torneio </h2>

`GET /matches?&tournament=:id - FORMATO DA RESPOSTA - STATUS 200`

Para obter as partidas de um torneio, envie uma requisição /GET para a rota url/matches?&tournament=:id, onde o ":id" é o id do torneio.

Caso bem sucedido o retorno da requisição será um array com todas as partidas do torneio.

<h2 align ='center'> Listar partida </h2>

`GET /matches/:id`

Para ler uma partida especifica, envie uma requisição /GET para a rota url/matches/:id, onde o ":id" é o id da partida.

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "tournament": 1,
  "id": 1,
  "order": 1,
  "teamA": null,
  "teamB": null,
  "winner": null,
  "score": {
    "regular": {
      "teamA": null,
      "teamB": null
    },
    "penalties": {
      "teamA": null,
      "teamB": null
    }
  }
}
```

<h2 align ='center'> Listar pedidos de inscrição em torneios </h2>

`GET /subscriptions??&tournamentId=:id`

Para ler os pedidos de inscrição para um torneio, envie uma requisição /GET para a rota url/subscriptions??&tournamentId=:id, onde o ":id" é o id do torneio.

Caso bem sucedido o retorno da requisição será um array com todas os pedidos de inscrição no torneio no seguinte formato:

`STATUS 200`

```json
{
  "id": 1,
  "tournament": 1,
  "teamId": 1,
  "accepted": false
}
```

## ROTAS QUE PRECISAM DE AUTENTICAÇÃO

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Atualizar o time nos dados do usuário </h2>

`PATCH /users/:id`

Para definir qual é o ID do time do usuário, envie uma requisição de /PATCH para a rota url/users/idDoUsuário.

Envie no corpo da requisição:

```json
{
  "teamId": 1
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "email": "user@test.com",
  "password": "$2a$10$hNWFIn/NDxV8KTm62CkE/uQ3FHiNVy.kvYFybgQKW07Gp1VxhxRJq",
  "name": "Test User",
  "contact": "127.0.0.1",
  "myTeam": 1,
  "id": 3
}
```

<h2 align ='center'> Buscar dados do usuário </h2>

`GET /users/:id`

Para buscar os dados do usuário, envie uma requisição de /GET para a rota url/users/:id

Envie no corpo da requisição:

```json
{
  "userId": 1
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "email": "user@test.com",
  "password": "$2a$10$hNWFIn/NDxV8KTm62CkE/uQ3FHiNVy.kvYFybgQKW07Gp1VxhxRJq",
  "name": "Test User",
  "contact": "127.0.0.1",
  "myTeam": 1,
  "id": 2
}
```

<h2 align ='center'> Criar novo time </h2>

`POST /teams`

Para criar um novo time, envie uma requisição /POST na rota url/teams.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário",
  "name": "nome do time",
  "logo": "url do símbolo do time"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 201`

```json
{
  "userId": 1,
  "name": "FC KENZIE",
  "logo": "https://imgs.search.brave.com/B9RMHDqmhcs6PqdPKbzkPdzqdx1eZzjjBwq4cuX01SU/rs:fit:474:225:1/g:ce/aHR0cHM6Ly90c2Ux/Lm1tLmJpbmcubmV0/L3RoP2lkPU9JUC5O/QnNGVk1pdzR6Nk9x/Y3VJQm14UWJRSGFI/YSZwaWQ9QXBp",
  "id": 2
}
```

<h2 align ='center'> Atualizar time </h2>

`POST /teams/:id`

Para atualizar os dados de um time, envie uma requisição /PATCH para a rota url/teams/:id onde o "id" é o id do time.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário"
  // E outros campos que serão alterados
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "userId": 1,
  "name": "Kenzie Brasil FC",
  "logo": "https://imgs.search.brave.com/B9RMHDqmhcs6PqdPKbzkPdzqdx1eZzjjBwq4cuX01SU/rs:fit:474:225:1/g:ce/aHR0cHM6Ly90c2Ux/Lm1tLmJpbmcubmV0/L3RoP2lkPU9JUC5O/QnNGVk1pdzR6Nk9x/Y3VJQm14UWJRSGFI/YSZwaWQ9QXBp",
  "id": 1
}
```

<h2 align ='center'> Excluir time </h2>

`DELETE /teams/:id`

Para deletar o time, envie uma requisição /DELETE para a rota url/teams/:id onde o "id" é o id do time.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{}
```

ATENÇÃO: Logo em seguida, envie uma requisição `Update User's Team`, com o corpo:

```json
{
  "myTeam": null
}
```

<h2 align ='center'> Criar novo jogador </h2>

`POST /players`

Para inserir um jogador em um time, envie uma requisição /POST para a rota url/players.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário",
  "teamId": "id do time",
  "name": "nome do jogador",
  "position": null,
  "number": "número da camisa do jogador"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 201`

```json
{
  "userId": 1,
  "teamId": 1,
  "name": "Ronaldo",
  "position": null,
  "number": 10,
  "id": 2
}
```

<h2 align ='center'> Atualizar dados do jogador </h2>

`POST /players/:id`

Para atualizar os dados de um jogador, envie uma requisição /PATCH para a rota url/players/:id onde o "id" é o id do jogador.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário"
  // E outros campos que serão alterados
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "userId": 1,
  "teamId": 1,
  "name": "Rivaldo",
  "position": "Atacante",
  "number": 10,
  "id": 2
}
```

<h2 align ='center'> Excluir jogador </h2>

`POST /players/:id`

Para deletar um jogador em um time, envie uma requisição /DELETE para a rota url/players/:id onde o "id" é o id do jogador.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{}
```

<h2 align ='center'> Criar novo torneio </h2>

`POST /tournaments`

Para criar um torneio, envie uma requisição /POST para a rota url/tournaments.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário que criou o torneio",
  "name": "nome do torneio",
  "type": "tipo do torneio",
  "numberOfTeams": "número de times do torneio",
  "champion": null
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 201`

```json
{
  "userId": 2,
  "name": "Kenzie Copa",
  "type": "Qualifiers",
  "numberOfTeams": 8,
  "champion": null,
  "id": 2
}
```

<h2 align ='center'> Atualizar dados do torneio </h2>

`POST /tournaments/:id`

Para atualizar um torneio, envie uma requisição /PATCH para a rota url/tournaments/idDoTorneio.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário que criou o torneio"
  // E outros campos que serão alterados
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "userId": 2,
  "name": "Kenzie Master Cup",
  "type": "Qualifiers",
  "numberOfTeams": 8,
  "champion": null,
  "id": 2
}
```

<h2 align ='center'> Excluir torneio </h2>

`POST /tournaments/:id`

Para deletar um torneio, envie uma requisição /DELETE para a rota url/tournaments/:id onde o "id" é o id do torneio.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{}
```

<h2 align ='center'> Criar nova partida </h2>

`POST /matches`

Para criar uma partida, envie uma requisição /POST para a rota url/matches.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário",
  "tournament": "id do torneio",
  "order": "ordem da partida",
  "teamA": null,
  "teamB": null,
  "winner": null,
  "score": {
    "regular": {
      "teamA": null,
      "teamB": null
    },
    "penalties": {
      "teamA": null,
      "teamB": null
    }
  }
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 201`

```json
{
  "userId": 2,
  "tournament": 2,
  "order": 1,
  "teamA": null,
  "teamB": null,
  "winner": null,
  "score": {
    "regular": {
      "teamA": null,
      "teamB": null
    },
    "penalties": {
      "teamA": null,
      "teamB": null
    }
  },
  "id": 8
}
```

<h2 align ='center'> Atualizar dados da partida </h2>

`POST /matches/:id`

Para atualizar uma partida, envie uma requisição /PATCH para a rota url/matches/:id onde o "id" é o id da partida.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário"
  // E outros campos que serão alterados
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "userId": 2,
  "tournament": 2,
  "order": 1,
  "teamA": 5,
  "teamB": 2,
  "winner": 1,
  "score": {
    "regular": {
      "teamA": 3,
      "teamB": 3
    },
    "penalties": {
      "teamA": 4,
      "teamB": 3
    }
  },
  "id": 8
}
```

<h2 align ='center'> Excluir partida </h2>

`POST /tournaments/:id`

Para deletar uma partida, envie uma requisição /DELETE para a rota url/matches/:id onde o ":id" é o id da partida.

Envie no corpo da requisição:

```json
{
  "userId": "id do usuário"
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{}
```

<h2 align ='center'> Criar pedido de inscrição no torneio </h2>

`POST /subscriptions`

Para um time pedir para participar de um torneio, é necessário enviar uma requisição /POST para a rota url/subscriptions/.

Envie no corpo da requisição:

```json
{
  "tournamentId": "id do torneio",
  "teamId": "id do time",
  "accepted": false
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 201`

```json
{
  "tournamentId": 1,
  "teamId": 2,
  "accepted": false,
  "id": 3
}
```

<h2 align ='center'> Atualizar dados do pedido de inscrição no torneio </h2>

`POST /subscriptions/:id`

Para aceitar um pedido de inscrição, é necessário enviar uma requisição /PATCH para a rota url/subscriptions/:id onde ":id" é o id do pedido.

Envie no corpo da requisição:

```json
{
  "accepted": true
}
```

Caso dê tudo certo, a resposta será assim:

`STATUS 200`

```json
{
  "tournament": 1,
  "teamId": 2,
  "accepted": true,
  "id": 2
}
```
