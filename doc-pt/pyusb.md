módulo **`pyusb`** para acessar dispositivos USB no **Windows 10** e no **Ubuntu Linux**, e fazer um **exemplo completo** que lista os dispositivos USB conectados.

---

## ✅ O que é o `pyusb`?

O `pyusb` é um módulo Python que permite interagir com dispositivos USB diretamente, através da biblioteca de backend como `libusb`.

Ele é multiplataforma e pode ser usado em **Windows, Linux e macOS**. Ele facilita a comunicação com dispositivos USB sem drivers especiais.

---

## 🧰 Pré-requisitos

### 👉 No Windows 10:

1. **Instalar Python** (3.x):
   [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)

2. **Instalar `pyusb`:**

   ```bash
   pip install pyusb
   ```

3. **Instalar o driver libusb-win32 ou Zadig:**

   O `pyusb` precisa da biblioteca `libusb`. No Windows, você deve instalar os drivers com o Zadig:

   * Baixar: [https://zadig.akeo.ie/](https://zadig.akeo.ie/)
   * Executar o Zadig
   * Escolher o dispositivo USB
   * Selecionar `libusb-win32` como driver
   * Clicar em "Install Driver"

---

### 👉 No Ubuntu Linux:

1. **Instalar Python (geralmente já vem instalado):**

   ```bash
   sudo apt update
   sudo apt install python3 python3-pip
   ```

2. **Instalar `pyusb` e `libusb-1.0`:**

   ```bash
   sudo apt install libusb-1.0-0-dev
   pip3 install pyusb
   ```

3. **Permissões de USB (opcional):**
   Para evitar usar `sudo`, crie uma regra `udev`:

   ```bash
   sudo nano /etc/udev/rules.d/50-myusb.rules
   ```

   Exemplo de conteúdo:

   ```
   SUBSYSTEM=="usb", MODE="0666"
   ```

   Depois:

   ```bash
   sudo udevadm control --reload
   sudo udevadm trigger
   ```

---

## 📜 Exemplo completo: Listar dispositivos USB conectados

### 🔧 Código Python:

```python
import usb.core
import usb.util

def listar_dispositivos_usb():
    # Encontra todos os dispositivos USB
    dispositivos = usb.core.find(find_all=True)

    if not dispositivos:
        print("Nenhum dispositivo USB encontrado.")
        return

    print("Dispositivos USB encontrados:\n")
    for dispositivo in dispositivos:
        print(f"ID do fabricante : {hex(dispositivo.idVendor)}")
        print(f"ID do produto    : {hex(dispositivo.idProduct)}")

        try:
            fabricante = usb.util.get_string(dispositivo, dispositivo.iManufacturer)
            produto = usb.util.get_string(dispositivo, dispositivo.iProduct)
            numero_serie = usb.util.get_string(dispositivo, dispositivo.iSerialNumber)
        except usb.core.USBError as e:
            fabricante = produto = numero_serie = "Erro de acesso"
            print(f"Erro ao acessar strings: {e}")

        print(f"Fabricante       : {fabricante}")
        print(f"Produto          : {produto}")
        print(f"Nº de série      : {numero_serie}")
        print("-" * 40)

if __name__ == "__main__":
    listar_dispositivos_usb()
```

---

## ▶️ Como executar

### No **Windows**:

```bash
python listar_usb.py
```

> ⚠️ No Windows, você deve instalar os drivers corretos com o Zadig para conseguir acesso aos dispositivos.

### No **Ubuntu**:

```bash
python3 listar_usb.py
```

> 🔐 Se aparecer erro de permissão, use `sudo`, ou configure as regras `udev`.

---

## 📦 Extras (opcional)

Você pode também usar:

* `dispositivo.bcdDevice`: versão do dispositivo
* `dispositivo.bDeviceClass`: classe do dispositivo (por ex., áudio, vídeo)
* `dispositivo.bNumConfigurations`: número de configurações USB disponíveis

---

## 🧪 Testado com:

* USB Pendrive
* Placa Arduino
* Teclado/Rato USB

---

## ❗ Dicas de depuração

* Se aparecer erro `usb.core.USBError: [Errno 13] Access denied (insufficient permissions)` no Linux → use `sudo` ou regras `udev`.
* Se o dispositivo não aparece → verifique se o driver está instalado corretamente (Zadig no Windows).
