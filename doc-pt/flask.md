**módulo Flask**, uma microframework web em Python muito usada para criar **servidores web simples** e **APIs REST**. Vou explicar passo a passo como instalar, configurar e criar uma aplicação Flask, **tanto no Windows 10 quanto no Ubuntu**, e depois mostrar um **exemplo completo com comentários**.

---

## ✅ O que é o Flask?

Flask é um microframework para aplicações web escrito em Python. Ele é leve e simples, permitindo que você crie servidores web, APIs ou até mesmo sites com interface.

---

## 🛠️ Instalação do Flask

### 🔷 Windows 10

1. **Instalar o Python:**

   * Acede a [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)
   * Faz download e instala (marca a opção *"Add Python to PATH"*)
2. **Instalar o Flask:**
   Abre o *cmd* ou *PowerShell* e digita:

   ```bash
   pip install flask
   ```

---

### 🔶 Ubuntu Linux

1. **Instalar Python (normalmente já vem instalado):**

   ```bash
   sudo apt update
   sudo apt install python3 python3-pip
   ```

2. **Instalar Flask:**

   ```bash
   pip3 install flask
   ```

---

## 📁 Estrutura básica do projeto

```
meu_app/
│
├── app.py           ← ficheiro principal Flask
├── templates/
│   └── index.html   ← página HTML do site
└── static/          ← imagens, CSS, JS (opcional)
```

---

## ✅ Exemplo completo: servidor Flask com HTML

### 📄 `app.py`

```python
from flask import Flask, render_template, request

# Cria a aplicação Flask
app = Flask(__name__)

# Página principal
@app.route('/')
def index():
    return render_template('index.html')

# Página que trata o formulário
@app.route('/processa', methods=['POST'])
def processa():
    nome = request.form['nome']
    return f"<h1>Olá, {nome}!</h1>"

# Inicia o servidor
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
```

---

### 📄 `templates/index.html`

Cria a pasta `templates` e dentro dela o ficheiro `index.html` com o seguinte conteúdo:

```html
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <title>Exemplo Flask</title>
</head>
<body>
    <h1>Bem-vindo ao Flask!</h1>
    <form action="/processa" method="post">
        <label for="nome">O teu nome:</label>
        <input type="text" id="nome" name="nome">
        <button type="submit">Enviar</button>
    </form>
</body>
</html>
```

---

## ▶️ Executar o projeto

No terminal (Windows ou Ubuntu), vai até à pasta onde está o `app.py` e escreve:

```bash
python app.py
```

Se estiveres no Ubuntu e o Python 3 for necessário:

```bash
python3 app.py
```

Acede no navegador:

```
http://localhost:5000
```

---

## 🔍 Explicação passo a passo

| Linha / Parte                               | Explicação                                                                                        |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `Flask(__name__)`                           | Cria a aplicação Flask. `__name__` permite que Flask saiba onde está o ficheiro principal.        |
| `@app.route('/')`                           | Define a rota principal, que responde ao URL `/`.                                                 |
| `render_template()`                         | Carrega um ficheiro HTML da pasta `templates`.                                                    |
| `@app.route('/processa', methods=['POST'])` | Define uma rota que responde ao envio do formulário.                                              |
| `request.form['nome']`                      | Acede ao dado enviado pelo formulário.                                                            |
| `app.run(...)`                              | Inicia o servidor no endereço `http://0.0.0.0:5000` com `debug=True` (útil para desenvolvimento). |

---

## 📌 Notas adicionais

* `templates/` é obrigatória para os HTMLs.
* `static/` é usada para imagens, CSS ou JS.
* Pode usar `GET` e `POST` em formulários.
* Para APIs, pode retornar JSON com `return jsonify(...)`.

---

## 🧪 Teste adicional: uma API simples com JSON

### Alterar `app.py` para incluir:

```python
from flask import jsonify

@app.route('/api/dados')
def dados():
    return jsonify({"nome": "João", "idade": 30})
```

Agora, acede a:

```
http://localhost:5000/api/dados
```

Irás ver:

```json
{
  "nome": "João",
  "idade": 30
}
```

---

Se desejares, posso ajudar a criar:

* Interface gráfica com Flask para projeto específico.
* Ligação a base de dados (SQLite ou MySQL).
* Versão com autenticação.
