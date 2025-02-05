# Desafio Técnico: API de Gerenciamento de Tarefas

![Uvicorn](https://img.shields.io/badge/Uvicorn-ffdd57?style=for-the-badge&logo=uvicorn&logoColor=black)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)



Um gerenciador de tarefas usando FastAPI, OAuth2 com JWT para autenticação e SQLite como banco de dados. 

## Estrutura do Projeto

```
testAPI/
├── auth/
│   ├── __init__.py
│   └── jwt.py
├── database/
│   ├── __init__.py
│   └── database.py
├── models/
│   ├── __init__.py
│   └── task.py
├── routes/
│   ├── __init__.py
│   └── tasks.py
└── main.py
```

- **auth**/: Implementação de autenticação e autorização.

- **database/**: Configuração do banco de dados SQLite e modelos ORM.

- **models/**: Definições de esquemas Pydantic.

- **routes/**: Definição das rotas da API.

- **main.py**: Ponto de entrada para iniciar o servidor FastAPI.

Crie e ative um ambiente virtual:

## Instalação
### Crie e ative um ambiente virtual:
```
python -m venv venv
source venv\Scripts\activate
```
### Instale as dependências:
crie uma pasta com um documento txt, no documento deve conter as dependencias da seguinte maneira:

- Python 3.7+
- FastAPI
- Uvicorn
- SQLAlchemy
- Jinja2
- PyJWT

Logo em seguida crie um novo terminal e digite o seguinte comando:
```
pip install -r requirements.txt 
```

## Configuração do Banco de Dados
### banco de dados SQLite será criado automaticamente ao iniciar o servidor pela primeira vez.

## Uso
### Executando o Servidor
Para iniciar o servidor, execute o seguinte comando:

```
uvicorn main:app --reload
Abra o navegador e acesse http://127.0.0.1:8000/docs para ver a documentação interativa da API.
```

## Testes
### Gere um token de autenticação:

```py
curl -X POST "http://127.0.0.1:8000/token" -H "Content-Type: application/x-www-form-urlencoded" -d "username=admin&password=password123"
````
Use o token gerado para acessar os endpoints protegidos:

```py
curl -X POST "http://127.0.0.1:8000/tasks" -H "Authorization: Bearer seu_token_aqui" -H "Content-Type: application/json" -d "{\"titulo\": \"Nova Tarefa\", \"estado\": \"pendente\"}"
```

## Endpoints da API
### Autenticação

- **POST** /token: Gera um token de autenticação JWT.

   - Requisição:

```json
{
  "username": "admin",
  "password": "password123"
}
```

  - Resposta:

```json
{
  "access_token": "seu_token_aqui",
  "token_type": "bearer"
}
```

## Gerenciamento de Tarefas
- **POST** /tasks/: Cria uma nova tarefa.
   - Requisição:

```json
{
  "titulo": "Nova Tarefa",
  "estado": "pendente"
}
```

   - Resposta:

```json
{
  "id": 1,
  "titulo": "Nova Tarefa",
  "estado": "pendente",
  "data_criacao": "2025-01-15T00:00:00Z",
  "data_atualizacao": "2025-01-15T00:00:00Z"
}
```

**GET** /tasks/: Lista todas as tarefas.

   - Resposta:

```json
[
  {
    "id": 1,
    "titulo": "Nova Tarefa",
    "estado": "pendente",
    "data_criacao": "2025-01-15T00:00:00Z",
    "data_atualizacao": "2025-01-15T00:00:00Z"
  }
]
```

**GET** /tasks/{task_id}: Obtém uma tarefa específica.

   - Resposta:

``` json
{
  "id": 1,
  "titulo": "Nova Tarefa",
  "estado": "pendente",
  "data_criacao": "2025-01-15T00:00:00Z",
  "data_atualizacao": "2025-01-15T00:00:00Z"
}
```

**PUT** /tasks/{task_id}: Atualiza uma tarefa existente.

   - Requisição:

```json
{
  "titulo": "Tarefa Atualizada",
  "estado": "em andamento"
}
```
   - Resposta:

```json
{
  "id": 1,
  "titulo": "Tarefa Atualizada",
  "estado": "em andamento",
  "data_criacao": "2025-01-15T00:00:00Z",
  "data_atualizacao": "2025-01-15T00:00:00Z"
}
``` 

**DELETE** /tasks/{task_id}: Deleta uma tarefa.

   - Resposta:

```json
{
  "message": "Task deleted successfully"
}

```
