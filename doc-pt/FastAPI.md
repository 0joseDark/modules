- [voltar](https://github.com/0joseDark/modules/blob/main/README.md)
- O **FastAPI** é um framework web rápido e moderno para Python, ideal para construir APIs de forma eficiente. Ele utiliza a tipagem do Python para facilitar a validação automática de dados e gerar documentação interativa automaticamente.

Aqui está um guia para começar com o FastAPI no Windows 10, incluindo exemplos.

---

## **Pré-requisitos**
1. Certifique-se de ter o Python instalado (versão 3.7 ou superior).
   - Para verificar: `python --version`
   - Para instalar: [Download Python](https://www.python.org/downloads/)
2. Instale o FastAPI e o servidor ASGI Uvicorn:
   ```bash
   pip install fastapi uvicorn
   ```

---

## **Criando um Projeto Simples com FastAPI**

### 1. **Estrutura do Projeto**
Vamos criar uma API simples que gerencia usuários. A estrutura será:

```
projeto_fastapi/
│
├── main.py          # Arquivo principal do FastAPI
├── models.py        # Estrutura de dados
└── requirements.txt # Dependências do projeto
```

---

### 2. **Código Base: `main.py`**

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

# Modelo de dados para o usuário
class Usuario(BaseModel):
    id: int
    nome: str
    email: str

# Base de dados simulada
usuarios = {}

# Rota inicial
@app.get("/")
def leia_raiz():
    return {"mensagem": "Bem-vindo à API de Usuários!"}

# Criar um novo usuário
@app.post("/usuarios/")
def criar_usuario(usuario: Usuario):
    if usuario.id in usuarios:
        raise HTTPException(status_code=400, detail="Usuário já existe.")
    usuarios[usuario.id] = usuario
    return {"mensagem": "Usuário criado com sucesso!"}

# Listar todos os usuários
@app.get("/usuarios/")
def listar_usuarios():
    return usuarios

# Obter detalhes de um usuário
@app.get("/usuarios/{usuario_id}")
def obter_usuario(usuario_id: int):
    if usuario_id not in usuarios:
        raise HTTPException(status_code=404, detail="Usuário não encontrado.")
    return usuarios[usuario_id]

# Apagar um usuário
@app.delete("/usuarios/{usuario_id}")
def apagar_usuario(usuario_id: int):
    if usuario_id not in usuarios:
        raise HTTPException(status_code=404, detail="Usuário não encontrado.")
    del usuarios[usuario_id]
    return {"mensagem": "Usuário apagado com sucesso!"}
```

---

### 3. **Executando o Servidor**
1. No terminal, navegue até o diretório do projeto:
   ```bash
   cd projeto_fastapi
   ```
2. Execute o servidor com o Uvicorn:
   ```bash
   uvicorn main:app --reload
   ```
3. Acesse no navegador:
   - A API: [http://127.0.0.1:8000](http://127.0.0.1:8000)
   - A documentação automática: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

### 4. **Exemplo de Testes**
Use **cURL**, **Postman** ou **Python requests** para interagir com a API.

#### **Criar Usuário**
```bash
curl -X POST "http://127.0.0.1:8000/usuarios/" -H "Content-Type: application/json" -d "{\"id\":1,\"nome\":\"João\",\"email\":\"joao@email.com\"}"
```

#### **Listar Usuários**
```bash
curl -X GET "http://127.0.0.1:8000/usuarios/"
```

---

## **Explicação do Código**
1. **FastAPI** usa decoradores (`@app`) para definir rotas.
2. **Pydantic** valida automaticamente os dados com base no modelo `Usuario`.
3. A documentação interativa (`/docs`) é gerada automaticamente, facilitando testes.
4. **HTTPException** lida com erros personalizados.

---

### Exemplo Avançado
Adicione autenticação JWT ou integre com uma base de dados real (usando **SQLite** ou **PostgreSQL** com **SQLAlchemy**)
