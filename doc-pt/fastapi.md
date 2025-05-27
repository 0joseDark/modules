**FastAPI**, tanto no **Windows 10** como no **Ubuntu**, incluindo um **exemplo completo** com explicações detalhadas.

---

## ✅ O que é o FastAPI?

O **FastAPI** é um framework web moderno e rápido (alta performance) para a construção de APIs com **Python 3.7+**, baseado em **Starlette** (para a web) e **Pydantic** (para validação de dados). Ele é usado para criar **APIs REST** de forma simples, eficiente e com ótima documentação automática.

---

## 🔧 Instalação do FastAPI e Uvicorn

### ▶️ No **Windows 10** e **Ubuntu** (iguais):

1. **Criar um ambiente virtual (opcional, mas recomendado):**

```bash
python -m venv venv
```

2. **Ativar o ambiente virtual:**

* **Windows:**

```bash
venv\Scripts\activate
```

* **Ubuntu:**

```bash
source venv/bin/activate
```

3. **Instalar o FastAPI e o Uvicorn:**

```bash
pip install fastapi uvicorn
```

---

## 💡 Exemplo completo de API com FastAPI

### Objetivo:

Vamos criar uma API para gerir uma lista de **utilizadores** com as operações:

* Criar utilizador
* Listar utilizadores
* Obter um utilizador por ID
* Apagar um utilizador

---

### 📄 Ficheiro `main.py`

```python
# main.py
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from typing import List

app = FastAPI()

# Modelo de dados
class User(BaseModel):
    id: int
    nome: str
    email: str

# Base de dados simulada (na memória)
users_db: List[User] = []

# Rota para listar todos os utilizadores
@app.get("/users", response_model=List[User])
def listar_utilizadores():
    return users_db

# Rota para obter utilizador por ID
@app.get("/users/{user_id}", response_model=User)
def obter_utilizador(user_id: int):
    for user in users_db:
        if user.id == user_id:
            return user
    raise HTTPException(status_code=404, detail="Utilizador não encontrado")

# Rota para criar utilizador
@app.post("/users", response_model=User)
def criar_utilizador(user: User):
    # Verificar se o ID já existe
    for u in users_db:
        if u.id == user.id:
            raise HTTPException(status_code=400, detail="ID já existe")
    users_db.append(user)
    return user

# Rota para apagar utilizador
@app.delete("/users/{user_id}")
def apagar_utilizador(user_id: int):
    for index, user in enumerate(users_db):
        if user.id == user_id:
            del users_db[index]
            return {"mensagem": "Utilizador apagado com sucesso"}
    raise HTTPException(status_code=404, detail="Utilizador não encontrado")
```

---

## 🚀 Como executar o servidor

No terminal, escreve:

```bash
uvicorn main:app --reload
```

* `main`: nome do ficheiro (`main.py`)
* `app`: nome da variável FastAPI
* `--reload`: reinicia automaticamente ao alterar o código (bom para desenvolvimento)

---

## 🌐 Acessar a API

### 1. Documentação automática (Swagger UI):

Abre o navegador e visita:

```
http://127.0.0.1:8000/docs
```

### 2. Outra documentação (ReDoc):

```
http://127.0.0.1:8000/redoc
```

---

## ✅ Testes na API (via Swagger UI)

1. Vai até `POST /users`
2. Adiciona:

```json
{
  "id": 1,
  "nome": "João",
  "email": "joao@email.com"
}
```

3. Vai até `GET /users` para ver a lista completa
4. Usa `GET /users/{user_id}` com `1`
5. Testa `DELETE /users/1`

---

## 📦 Extras úteis

Se quiser guardar os dados num ficheiro JSON ou usar uma base de dados real (como SQLite, PostgreSQL), FastAPI também é compatível com SQLAlchemy, Tortoise ORM, etc.

---

## 📁 Estrutura recomendada de pastas (para projetos maiores)

```
meu_app/
│
├── main.py
├── models.py
├── routers/
│   └── users.py
├── database.py
├── requirements.txt
```

---

## 📜 Requisitos (cria o ficheiro `requirements.txt`):

```text
fastapi
uvicorn
```

Depois, instala com:

```bash
pip install -r requirements.txt
```
