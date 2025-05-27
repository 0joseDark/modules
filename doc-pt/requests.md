O módulo `requests` em Python é uma biblioteca muito poderosa e fácil de usar para fazer **requisições HTTP** (como `GET`, `POST`, `PUT`, `DELETE`, etc.). Ele funciona da mesma forma tanto no **Windows 10** quanto no **Ubuntu**, porque é um módulo Python puro, ou seja, não depende diretamente do sistema operativo.

---

## ✅ **Instalação do módulo `requests`**

### 💻 No Windows 10 ou Ubuntu (no terminal ou no CMD):

```bash
pip install requests
```

> Se estiver a usar Python 3, pode usar:

```bash
pip3 install requests
```

---

## 📌 **O que o módulo `requests` pode fazer:**

* Enviar e receber **dados** via HTTP
* Aceder a **API's** (REST)
* Fazer **login automático**, **envio de ficheiros**, **cookies**, etc.
* Trabalhar com **JSON**, **formulários**, etc.

---

## 🧠 **Funções principais do módulo `requests`:**

| Método HTTP | Função `requests`   | Usado para...                |
| ----------- | ------------------- | ---------------------------- |
| `GET`       | `requests.get()`    | Obter dados de um servidor   |
| `POST`      | `requests.post()`   | Enviar dados para o servidor |
| `PUT`       | `requests.put()`    | Atualizar dados no servidor  |
| `DELETE`    | `requests.delete()` | Apagar dados no servidor     |

---

## 🧪 **Exemplo completo passo a passo**

Vamos fazer um script que:

1. Usa `GET` para buscar dados de uma API pública.
2. Usa `POST` para enviar dados simulados para um servidor de testes.
3. Mostra a resposta, o código e os dados JSON recebidos.

### 📄 Código Python com comentários:

```python
import requests  # importa o módulo

# 1. Fazer um pedido GET para uma API pública
print("=== GET ===")
url_get = "https://jsonplaceholder.typicode.com/posts/1"
resposta_get = requests.get(url_get)

print("Status Code:", resposta_get.status_code)  # mostra o código da resposta
print("Resposta JSON:")
print(resposta_get.json())  # mostra o conteúdo da resposta em JSON

# 2. Fazer um pedido POST (simular envio de dados)
print("\n=== POST ===")
url_post = "https://jsonplaceholder.typicode.com/posts"
dados = {
    "title": "Teste com Python",
    "body": "Este é um teste usando o módulo requests",
    "userId": 1
}

resposta_post = requests.post(url_post, json=dados)

print("Status Code:", resposta_post.status_code)
print("Resposta JSON:")
print(resposta_post.json())

# 3. Verificar cabeçalhos da resposta
print("\n=== Cabeçalhos ===")
print(resposta_post.headers)
```

---

## 📦 Saída esperada (resumo)

```txt
=== GET ===
Status Code: 200
Resposta JSON:
{'userId': 1, 'id': 1, 'title': '...', 'body': '...'}

=== POST ===
Status Code: 201
Resposta JSON:
{'title': 'Teste com Python', 'body': '...', 'userId': 1, 'id': 101}

=== Cabeçalhos ===
{'Content-Type': 'application/json; charset=utf-8', ...}
```

> ✅ Nota: A API `https://jsonplaceholder.typicode.com` é falsa, usada apenas para testes — não altera dados reais.

---

## 💡 Dicas úteis

* Use `resposta.text` se a resposta não for JSON.
* Use `resposta.status_code` para verificar se a requisição foi bem-sucedida (`200`, `201`, etc.).
* Pode enviar ficheiros com `requests.post(url, files={...})`
* Pode enviar parâmetros com `requests.get(url, params={"chave": "valor"})`

---

## 📌 Requisitos

* Python 3.x
* Módulo `requests` instalado (funciona no Windows 10 e Ubuntu igualmente)
