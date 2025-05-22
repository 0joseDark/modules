O módulo `usbinfo` em Python é usado para obter **informações sobre dispositivos USB conectados ao sistema**, como o nome do fabricante, número de série, ID do produto, e ID do fabricante. Ele é útil tanto no **Windows 10** como no **Ubuntu Linux**, embora haja algumas diferenças no funcionamento devido ao sistema operativo.

---

## ✅ Instalação do `usbinfo`

No Windows e no Ubuntu:

```bash
pip install usbinfo
```

---

## 🔍 O que o `usbinfo` faz?

O `usbinfo`:

* Lista todos os dispositivos USB conectados.
* Mostra informações como:

  * `Vendor ID (VID)`
  * `Product ID (PID)`
  * `Manufacturer`
  * `Serial Number`
  * `Product Name`

---

## 🧪 Exemplo Completo com Explicações

Aqui está um exemplo funcional com **comentários passo a passo**, compatível com **Windows 10 e Ubuntu**.

```python
import usbinfo

def listar_dispositivos_usb():
    print("🔌 Dispositivos USB conectados:\n")

    # Lista todos os dispositivos USB encontrados
    dispositivos = usbinfo.list_usb_devices()

    # Se não houver dispositivos
    if not dispositivos:
        print("Nenhum dispositivo USB encontrado.")
        return

    # Para cada dispositivo encontrado
    for idx, dispositivo in enumerate(dispositivos):
        print(f"📦 Dispositivo {idx + 1}")
        print(f"  - Vendor ID      : {dispositivo.vendor_id}")
        print(f"  - Product ID     : {dispositivo.product_id}")
        print(f"  - Fabricante     : {dispositivo.manufacturer}")
        print(f"  - Produto        : {dispositivo.product}")
        print(f"  - Número de série: {dispositivo.serial_number}")
        print(f"  - Caminho        : {dispositivo.device_path}")
        print()

if __name__ == "__main__":
    listar_dispositivos_usb()
```

---

## 🧾 Explicações dos Campos

| Campo           | Descrição                                                                             |
| --------------- | ------------------------------------------------------------------------------------- |
| `vendor_id`     | ID do fabricante (por exemplo, `0x046D` para Logitech)                                |
| `product_id`    | ID do produto (identifica o modelo do dispositivo)                                    |
| `manufacturer`  | Nome do fabricante (ex: "SanDisk")                                                    |
| `product`       | Nome do produto (ex: "Cruzer Blade")                                                  |
| `serial_number` | Número de série do dispositivo (único)                                                |
| `device_path`   | Caminho do dispositivo no sistema (como `/dev/...` no Linux ou `USB\\...` no Windows) |

---

## 🪟 Diferenças entre Windows e Ubuntu

| Sistema     | Requisitos               | Notas adicionais                                                            |
| ----------- | ------------------------ | --------------------------------------------------------------------------- |
| **Windows** | Nada extra necessário    | Funciona direto após `pip install usbinfo`                                  |
| **Ubuntu**  | Pode requerer permissões | Use `sudo` se necessário. Pode precisar de udev rules para acesso sem root. |

---

## 💡 Dica para Ubuntu: criar regra udev

Se no Ubuntu o script só funcionar com `sudo`, podes criar uma regra udev:

1. Cria o ficheiro:

```bash
sudo nano /etc/udev/rules.d/99-usbinfo.rules
```

2. Adiciona (exemplo para todos dispositivos USB):

```
SUBSYSTEM=="usb", MODE="0666"
```

3. Reinicia o udev:

```bash
sudo udevadm control --reload
sudo udevadm trigger
```

---

## 🖥️ Output de exemplo

```text
🔌 Dispositivos USB conectados:

📦 Dispositivo 1
  - Vendor ID      : 0x0781
  - Product ID     : 0x5567
  - Fabricante     : SanDisk
  - Produto        : Cruzer Blade
  - Número de série: 4C531001230421103391
  - Caminho        : \\.\USB#VID_0781&PID_5567#4C531001230421103391
```
