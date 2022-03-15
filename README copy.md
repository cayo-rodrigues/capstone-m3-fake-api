# Json-server fake API

Esse repositório usa as bibliotecas json-server + json-server-auth para criar uma fake api simples.
Sua base de dados guarda informações de usuários, "postagens" e "comentários". Não existe verificação da integridade dos dados. As únicas validações são de permissão de acesso nas rotas, além das validações padrão relacionadas a cadastro e login que já vem com o json-server-auth.


## URL base

https://json-server-posts-n-comments.herokuapp.com/

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.


### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

#### Exemplo de requisição

```javascript
{
	"email": "kenzinho@mail.com",
	"password": "123456"
}
```

#### Resposta

200 OK

```javascript
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvQG1haWwuY29tIiwiaWF0IjoxNjQ2ODQ0NTU4LCJleHAiOjE2NDY4NDgxNTgsInN1YiI6IjEifQ.lNVy5n2FWF-ZN9h6zI4BZtZztbZ85MBapM8X9ItTU5c",
	"user": {
		"email": "kenzinho@mail.com",
		"name": "Kenzinho",
		"age": 38,
		"id": 1
	}
}
```

### Visualizar usuários

GET /users

É necessário passar um token de autenticação, seguindo a convenção do JWT, de colocar a palavra Bearer antes do token. Esse token precisa ser enviado no header da requisição. Ex:

```javascript
headers: {
	Authorization: `Bearer ${token}`
}
```

No insomnia, também existe a possibilidade de fazer de outra forma. Você pode clicar em "Auth" e selecionar "Bearer Token" no dropdown. Lembre-se de que as aspas não fazem parte do token.

Para ver todas as postagens de um usuário:

- GET /users/:userId?_embed=posts

Para ver todos os comentários de um usuário:

- GET /users/:userId?_embed=comments

Se quiser combinar as duas requisições acima, e ver um usuário, juntamente com as postagens e comentários que ele fez:

- GET /users/:userId?_embed=comments&_embed=posts


### Visualizar postagens

GET /posts

Não é necessário nenhum tipo de autenticação nesse endpoint, qualquer um pode ver as postagens dos usuários.

Para ver as postagens, juntamente com os usuários que as fizeram:

- GET /posts?_expand=user

Para ver as postagens, juntamente com os comentários relacionados a elas:

- GET /posts?_embed=comments



### Fazer uma nova postagem

POST /posts

É necessário passar um token de autenticação, seguindo a convenção do JWT, de colocar a palavra Bearer antes do token. Esse token precisa ser enviado no header da requisição. Ex:

```javascript
headers: {
	Authorization: `Bearer ${token}`
}
```

No insomnia, também existe a possibilidade de fazer de outra forma. Você pode clicar em "Auth" e selecionar "Bearer Token" no dropdown. Lembre-se de que as aspas não fazem parte do token.

**Importante:**

No corpo da requisição, não esqueça de passar um "userId" (exatamente nesse formato). Assim, será possível relacionar a postagem com o usuário.


#### Exemplo de requisição

```javascript
{
  "imgUrl": "myImgUrl",
	"title": "myPostTitle",
	"description": "MyPostDescription",
	"userId": 1
}
```


#### Resposta

201 Created

`
{
  "imgUrl": "myImgUrl",
	"title": "myPostTitle",
	"description": "MyPostDescription",
	"userId": 1,
  "id": 1
}
`

### Visualizar comentários

GET /comments

Não é necessário nenhum tipo de autenticação nesse endpoint, qualquer um pode ver os comentários dos usuários.

Para ver os comentários, juntamente com os usuários que os fizeram:

- GET /comments?_expand=user

Para ver os comentários, juntamente com as postagens em que eles foram feitos:

- GET /comments?_expand=post

Se quiser combinar as duas requisições acima, e ver os comentários, juntamente com as postagens e usuŕios relacionados:

- GET /comments?_expand=post&_expand=user


### Fazer um comentário

POST /comments

É necessário passar um token de autenticação, seguindo a convenção do JWT, de colocar a palavra Bearer antes do token. Esse token precisa ser enviado no header da requisição. Ex:

```javascript
headers: {
	Authorization: `Bearer ${token}`
}
```

No insomnia, também existe a possibilidade de fazer de outra forma. Você pode clicar em "Auth" e selecionar "Bearer Token" no dropdown. Lembre-se de que as aspas não fazem parte do token.

**Importante:**

No corpo da requisição, não esqueça de passar um "userId" (exatamente nesse formato) e também um "postId" (exatamente nesse formato). Assim, será possível relacionar o comentário com o usuário e também com a postagem em que está sendo feito o comentário.


#### Exemplo de requisição

```javascript
{
  "comment": "myComment",
	"userId": 1,
  "postId": 2
}
```


#### Resposta

201 Created

```javascript
{
	"comment": "myComment",
	"userId": 1,
	"postId": 2,
	"id": 1
}
```