[**voltar**](https://github.com/0joseDark/modules/blob/main/README.md)
---
- Para desenvolver um módulo de "Dispositivos USB" no contexto do seu projeto em Python, vamos seguir uma abordagem que envolve:

1. **Explicação Geral de Módulos e Dispositivos USB em Python**  
2. **Desenvolvimento do Módulo em Python**  
3. **Incorporar "Dispositivos USB" ao seu projeto existente**  

---

### **1. Explicação Geral de Módulos e Dispositivos USB em Python**
#### O que são módulos?
- **Módulos** em Python são arquivos de código que contêm funções, classes ou variáveis prontas para serem reutilizadas em outros programas.
- Podem ser criados por você ou importados de bibliotecas externas (ex.: `os`, `sys`, `usb.core`).

#### Como Python interage com dispositivos USB?
- Python permite gerenciar dispositivos USB usando bibliotecas especializadas, como:
  - **`pyusb`**: Para comunicação genérica com dispositivos USB.
  - **`usbinfo`**: Fornece informações detalhadas sobre dispositivos conectados.
  - **`hid`**: Para dispositivos de entrada USB, como teclados ou ratos.
  - **`serial`**: Para dispositivos USB que usam portas seriais (como Arduino).

---

### **2. Desenvolvimento do Módulo em Python**
#### Funcionalidades Básicas
- Listar dispositivos USB conectados.
- Detalhar informações de cada dispositivo (ex.: ID do fabricante, ID do produto, nome do dispositivo).
- Fornecer uma interface para enviar ou receber dados de um dispositivo USB (se aplicável).

#### Código para o Módulo "dispositivos_usb.py"
```python
# dispositivos_usb.py
import usb.core
import usb.util

def listar_dispositivos_usb():
    """
    Lista todos os dispositivos USB conectados ao sistema.
    """
    dispositivos = usb.core.find(find_all=True)
    lista_dispositivos = []
    for dispositivo in dispositivos:
        lista_dispositivos.append({
            "ID Fabricante": hex(dispositivo.idVendor),
            "ID Produto": hex(dispositivo.idProduct),
            "Nome": usb.util.get_string(dispositivo, dispositivo.iProduct) if dispositivo.iProduct else "Desconhecido"
        })
    return lista_dispositivos

def detalhes_dispositivo_usb(id_vendor, id_product):
    """
    Retorna detalhes de um dispositivo USB específico.
    """
    dispositivo = usb.core.find(idVendor=int(id_vendor, 16), idProduct=int(id_product, 16))
    if dispositivo:
        return {
            "ID Fabricante": hex(dispositivo.idVendor),
            "ID Produto": hex(dispositivo.idProduct),
            "Fabricante": usb.util.get_string(dispositivo, dispositivo.iManufacturer) if dispositivo.iManufacturer else "Desconhecido",
            "Nome": usb.util.get_string(dispositivo, dispositivo.iProduct) if dispositivo.iProduct else "Desconhecido",
            "Número de Série": usb.util.get_string(dispositivo, dispositivo.iSerialNumber) if dispositivo.iSerialNumber else "Desconhecido"
        }
    else:
        return "Dispositivo não encontrado."

if __name__ == "__main__":
    print("Dispositivos USB conectados:")
    dispositivos = listar_dispositivos_usb()
    for idx, dispositivo in enumerate(dispositivos, start=1):
        print(f"{idx}: {dispositivo}")
```

---

### **3. Incorporar "Dispositivos USB" ao Seu Projeto**
#### No seu projeto Flask com XML:
1. **Página HTML para Dispositivos USB**:
   - Crie uma página chamada `dispositivos_usb.html` para exibir a lista de dispositivos USB.
   - Utilize AJAX para enviar e receber informações sem recarregar a página.

2. **Endpoint no Flask para Dispositivos USB**:
   - Adicione rotas no Flask para listar dispositivos e buscar detalhes.

#### Código para o Flask:
```python
from flask import Flask, jsonify, render_template
import dispositivos_usb

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/listar_usb")
def listar_usb():
    dispositivos = dispositivos_usb.listar_dispositivos_usb()
    return jsonify(dispositivos)

@app.route("/detalhes_usb/<id_vendor>/<id_product>")
def detalhes_usb(id_vendor, id_product):
    detalhes = dispositivos_usb.detalhes_dispositivo_usb(id_vendor, id_product)
    return jsonify(detalhes)

if __name__ == "__main__":
    app.run(debug=True)
```

#### Arquivo `dispositivos_usb.html`:
```html
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <title>Dispositivos USB</title>
</head>
<body>
    <h1>Dispositivos USB Conectados</h1>
    <button onclick="listarDispositivos()">Atualizar Lista</button>
    <ul id="lista_usb"></ul>

    <script>
        function listarDispositivos() {
            fetch('/listar_usb')
                .then(response => response.json())
                .then(data => {
                    const lista = document.getElementById('lista_usb');
                    lista.innerHTML = '';
                    data.forEach((dispositivo, index) => {
                        const item = document.createElement('li');
                        item.textContent = `#${index + 1}: ${dispositivo['Nome']} (Fabricante: ${dispositivo['ID Fabricante']}, Produto: ${dispositivo['ID Produto']})`;
                        lista.appendChild(item);
                    });
                });
        }
    </script>
</body>
</html>
```

---

### **Explicação Passo a Passo**
1. **Importação de Bibliotecas**:
   - `usb.core` e `usb.util` são usados para interagir com dispositivos USB.
2. **Listagem de Dispositivos**:
   - A função `usb.core.find()` identifica todos os dispositivos conectados.
3. **Integração com Flask**:
   - Criação de endpoints `/listar_usb` e `/detalhes_usb`.
   - Uso de `fetch` no HTML para comunicação assíncrona.
4. **Frontend**:
   - Exibição dinâmica da lista de dispositivos USB na página.
