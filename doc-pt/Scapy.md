O Scapy é uma poderosa ferramenta para manipular e analisar pacotes de rede em Python. Ele permite criar, enviar, capturar e manipular pacotes de rede de forma flexível, sendo usado principalmente em testes de segurança, análise de rede e desenvolvimento de protocolos.

Aqui está um guia para começar a usar o Scapy no Windows 10, com explicações e exemplos básicos.

---

### **1. Instalação do Scapy**
1. Certifique-se de que o **Python** está instalado no seu sistema. Use uma versão recente (3.7 ou superior).
2. Abra o **Prompt de Comando** e instale o Scapy com o comando:
   ```bash
   pip install scapy
   ```
3. Para evitar problemas de permissão, execute o Prompt de Comando como **administrador**.

---

### **2. Conceitos básicos do Scapy**
- **Criação de pacotes**: Scapy permite criar pacotes de rede do zero.
- **Envio de pacotes**: Você pode enviar pacotes personalizados para a rede.
- **Captura de pacotes**: Monitorar e analisar o tráfego de rede.
- **Manipulação de pacotes**: Modificar pacotes capturados ou criados.

---

### **3. Exemplos práticos**

#### **3.1. Enviar um ping (ICMP Echo Request)**
Este exemplo envia um pacote ICMP (ping) para verificar a conectividade com um IP.

```python
from scapy.all import *

# Enviar um ping para o Google (8.8.8.8)
response = sr1(IP(dst="8.8.8.8")/ICMP(), timeout=2)

if response:
    print("Resposta recebida!")
    response.show()
else:
    print("Sem resposta do host.")
```

- **Explicação**:
  - `IP(dst="8.8.8.8")`: Cria um pacote IP com o destino especificado.
  - `/ICMP()`: Adiciona um pacote ICMP ao pacote IP.
  - `sr1()`: Envia o pacote e espera uma resposta (somente um pacote de resposta).

---

#### **3.2. Escutar pacotes na rede**
Este exemplo captura pacotes na rede local.

```python
from scapy.all import *

# Função para processar pacotes capturados
def process_packet(packet):
    print(packet.summary())  # Exibe um resumo do pacote

# Capturar pacotes na interface padrão (Ctrl+C para parar)
sniff(prn=process_packet, count=10)
```

- **Explicação**:
  - `sniff()`: Captura pacotes na rede.
  - `prn=process_packet`: Define uma função para processar cada pacote capturado.
  - `count=10`: Limita a captura a 10 pacotes.

---

#### **3.3. Fazer um traceroute simples**
Um traceroute exibe o caminho que os pacotes percorrem para alcançar um destino.

```python
from scapy.all import *

# Traceroute para um destino
result, unans = traceroute(["8.8.8.8"], maxttl=20)

# Exibir o resultado
result.show()
```

- **Explicação**:
  - `traceroute(["8.8.8.8"])`: Envia pacotes ICMP incrementando o TTL para mapear o caminho.
  - `maxttl=20`: Limita o TTL máximo para evitar loops infinitos.

---

#### **3.4. Escanear portas TCP de um host**
Este exemplo escaneia portas abertas em um endereço IP.

```python
from scapy.all import *

# Definir alvo
target_ip = "192.168.1.1"

# Escanear portas
for port in range(20, 1025):  # Escanear da porta 20 à 1024
    packet = IP(dst=target_ip)/TCP(dport=port, flags="S")
    response = sr1(packet, timeout=1, verbose=0)
    
    if response and response[TCP].flags == "SA":
        print(f"Porta {port} está aberta.")
```

- **Explicação**:
  - `TCP(dport=port, flags="S")`: Cria um pacote TCP com o flag SYN para iniciar a comunicação.
  - `sr1()`: Envia o pacote e aguarda resposta.
  - `flags == "SA"`: Indica que a porta está aberta.

---

### **4. Dicas para uso no Windows**
- Execute o script como administrador para evitar restrições de acesso à rede.
- Certifique-se de que o firewall ou antivírus não está bloqueando o tráfego gerado pelo Scapy.
- O Scapy funciona melhor com interfaces nativas, mas pode ter limitações no Windows. Considere usar o WinPcap ou Npcap para captura de pacotes.

---

### **5. Próximos passos**
- Explore mais funções no [site oficial do Scapy](https://scapy.net/).
- Teste outros protocolos, como ARP, UDP, DNS e HTTP.
- Integre o Scapy em scripts de segurança e automação de rede.
