O módulo `hid` (do pacote `hidapi` ou `hid` em Python) permite comunicar com dispositivos **HID (Human Interface Devices)** como teclados, ratos, comandos de jogo, leitores de código de barras, controladores USB, entre outros. Funciona tanto no **Windows 10** como no **Ubuntu Linux** e é muito útil para comunicação USB de baixo nível.

---

## ✅ 1. Instalar o módulo `hid`

### 🟦 No Windows 10:

```bash
pip install hid
```

### 🟪 No Ubuntu:

Antes de instalar, certifica-te que tens as dependências:

```bash
sudo apt-get install libhidapi-libusb0 libhidapi-hidraw0
pip install hid
```

---

## ✅ 2. Importar e listar os dispositivos HID ligados

```python
import hid

# Listar todos os dispositivos HID conectados
for device in hid.enumerate():
    print(f"Vendor ID : {hex(device['vendor_id'])}")
    print(f"Product ID: {hex(device['product_id'])}")
    print(f"Product   : {device['product_string']}")
    print(f"Serial Nº : {device['serial_number']}")
    print(f"Path      : {device['path']}")
    print("-" * 30)
```

---

## ✅ 3. Ligar a um dispositivo HID

Para te ligares a um dispositivo, precisas do **vendor\_id** e **product\_id**, ou do **path**.

```python
import hid

# Substituir pelos valores reais do teu dispositivo
VENDOR_ID = 0x1234
PRODUCT_ID = 0x5678

# Abre a conexão com o dispositivo HID
try:
    h = hid.Device(vid=VENDOR_ID, pid=PRODUCT_ID)
    print("Dispositivo ligado com sucesso.")
except Exception as e:
    print("Erro ao ligar:", e)
```

---

## ✅ 4. Escrever dados para o dispositivo HID

Muitos dispositivos HID aceitam comandos com o primeiro byte como **ID do relatório** (0x00 por padrão).

```python
# Enviar 8 bytes para o dispositivo (exemplo)
data = [0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07]  # Primeiro byte é Report ID (0x00)
h.write(data)
print("Dados enviados.")
```

---

## ✅ 5. Ler dados do dispositivo HID

```python
# Ler 8 bytes com timeout de 1000 ms (1 segundo)
try:
    resposta = h.read(8, timeout=1000)
    if resposta:
        print("Resposta recebida:", resposta)
    else:
        print("Sem resposta.")
except Exception as e:
    print("Erro ao ler:", e)
```

---

## ✅ 6. Fechar a conexão

```python
h.close()
print("Conexão encerrada.")
```

---

## 🔁 Exemplo completo com tudo

```python
import hid
import time

VENDOR_ID = 0x1234  # Substitui pelo ID do teu dispositivo
PRODUCT_ID = 0x5678

try:
    # Ligar ao dispositivo
    h = hid.Device(vid=VENDOR_ID, pid=PRODUCT_ID)
    print("Ligado ao dispositivo:", h.get_manufacturer_string(), h.get_product_string())

    # Enviar comando
    comando = [0x00, 0x01, 0x02, 0x03, 0x00, 0x00, 0x00, 0x00]
    h.write(comando)
    print("Comando enviado:", comando)

    # Aguardar resposta
    time.sleep(0.5)
    resposta = h.read(8, timeout=1000)
    print("Resposta:", resposta)

    # Fechar
    h.close()
    print("Conexão terminada.")

except Exception as e:
    print("Erro:", e)
```

---

## ✅ Notas importantes

* **Permissões no Ubuntu**:

  * Podes precisar de permissões para aceder ao dispositivo (`sudo`).
  * Cria uma regra `udev` para permitir acesso ao utilizador sem `sudo`.

```bash
sudo nano /etc/udev/rules.d/99-hid.rules
```

E adiciona:

```
SUBSYSTEM=="hidraw", ATTRS{idVendor}=="1234", ATTRS{idProduct}=="5678", MODE="0666"
```

Depois:

```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

* **No Windows**, não são necessárias regras adicionais.
