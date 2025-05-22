[voltar](https://github.com/0joseDark/modules/blob/main/README.md)
- O `libusb` é uma biblioteca C que fornece acesso genérico a dispositivos USB. Ela permite que programas controlem dispositivos USB sem a necessidade de drivers específicos. É multiplataforma (Windows, Linux, macOS, etc.).

Neste guia, vamos:

1. Explicar o que é o `libusb`.
2. Mostrar como instalar no **Windows 10** e no **Ubuntu**.
3. Apresentar um exemplo completo em **Python** usando `PyUSB`, que é um wrapper em Python para `libusb`.

---

## ✅ 1. O que é `libusb`

* **`libusb`** é uma biblioteca de comunicação USB de baixo nível.
* Permite:

  * Detetar dispositivos USB.
  * Enviar comandos para dispositivos.
  * Ler e escrever dados nas portas USB.
* É muito usada em **projetos com microcontroladores (ex: Arduino)**, scanners, impressoras, etc.

---

## 🛠️ 2. Instalação

### 💻 **No Ubuntu**

```bash
sudo apt update
sudo apt install libusb-1.0-0-dev python3-pip
pip install pyusb
```

### 🪟 **No Windows 10**

1. Instalar o Python:

   * [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)
   * Marcar a opção **"Add Python to PATH"**.

2. Instalar o `libusb`:

   * Baixe de [https://libusb.info](https://libusb.info).
   * Ou use um driver com o **Zadig**:

     * Baixe o Zadig: [https://zadig.akeo.ie/](https://zadig.akeo.ie/)
     * Execute, selecione o seu dispositivo, e instale o driver **libusb-win32** ou **WinUSB**.

3. Instalar o PyUSB:

   ```bash
   pip install pyusb
   ```

4. Verifique se o `libusb-1.0.dll` está disponível:

   * Coloque o `.dll` na mesma pasta do seu script ou no diretório do Python (`C:\Python3x\Lib\site-packages\usb\backend\`).

---

## 🧪 3. Exemplo Completo em Python

Este script lista todos os dispositivos USB ligados.

### `usb_listar_dispositivos.py`

```python
import usb.core
import usb.util

def listar_dispositivos_usb():
    dispositivos = usb.core.find(find_all=True)
    
    if dispositivos is None:
        print("Nenhum dispositivo USB encontrado.")
        return
    
    for dispositivo in dispositivos:
        print(f"Dispositivo encontrado:")
        print(f"  ID: {hex(dispositivo.idVendor)}:{hex(dispositivo.idProduct)}")
        try:
            print(f"  Fabricante: {usb.util.get_string(dispositivo, dispositivo.iManufacturer)}")
            print(f"  Produto: {usb.util.get_string(dispositivo, dispositivo.iProduct)}")
            print(f"  Número de Série: {usb.util.get_string(dispositivo, dispositivo.iSerialNumber)}")
        except usb.core.USBError:
            print("  (sem permissão para ler informações adicionais)")
        print("-" * 40)

if __name__ == "__main__":
    listar_dispositivos_usb()
```

---

## ⚠️ Notas importantes

* **Ubuntu**: Se não estiver como root, pode não ter permissão. Execute com:

  ```bash
  sudo python3 usb_listar_dispositivos.py
  ```

* **Windows**: Pode precisar de instalar um driver com o Zadig (como o WinUSB).

---

## 📌 Acessar dados do dispositivo USB

Exemplo para enviar e receber dados (supõe que conheces o dispositivo):

```python
dev = usb.core.find(idVendor=0xXXXX, idProduct=0xYYYY)
if dev is None:
    raise ValueError("Dispositivo não encontrado")

dev.set_configuration()
cfg = dev.get_active_configuration()
intf = cfg[(0,0)]

ep_out = usb.util.find_descriptor(intf, custom_match=lambda e: usb.util.endpoint_direction(e.bEndpointAddress) == usb.util.ENDPOINT_OUT)
ep_in = usb.util.find_descriptor(intf, custom_match=lambda e: usb.util.endpoint_direction(e.bEndpointAddress) == usb.util.ENDPOINT_IN)

ep_out.write(b'comando')
resposta = ep_in.read(64)
print(bytes(resposta))
```

---

## ✅ Resumo

| Passo | Descrição                                       |
| ----- | ----------------------------------------------- |
| 1     | Instalar `libusb` e `PyUSB`                     |
| 2     | Ligar o dispositivo USB                         |
| 3     | (Windows) Usar Zadig para instalar driver       |
| 4     | Executar script Python para listar ou comunicar |

---
