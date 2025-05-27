## 🧠 O que é o **Paramiko**?

**Paramiko** é um módulo Python que permite fazer **conexões SSH (Secure Shell)** e **transferências SFTP** (como FTP, mas via SSH). Ele é usado para automatizar tarefas em servidores remotos, executar comandos, enviar e receber ficheiros com segurança.

---

## 📦 Instalação no **Windows 10** e **Ubuntu**

### ▶️ Passo 1: Instalar o módulo

No **Windows 10** e no **Ubuntu**, usa o seguinte comando no terminal:

```bash
pip install paramiko
```

---

## 📁 Estrutura do exemplo completo

Vamos criar um script que:

1. Conecta-se por SSH a um servidor remoto.
2. Executa um comando remoto (`ls`).
3. Faz download e upload de ficheiros via SFTP.
4. Fecha a conexão.

---

## ⚙️ Exemplo completo passo a passo

### 📝 Script: `exemplo_paramiko.py`

```python
import paramiko

# Passo 1: Criar um cliente SSH
ssh = paramiko.SSHClient()

# Passo 2: Aceitar automaticamente chaves desconhecidas (não recomendado para produção)
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())

# Passo 3: Conectar ao servidor
servidor = '192.168.1.10'         # IP ou domínio do servidor
utilizador = 'seu_utilizador'     # Nome de utilizador SSH
senha = 'sua_senha'               # Palavra-passe

try:
    print("A ligar ao servidor...")
    ssh.connect(servidor, username=utilizador, password=senha)
    print("Ligação SSH estabelecida com sucesso!")

    # Passo 4: Executar comando remoto
    comando = 'ls -la'
    stdin, stdout, stderr = ssh.exec_command(comando)

    print("\nResultado do comando remoto:")
    for linha in stdout.readlines():
        print(linha.strip())

    # Passo 5: Transferência SFTP
    sftp = ssh.open_sftp()
    
    # Upload: Enviar ficheiro local para o servidor
    ficheiro_local = 'teste_envio.txt'
    ficheiro_remoto = '/home/seu_utilizador/teste_envio.txt'
    sftp.put(ficheiro_local, ficheiro_remoto)
    print(f"\nFicheiro '{ficheiro_local}' enviado para o servidor.")

    # Download: Buscar ficheiro do servidor
    ficheiro_para_receber = '/home/seu_utilizador/teste_receber.txt'
    ficheiro_guardar = 'teste_recebido.txt'
    sftp.get(ficheiro_para_receber, ficheiro_guardar)
    print(f"Ficheiro '{ficheiro_para_receber}' recebido do servidor.")

    sftp.close()
    ssh.close()
    print("\nConexão encerrada com sucesso.")

except Exception as e:
    print(f"Erro: {e}")
```

---

## 📁 Ficheiros usados no exemplo

1. `teste_envio.txt` – um ficheiro qualquer que tenhas localmente.
2. `teste_receber.txt` – deve já existir no servidor para o download.

---

## 🖥️ Testar no **Windows 10**

1. Certifica-te de que tens o Python instalado (usa `python --version` no CMD).
2. Cria o ficheiro `exemplo_paramiko.py`.
3. Cria também `teste_envio.txt`.
4. Corre com:

```bash
python exemplo_paramiko.py
```

---

## 🖥️ Testar no **Ubuntu**

1. Idêntico ao Windows, mas usa o terminal.
2. Instala o Python e `pip` se necessário:

```bash
sudo apt update
sudo apt install python3 python3-pip
pip3 install paramiko
```

3. Corre com:

```bash
python3 exemplo_paramiko.py
```

---

## 🔐 Segurança

* Para produção, usa **chaves SSH (privada/pública)** em vez de palavra-passe.
* Exemplo:

```python
ssh.connect(servidor, username=utilizador, key_filename='/caminho/para/id_rsa')
```

---

## ✅ Resumo dos passos:

| Passo | Descrição                         |
| ----- | --------------------------------- |
| 1     | Instalar o `paramiko`             |
| 2     | Criar cliente SSH                 |
| 3     | Conectar ao servidor              |
| 4     | Executar comando remoto           |
| 5     | Enviar/receber ficheiros via SFTP |
| 6     | Fechar conexões SSH e SFTP        |

