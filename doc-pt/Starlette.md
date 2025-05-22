- [voltar](https://github.com/0joseDark/modules/blob/main/README.md)
- O **Starlette** é um framework leve e rápido para construir aplicações web em Python. Ele é projetado para ser assíncrono e altamente eficiente, utilizando bibliotecas como `asyncio` e `ASGI` (Asynchronous Server Gateway Interface). Vou explicar como configurá-lo e criar exemplos em português, com comentários detalhados.

---

### Passos para Instalar e Configurar o Starlette

1. **Instale o Starlette e o servidor ASGI:**
   No Windows 10, abra o terminal ou o PowerShell e execute:
   ```bash
   pip install starlette uvicorn
   ```

2. **Crie um ficheiro Python para a aplicação:**
   Por exemplo, `app.py`.

3. **Estrutura do código básico:**
   Aqui está um exemplo básico de aplicação usando o Starlette.

---

### Exemplo 1: "Olá, Mundo!"

Crie um ficheiro chamado `app.py` e adicione o seguinte código:

```python
from starlette.applications import Starlette
from starlette.responses import JSONResponse
import uvicorn

# Configurar a aplicação Starlette
app = Starlette(debug=True)

# Criar uma rota básica
@app.route("/")
async def homepage(request):
    return JSONResponse({"mensagem": "Olá, Mundo!"})

# Executar o servidor
if __name__ == "__main__":
    uvicorn.run(app, host="127.0.0.1", port=8000)
```

### Como Executar:
1. Abra o terminal na pasta onde está o ficheiro `app.py`.
2. Execute o comando:
   ```bash
   python app.py
   ```
3. Abra o navegador e aceda a `http://127.0.0.1:8000`. Você verá:
   ```json
   {"mensagem": "Olá, Mundo!"}
   ```

---

### Exemplo 2: Receber Dados via POST

Atualize o ficheiro `app.py` com uma rota POST para receber dados JSON.

```python
from starlette.applications import Starlette
from starlette.responses import JSONResponse
from starlette.requests import Request
import uvicorn

app = Starlette(debug=True)

@app.route("/dados", methods=["POST"])
async def receber_dados(request: Request):
    dados = await request.json()  # Ler os dados JSON do corpo da requisição
    nome = dados.get("nome", "Visitante")
    return JSONResponse({"mensagem": f"Olá, {nome}!"})

if __name__ == "__main__":
    uvicorn.run(app, host="127.0.0.1", port=8000)
```

### Como Testar:
1. Use um cliente HTTP como o Postman ou `curl` para enviar uma requisição POST para `http://127.0.0.1:8000/dados`.
2. Envie o seguinte JSON no corpo da requisição:
   ```json
   {"nome": "João"}
   ```
3. A resposta será:
   ```json
   {"mensagem": "Olá, João!"}
   ```

---

### Exemplo 3: Servir Ficheiros Estáticos

Adicione suporte para servir ficheiros estáticos como imagens, CSS ou JavaScript.

```python
from starlette.applications import Starlette
from starlette.responses import JSONResponse
from starlette.staticfiles import StaticFiles
import uvicorn

app = Starlette(debug=True)

# Configurar pasta para ficheiros estáticos
app.mount("/static", StaticFiles(directory="static"), name="static")

@app.route("/")
async def homepage(request):
    return JSONResponse({"mensagem": "Visite /static para acessar os ficheiros estáticos."})

if __name__ == "__main__":
    uvicorn.run(app, host="127.0.0.1", port=8000)
```

### Como Configurar:
1. Crie uma pasta chamada `static` na mesma diretoria do `app.py`.
2. Coloque ficheiros, como `imagem.jpg`, dentro da pasta.
3. Aceda a `http://127.0.0.1:8000/static/imagem.jpg` para visualizar o ficheiro.

---

### Recursos Adicionais do Starlette

1. **Gestão de Rotas com Parâmetros:**
   ```python
   @app.route("/usuario/{id}")
   async def usuario(request):
       user_id = request.path_params['id']
       return JSONResponse({"id": user_id})
   ```

2. **Middleware:**
   Para adicionar lógica a todas as requisições:
   ```python
   from starlette.middleware.base import BaseHTTPMiddleware

   class MeuMiddleware(BaseHTTPMiddleware):
       async def dispatch(self, request, call_next):
           response = await call_next(request)
           response.headers['X-Powered-By'] = 'Starlette'
           return response

   app.add_middleware(MeuMiddleware)
   ```

3. **WebSockets:**
   Para comunicação em tempo real:
   ```python
   @app.websocket_route("/ws")
   async def websocket_endpoint(websocket):
       await websocket.accept()
       await websocket.send_text("Bem-vindo ao WebSocket!")
       await websocket.close()
   ```

---

Estas são introduções básicas ao **Starlette**. Para projetos mais complexos, ele pode ser combinado com ORMs como SQLAlchemy, autenticação, e templates (Jinja2).
