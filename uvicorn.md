O Uvicorn é um servidor ASGI (Asynchronous Server Gateway Interface) rápido e leve, ideal para executar aplicações web baseadas em Python, especialmente aquelas criadas com frameworks como **FastAPI** e **Starlette**. Ele é amplamente usado para criar aplicações web modernas e eficientes. Vamos explorar como instalar, configurar e usar o Uvicorn no Windows 10, com exemplos e explicações passo a passo.

---

### **1. Instalar o Uvicorn**
Antes de começar, você precisa ter o Python 3.7 ou superior instalado no seu sistema. Depois, instale o Uvicorn usando o comando:

```bash
pip install uvicorn
```

---

### **2. Criar um Servidor Simples**
Vamos criar um servidor simples que responde "Olá, Mundo!" a uma solicitação HTTP.

1. Crie um ficheiro chamado `app.py`:

```python
# app.py
async def app(scope, receive, send):
    assert scope['type'] == 'http'
    response_body = b"Olá, Mundo!"
    headers = [(b"content-type", b"text/plain")]

    await send({
        'type': 'http.response.start',
        'status': 200,
        'headers': headers,
    })
    await send({
        'type': 'http.response.body',
        'body': response_body,
    })
```

2. Execute o servidor com o comando:

```bash
uvicorn app:app --host 127.0.0.1 --port 8000
```

### **Explicação**
- O `scope` contém informações sobre a solicitação.
- O `receive` é uma função assíncrona para receber mensagens do cliente.
- O `send` é uma função assíncrona para enviar respostas ao cliente.
- A aplicação responde com o texto "Olá, Mundo!" em formato `text/plain`.

---

### **3. Usar com FastAPI**
O Uvicorn é amplamente utilizado com o **FastAPI**, um framework moderno para criar APIs rápidas.

1. Instale o FastAPI e o Uvicorn:

```bash
pip install fastapi
pip install "uvicorn[standard]"
```

2. Crie um ficheiro chamado `main.py`:

```python
# main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"mensagem": "Olá, Mundo!"}

@app.get("/saudacao/{nome}")
def saudacao(nome: str):
    return {"mensagem": f"Olá, {nome}!"}
```

3. Execute o servidor com o comando:

```bash
uvicorn main:app --reload
```

4. Acesse no navegador:
   - Para a rota principal: [http://127.0.0.1:8000/](http://127.0.0.1:8000/)
   - Para a saudação personalizada: [http://127.0.0.1:8000/saudacao/João](http://127.0.0.1:8000/saudacao/João)

---

### **4. Opções Úteis do Uvicorn**
- **`--reload`**: Reinicia automaticamente o servidor ao detectar alterações no código.
- **`--host`**: Define o endereço de host (por exemplo, `0.0.0.0` para disponibilizar para outros dispositivos na rede).
- **`--port`**: Define a porta (padrão é `8000`).
- **`--workers`**: Número de processos simultâneos para lidar com solicitações.

Exemplo:

```bash
uvicorn main:app --host 0.0.0.0 --port 8080 --workers 4
```

---

### **5. Adicionar HTTPS**
Para usar HTTPS, você precisa de um certificado SSL. Suponha que você tenha os ficheiros `cert.pem` e `key.pem`:

```bash
uvicorn main:app --ssl-keyfile=key.pem --ssl-certfile=cert.pem
```

---

### **Conclusão**
O Uvicorn é uma ferramenta poderosa e fácil de usar para servir aplicações ASGI. Ele é rápido, eficiente e combina bem com frameworks modernos como o FastAPI. Use-o para criar aplicações web robustas e escaláveis.
