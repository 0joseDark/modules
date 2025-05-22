- [voltar](https://github.com/0joseDark/modules/blob/main/README.md)
- **Kivy**, um poderoso framework Python para criar interfaces gráficas (GUIs) modernas e multi-plataforma — funciona em Windows, Linux (como Ubuntu), Android e iOS. Abaixo, explico **passo a passo** como instalar, configurar e criar um exemplo **completo** de aplicação Kivy que roda tanto no **Windows 10** quanto no **Ubuntu**.

---

## ✅ O que é o Kivy?

O **Kivy** é um framework open-source para o desenvolvimento de aplicações com interfaces gráficas que funcionam em múltiplas plataformas com o **mesmo código**. Suporta **multitouch**, **widgets customizáveis**, **layouts dinâmicos** e **gráficos acelerados por GPU (OpenGL)**.

---

## 🛠️ Instalação do Kivy

### 👉 No Windows 10

1. **Instalar Python 3.8+**: [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)
2. **Instalar o Kivy no terminal (cmd ou PowerShell)**:

   ```bash
   python -m pip install --upgrade pip setuptools wheel
   python -m pip install "kivy[base]" kivy_examples
   ```

### 👉 No Ubuntu Linux

1. **Instalar dependências do sistema**:

   ```bash
   sudo apt update
   sudo apt install python3-pip python3-setuptools python3-wheel python3-virtualenv libgl1-mesa-dev
   ```

2. **Instalar o Kivy**:

   ```bash
   python3 -m pip install --upgrade pip setuptools wheel
   python3 -m pip install "kivy[base]" kivy_examples
   ```

---

## 🧪 Criar um Exemplo Completo com Kivy

Vamos fazer um programa com:

* Janela com um botão
* Um campo de texto
* Ao clicar no botão, exibe uma mensagem

### 🗂 Estrutura dos ficheiros

```
meu_app_kivy/
├── main.py
└── meu_layout.kv
```

---

### 📄 `main.py`

```python
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.lang import Builder

# Carrega o ficheiro KV
Builder.load_file("meu_layout.kv")

# Classe que representa o layout
class MeuWidget(BoxLayout):
    def mostrar_mensagem(self):
        nome = self.ids.input_nome.text
        self.ids.label_mensagem.text = f"Olá, {nome}!"

# Classe principal da App
class MeuApp(App):
    def build(self):
        return MeuWidget()

# Executar
if __name__ == '__main__':
    MeuApp().run()
```

---

### 📄 `meu_layout.kv`

```kv
<MeuWidget>:
    orientation: 'vertical'
    padding: 20
    spacing: 20

    TextInput:
        id: input_nome
        hint_text: "Escreve o teu nome"
        multiline: False
        size_hint_y: None
        height: 40

    Button:
        text: "Clique aqui"
        size_hint_y: None
        height: 50
        on_release: root.mostrar_mensagem()

    Label:
        id: label_mensagem
        text: "Mensagem aparecerá aqui."
```

---

## ▶️ Executar o programa

No terminal:

```bash
python main.py
```

A janela mostrará:

* Um campo de texto para digitar o nome
* Um botão
* Ao clicar, exibe "Olá, \[nome digitado]!"

---

## 🧼 Explicação passo a passo

| Parte               | Explicação                                                  |
| ------------------- | ----------------------------------------------------------- |
| `BoxLayout`         | Layout que organiza widgets em linha ou coluna              |
| `TextInput`         | Campo de entrada de texto                                   |
| `Button`            | Botão que chama uma função                                  |
| `Label`             | Exibe texto na interface                                    |
| `ids`               | Permite referenciar widgets definidos no ficheiro `.kv`     |
| `Builder.load_file` | Carrega o layout `.kv` para associar com a classe principal |
| `App`               | Classe base da aplicação Kivy                               |

---

## 📝 Notas

* O ficheiro `.kv` deve ter o **mesmo nome da classe do widget em minúsculas**, sem "App" (ex: `MeuWidget` → `meu_layout.kv`).
* A aplicação é **portável**, roda igual em Windows e Ubuntu.
* Pode criar interfaces complexas com `GridLayout`, `ScreenManager`, `Canvas`, `Imagens`, `Som`, `Vídeo`, etc.
