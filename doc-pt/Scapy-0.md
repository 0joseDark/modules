O `Scapy` é um poderoso módulo em Python para manipulação de pacotes de rede. Ele permite **criar, enviar, capturar e analisar pacotes** de forma flexível e interativa.

---

### ✅ **1. Instalação do Scapy**

#### 📍 Windows 10

1. Abre o **Prompt de Comando (CMD)** ou **PowerShell** como administrador.
2. Escreve:

   ```bash
   pip install scapy
   ```

#### 📍 Ubuntu Linux

1. Abre o terminal.
2. Escreve:

   ```bash
   sudo apt update
   sudo apt install python3-pip
   pip3 install scapy
   ```

---

### ✅ **2. Importação básica do módulo**

```python
from scapy.all import *
```

> Isto importa todas as funcionalidades principais de Scapy.

---

### ✅ **3. Funções principais do Scapy**

| Função           | Descrição                                   |
| ---------------- | ------------------------------------------- |
| `IP()`           | Cria um pacote IP                           |
| `TCP()`, `UDP()` | Cria cabeçalhos de transporte TCP ou UDP    |
| `send()`         | Envia pacotes (camada 3)                    |
| `sendp()`        | Envia pacotes (camada 2, Ethernet)          |
| `sr()`           | Envia e recebe pacotes (camada 3)           |
| `sniff()`        | Captura pacotes                             |
| `ls()`           | Lista campos de um protocolo (ex: `ls(IP)`) |
| `hexdump()`      | Mostra pacotes em formato hexadecimal       |

---

### ✅ **4. Exemplo completo passo a passo**

Vamos criar um **scanner de portas TCP** simples com Scapy que verifica se uma porta está aberta num IP.

#### 🔍 Objetivo

Enviar pacotes SYN para um IP e verificar se a resposta é SYN+ACK (porta aberta) ou RST (porta fechada).

---

### 🔧 Código completo: `scanner_portas.py`

```python
from scapy.all import IP, TCP, sr1
import sys

def scan_port(ip, porta):
    pacote_ip = IP(dst=ip)
    pacote_tcp = TCP(dport=porta, flags='S')
    
    resposta = sr1(pacote_ip/pacote_tcp, timeout=1, verbose=0)

    if resposta is None:
        print(f"Porta {porta} está filtrada ou não respondeu.")
    elif resposta.haslayer(TCP):
        if resposta.getlayer(TCP).flags == 0x12:
            print(f"Porta {porta} está ABERTA.")
            # enviar RST para terminar
            rst = TCP(dport=porta, flags='R')
            send(pacote_ip/rst, verbose=0)
        elif resposta.getlayer(TCP).flags == 0x14:
            print(f"Porta {porta} está FECHADA.")
    else:
        print(f"Porta {porta} retornou uma resposta inesperada.")

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Uso: python scanner_portas.py <IP> <PORTA>")
        sys.exit(1)

    destino_ip = sys.argv[1]
    destino_porta = int(sys.argv[2])
    scan_port(destino_ip, destino_porta)
```

---

### 🖥️ Como executar

#### ✅ Windows 10 ou Ubuntu:

No terminal ou CMD:

```bash
python scanner_portas.py 192.168.1.1 80
```

---

### 🛡️ Importante: Permissões

* Em **Ubuntu**, pode precisar de `sudo` para enviar pacotes:

  ```bash
  sudo python3 scanner_portas.py 192.168.1.1 80
  ```

* Em **Windows**, recomenda-se abrir o terminal como **administrador**.

---

### ✅ Extra: Capturar pacotes na rede

```python
from scapy.all import sniff

# Capturar 5 pacotes na interface padrão
pacotes = sniff(count=5)
pacotes.summary()
```

---

### ✅ Listar campos de protocolos

```python
from scapy.all import ls
ls(IP)
ls(TCP)
```

---

### 📦 Exemplo de criação de pacote e visualização

```python
p = IP(dst="8.8.8.8")/ICMP()
p.show()
```

---

### ✅ Conclusão

O `scapy` é uma ferramenta avançada para testes de rede, ideal para:

* Pentesters
* Analistas de redes
* Programadores de segurança
