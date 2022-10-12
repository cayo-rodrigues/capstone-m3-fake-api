# capstone-m3-fake-api

Esse projeto é uma API Fake, criada usando as bibliotecas `json-server` e `json-server-auth`. Seu objetivo é suprir nossa carência por um servidor backend de maneira rápida e fácil, já que **o foco do projeto que irá consumi-la é front-end**.

Segue o link para o repositório da parte front do projeto, desenvolvida em `React`:

https://github.com/cayo-rodrigues/proworking

Essa API é usada para guardar informações sobre usuários e prestadores de serviços que se registram em nosso site.

## **Importante**

- Se estiver usando o `Insomnia`, você pode importar [este arquivo JSON](https://drive.google.com/file/d/1OfsE-MCKlQgW32CNaB1urVKFiu-OSTVk/view?usp=sharing) que já vem com várias requisições úteis! Pode facilitar sua vida.

- Em todas as requisições **`GET`**, é possível passar `query parameters` para otimizar a busca. Para saber como usar esses parâmetros na `URL` de forma correta, consulte a [documentação do json-server](https://github.com/typicode/json-server#table-of-contents). Fazer isso vai melhorar muito sua exeriência. Esta documentação não cobre todas as possibilidades de consulta na API.

- Na documentação do `json-server`, você encontrará features úteis, como **paginação**, **filtros**, **ordenação**, **relacionamento de dados** e **busca por texto**.


------------------------


## **Como enviar um token de autorização**

As rotas privadas exigem um `token de autorização`. Esse `token` é fornecido ao se cadastrar e ao fazer login.

No headers da sua requisição, envie o `token` no seguinte formato:

```javascript
headers: {
  Authorization: `Bearer ${token}`
}
```

Se estiver usando o `Insomnia`, lembre-se de que as aspas não fazem parte do `token`, e não se esqueça de colocar a palavra `Bearer` + um espaço em branco antes de colar o `token`. Também é possível apresentar o `token` selecionando a opção **`Bearer Token`** através da aba **`Auth`**.


------------------------


## URL Base

### https://proworking-api.onrender.com/

------------------------

## **Public Endpoints (Não precisa de token de autorização)**


### **`GET /users`**

Retorna todos os usuários cadastrados. Não requer um corpo de requisição.

### ***Response***

### **200 OK**
```json
[
	{
		"email": "kenzinho@mail.com",
		"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
		"name": "Kenzinho",
		"id": 1,
		"is_active": true,
		"is_admin": false
	},
	{
		"email": "cavalo@cavalo.com.com.com.com",
		"password": "$2a$10$HZT36TpM/cyQ5.OROcjUe.0flTLoulBHUb0gKwBAaH1VzgDNgxTF6",
		"name": "Cavalo",
		"is_active": true,
		"is_admin": false,
		"id": 2
	},
	{
		"email": "user@user.user",
		"password": "$2a$10$BE992NyAfUkwQ28bx4l.P.SddNX.1BG8DlAwyeMno2qcSo1sBU.hK",
		"name": "User",
		"is_active": true,
		"is_admin": false,
		"id": 3
	}
]

```

### **`GET /users/:id`**

Retorna um único usuário de acordo com o id. Não requer um corpo de requisição.

### ***Response***

### **200 OK**
```json
{
	"email": "kenzinho@mail.com",
	"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
	"name": "Kenzinho",
	"id": 1,
	"is_active": true,
	"is_admin": false
}
```

### **`GET /workers`**

Retorna todos os prestadores de serviço cadastrados. Não requer um corpo de requisição.


### ***Response***

### **200 OK**
```json
[
	{
		"userId": 1,
		"occupation_areas": [
			"soldador"
		],
		"cities": [
			{
				"state": "MG",
				"city": "Piranguinho"
			}
		],
		"summary": "soldo coisas, mas nunca fui soldado",
		"whatsapp": "(31) 99944-5697",
		"is_active": true,
		"id": 1
	},
	{
		"userId": 2,
		"occupation_areas": [
			"odontologia"
		],
		"cities": [
			{
				"state": "MG",
				"city": "Piranguinho"
			}
		],
		"summary": "bucéfalo de oferendas não perquires formação odôntica",
		"whatsapp": "(99) 12345-6789",
		"is_active": true,
		"id": 2
	}
]
```

### **`GET /workers/:id`**

Retorna um único prestador de serviço de acordo com o id. Não requer um corpo de requisição.

### ***Response***

### **200 OK**
```json
{
	"userId": 1,
	"occupation_areas": [
		"soldador"
	],
	"cities": [
		{
			"state": "MG",
			"city": "Piranguinho"
		}
	],
	"summary": "soldo coisas, mas nunca fui soldado",
	"whatsapp": "(31) 99944-5697",
	"is_active": true,
	"id": 1
}
```

### **`GET /workers?_expand=user`**

Retorna um array com todos os prestadore de serviço, incluindo suas informações de usuário. Afinal, todo prestador de serviço também é um usuário.

### ***Response***

### **200 OK**

```json
[
	{
		"userId": 1,
		"occupation_areas": [
			"soldador"
		],
		"cities": [
			{
				"state": "MG",
				"city": "Piranguinho"
			}
		],
		"summary": "soldo coisas, mas nunca fui soldado",
		"whatsapp": "(31) 99944-5697",
		"is_active": true,
		"id": 1,
		"user": {
			"email": "kenzinho@mail.com",
			"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
			"name": "Kenzinho",
			"id": 1,
			"is_active": true,
			"is_admin": false
		}
	},
	{
		"userId": 2,
		"occupation_areas": [
			"odontologia"
		],
		"cities": [
			{
				"state": "MG",
				"city": "Piranguinho"
			}
		],
		"summary": "bucéfalo de oferendas não perquires formação odôntica",
		"whatsapp": "(99) 12345-6789",
		"is_active": true,
		"id": 2,
		"user": {
			"email": "cavalo@cavalo.com.com.com.com.com",
			"password": "$2a$10$HZT36TpM/cyQ5.OROcjUe.0flTLoulBHUb0gKwBAaH1VzgDNgxTF6",
			"name": "Cavalo",
			"is_active": true,
			"is_admin": false,
			"id": 2
		}
	}
]
```

### **`POST /register`**

Cadastra um novo **usuário**. Requer um corpo de requisição em formato `JSON`. Também retorna um *`token`* de autenticação no formato `JWT`. Note que o campo `password` deve estar sempre em formato de `string`.

### ***Request***

```json
{
	"email": "user@user.user",
	"password": "147258",
	"name": "User",
	"is_active": true,
	"is_admin": false
}
```

### ***Response***

### **201 Created**

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InVzZXJAdXNlci51c2VyIiwiaWF0IjoxNjQ3MzU3ODI2LCJleHAiOjE2NDczNjE0MjYsInN1YiI6IjMifQ.xKwvlaqNJvfP-ZU7SP9hQHYBDze5dx0yX_3ldmlUQ7c",
	"user": {
		"email": "user@user.user",
		"name": "User",
		"is_active": true,
		"is_admin": false,
		"id": 3
	}
}
```

### **`POST /login`**

Loga um **usuário** na aplicação. Requer um corpo de requisição em formato `JSON`. Assim como a rota `/register`, retorna um *`token`* de autenticação no formato `JWT` e exige um `password` em formato `string`.

### ***Request***

```json
{
	"email": "cavalo@cavalo.com.com.com.com.com",
	"password": "123321"
}
```

### ***Response***

### **200 OK**

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImNhdmFsb0BjYXZhbG8uY29tLmNvbS5jb20uY29tIiwiaWF0IjoxNjQ3MzU4NjMzLCJleHAiOjE2NDczNjIyMzMsInN1YiI6IjIifQ.9fYf8a6psax19B-8_APVm69cXc4T9daMM05GJXpmA3s",
	"user": {
		"email": "cavalo@cavalo.com.com.com.com.com",
		"name": "Cavalo",
		"is_active": true,
		"is_admin": false,
		"id": 2
	}
}
```


### **`GET /ratings`**

Retorna todos os ratings, com referências para os usuários que os fizeram e também os trabalhadores que os receberam. Não possui corpo de requisição.


### ***Response***

### **200 OK**

```json
[
	{
		"stars": 5,
		"workerId": 1,
		"userId": 2,
		"id": 1
	},
	{
		"stars": 5,
		"workerId": 1,
		"userId": 4,
		"id": 2
	},
	{
		"stars": 4,
		"workerId": 2,
		"userId": 4,
		"id": 3
	}
]
```


### **`GET /ratings?workerId=:id`**

Essa requisição pode ser usada para retornar um array com todos os ratings relacionados a um prestador de serviço. Ela pode ser útil para calcular quantos ratings ele tem ao todo e então fazer uma média.

### **`GET /ratings?workerId=:id&userId=:id`**

Essa requisição pode ser usada para verificar se um usuário já fez algum rating a respeito de determinado trabalhador. Pode ser útil caso ele queira alterar a nota que deu para um prestador de serviço.

As duas requisições acima retornam um array, no mesmo formato já demonstrado.


### **`GET /feedbacks`**

Retorna um array de objetos, com todos os feedbacks. Não exige corpo de requisição.

### ***Response***

### **200 OK**

```json
[
	{
		"id": 1,
		"userId": 2,
		"workerId": 3,
		"content": "deu choque no meu sistema"
	},
	{
		"userId": 1,
		"workerId": 3,
		"content": "Deu choque no meu sistema também",
		"id": 2
	}
]
```

### **`GET /feedbacks?_expand=user`**

Essa requisição adiciona uma chave `user` na resposta, tornando fácil saber as informações de quem *fez* o feedback.

### **`GET /feedbacks?_expand=user&_expand=worker`**

Essa requisição faz o mesmo da mencionada acima, com o adicional de colocar uma chave `worker` na resposta, tornando mais fácil saber as informações de quem *recebeu* o feedback.


-----------------------------------

## **Private Endpoints (Requer token de autorização)**

### **`POST /workers`**

Cadastra um novo prestador de serviço. É necessário autenticação pois esse endpoint possui um campo obrigatório `userId` que referencia o usuário que está se tornando um trabalhador. O corpo da requisição deve estar em formato `JSON`.

### ***Request***

```json
{
	"userId": 2,
	"occupation_areas": ["odontologia"],
	"summary": "bucéfalo de oferendas não perquires formação odôntica",
	"whatsapp": "(99) 12345-6789",
	"cities": [{"state": "MG", "city": "Piranguinho"}],
	"is_active": true
}
```

### ***Response***

### **201 Created**

```json
{
	"userId": 2,
	"occupation_areas": ["odontologia"],
	"summary": "bucéfalo de oferendas não perquires formação odôntica",
	"whatsapp": "(99) 12345-6789",
	"cities": [{"state": "MG", "city": "Piranguinho"}],
	"is_active": true,
	"id": 2
}
```

### **`PATCH /workers/:id`**

Atualiza um ou mais campos de um prestador de serviço. O corpo da requisição deve estar no formato `JSON`, e obrigatóriamente deve conter o campo `userId`.

### ***Request***

```json
{
	"userId": 1,
	"whatsapp": "(31)99944-5697"
}
```


### ***Response***

### **200 OK**

```json
{
	"userId": 1,
	"occupation_areas": [
		"soldador"
	],
	"cities": [
		{
			"state": "MG",
			"city": "Piranguinho"
		}
	],
	"summary": "soldo coisas, mas nunca fui soldado",
	"whatsapp": "(31)99944-5697",
	"is_active": true,
	"id": 1
}
```

### **`PATCH /users/:id`**

Atualiza um ou mais campos de um usuário. O corpo da requisição deve estar no formato `JSON`.

### ***Request***

```json
{
	"email": "cavalo@cavalo.com.com.com.com.com"
}
```

### ***Response***

### **200 OK**

```json
{
	"email": "cavalo@cavalo.com.com.com.com.com",
	"password": "$2a$10$HZT36TpM/cyQ5.OROcjUe.0flTLoulBHUb0gKwBAaH1VzgDNgxTF6",
	"name": "Cavalo",
	"is_active": true,
	"is_admin": false,
	"id": 2
}
```

### **`POST /ratings`**

Faz um novo rating. Exige um corpo de resposta em formato `JSON` passando um `workerId` (para quem aquela nota está sendo dada), um `userId` (quem está dando a nota) e `stars` (no máximo 5).

### ***Request***

```json
{
	"stars": 5,
	"workerId": 2,
	"userId": 4
}
```

### ***Response***

### **201 Created**

```json
{
	"stars": 5,
	"workerId": 2,
	"userId": 4,
	"id": 3
}
```


### **`PATCH /ratings/:id`**

Atualiza um rating. Esta rota é útil quando um usuário já deu uma nota (fez o `POST`) mas agora quer alterá-la. Usar essa rota **evita a duplicidade**, então é muito importante que nunca sejam feitas duas requisições `POST` para o mesmo trabalhador. Uma dica para poder usar esta rota, seria fazer uma requisição `GET` passando ambos `workerId` e `userId` como `query params`, e então usar o `id` retornado para poder fazer uso da requisição `PATCH` em questão.

### ***Request***

```json
{
	"stars": 4
}
```

### ***Response***

### **200 OK**

```json
{
	"stars": 4,
	"workerId": 2,
	"userId": 4,
	"id": 3
}
```

### **`POST /feedbacks`**

Cria um novo feedback, guardando referências sobre quem *deu* o feedback (`userId`) e sobre quem *recebeu* o feedback (`workerId`). Corpo da quisição deve estar em formato `JSON`, obrigatóriamente passando um `workerId` e um `userId`.

### ***Request***

```json
{
	"userId": 1,
	"workerId": 3,
	"content": "Deu choque no meu sistema"
}
```

### ***Response***

### **201 Created**

```json
{
	"userId": 1,
	"workerId": 3,
	"content": "Deu choque no meu sistema",
	"id": 2
}
```

### **`PATCH /feedbacks/:id`**

Atualiza um feedback. O corpo da requisição também deve estar em formato `JSON`, e obrigatóriamente passar um `userId`. Também é obrigatório passar o **id do feedback** na url (ex: `feedbacks/2`).

### ***Request***

```json
{
	"userId": 1,
	"content": "Deu choque no meu sistema também"
}
```

### ***Response***

### **200 OK**

```json
{
	"userId": 1,
	"workerId": 3,
	"content": "Deu choque no meu sistema também",
	"id": 2
}
```
