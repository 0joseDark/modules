O módulo `socket` em Python permite a comunicação entre computadores, processos ou dispositivos através de redes (como a Internet ou uma rede local). Ele funciona tanto no **Windows 10** como no **Ubuntu Linux**, pois faz parte da biblioteca padrão do Python e usa a API de sockets do sistema operativo.

---

## 📘 Introdução ao `socket`

Um **socket** é como uma "porta" de entrada e saída para dados entre dois programas. Pode funcionar em modo:

* **Servidor**: escuta conexões.
* **Cliente**: conecta-se ao servidor.

---

## 🧱 Tipos de Sockets

* `AF_INET`: usa IPv4.
* `SOCK_STREAM`: usa TCP (conexão confiável).
* `SOCK_DGRAM`: usa UDP (sem conexão).

---

## 📦 Instalar Python

Já vem com o módulo `socket`:

```bash
python --version
```

Se não estiver instalado:

**Windows**: baixar do [python.org](https://www.python.org)
**Ubuntu**:

```bash
sudo apt update
sudo apt install python3
```

---

## 🧪 Exemplo Completo: Cliente e Servidor TCP

### 🔹 Servidor TCP (Python)

```python
# servidor_tcp.py
import socket

# 1. Criar socket TCP/IP
servidor = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 2. Definir endereço IP e porta
host = '0.0.0.0'  # escuta em todas as interfaces
porta = 5000
servidor.bind((host, porta))

# 3. Escutar conexões
servidor.listen(1)
print(f"[Servidor] A escutar em {host}:{porta}")

# 4. Aceitar uma ligação
cliente, endereco = servidor.accept()
print(f"[Servidor] Ligação recebida de {endereco}")

# 5. Receber e enviar dados
while True:
    dados = cliente.recv(1024)
    if not dados:
        break
    print(f"[Servidor] Recebido: {dados.decode()}")
    cliente.sendall(b"Mensagem recebida")

# 6. Fechar ligação
cliente.close()
servidor.close()
```

---

### 🔹 Cliente TCP (Python)

```python
# cliente_tcp.py
import socket

# 1. Criar socket TCP/IP
cliente = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 2. Conectar ao servidor
host = '127.0.0.1'  # localhost (mesmo PC)
porta = 5000
cliente.connect((host, porta))
print(f"[Cliente] Ligado a {host}:{porta}")

# 3. Enviar mensagem
mensagem = "Olá servidor!"
cliente.sendall(mensagem.encode())

# 4. Receber resposta
resposta = cliente.recv(1024)
print(f"[Cliente] Resposta: {resposta.decode()}")

# 5. Fechar ligação
cliente.close()
```

---

## 🧪 Como testar

### No Windows 10 ou Ubuntu:

1. **Abrir dois terminais.**
2. **Num terminal**, correr o servidor:

```bash
python servidor_tcp.py
```

3. **Noutro terminal**, correr o cliente:

```bash
python cliente_tcp.py
```

### Resultado Esperado:

No terminal do **servidor**:

```
[Servidor] A escutar em 0.0.0.0:5000
[Servidor] Ligação recebida de ('127.0.0.1', XXXX)
[Servidor] Recebido: Olá servidor!
```

No terminal do **cliente**:

```
[Cliente] Ligado a 127.0.0.1:5000
[Cliente] Resposta: Mensagem recebida
```

---

## 📝 Explicação Passo a Passo

| Passo                | Descrição         |
| -------------------- | ----------------- |
| `socket.socket(...)` | Cria o socket     |
| `bind()`             | Define IP e porta |
| `listen()`           | Começa a escutar  |
| `accept()`           | Espera um cliente |
| `recv()`             | Lê mensagem       |
| `sendall()`          | Envia mensagem    |
| `close()`            | Fecha a conexão   |

---

## 🔐 Notas sobre firewall

### No Windows 10:

* Pode aparecer um aviso de firewall — permitir acesso.
* Pode ativar/desativar com `wf.msc`.

### No Ubuntu:

* Verifique se o `ufw` (firewall) está ativado:

```bash
sudo ufw status
```

* Pode permitir a porta:

```bash
sudo ufw allow 5000
```

---

## ✅ Conclusão

O módulo `socket` permite criar programas de comunicação de rede em Python de forma simples e multiplataforma.


