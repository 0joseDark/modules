[voltar](https://github.com/0joseDark/modules/blob/main/README.md)
**Dear PyGui**, um módulo Python para criar interfaces gráficas modernas e rápidas com aceleração por GPU. Ele funciona bem no **Windows 10** e **Ubuntu Linux**.

---

## 🧩 O que é o Dear PyGui?

O **Dear PyGui** é um **framework GUI** (Interface Gráfica do Utilizador) **baseado em GPU**, criado sobre a biblioteca **Dear ImGui** (escrita em C++). É **simples, rápido, leve** e ideal para aplicações interativas como **ferramentas, visualizações e protótipos**.

---

## 📦 Instalação

### 🔹 No Windows 10

1. Abre o **Terminal do Windows (cmd)** ou **PowerShell**
2. Instala com:

```bash
pip install dearpygui
```

### 🔹 No Ubuntu Linux

1. Abre o terminal
2. Instala com:

```bash
pip3 install dearpygui
```

> ⚠️ Certifica-te de que o Python e o pip estão instalados (`sudo apt install python3 python3-pip` no Ubuntu)

---

## ✅ Exemplo Completo

Vamos criar um exemplo que inclui:

* Janela principal com título
* Caixa de texto
* Botão
* Texto dinâmico (resposta ao clicar)
* Menus
* Função de callback

### 📄 Código: `exemplo_gui.py`

```python
from dearpygui.core import *
from dearpygui.simple import *

# Função chamada quando o botão é clicado
def ao_clicar_botao(sender, data):
    nome = get_value("##input_nome")
    set_value("##saida_texto", f"Olá, {nome}! Bem-vindo ao Dear PyGui.")

# Interface gráfica
with window("Janela Principal", width=400, height=300):
    add_menu_bar("Menu Principal")
    with menu("Ficheiro"):
        add_menu_item("Sair", callback=lambda s, d: stop_dearpygui())
    with menu("Ajuda"):
        add_menu_item("Sobre", callback=lambda s, d: log_info("Criado com Dear PyGui"))

    add_text("Escreve o teu nome:")
    add_input_text("##input_nome", default_value="", hint="Nome aqui")
    add_button("Dizer Olá", callback=ao_clicar_botao)
    add_spacing(count=2)
    add_text("", source="##saida_texto")

# Corre a aplicação
start_dearpygui()
```

---

## 📌 Passo a Passo Explicado

| Passo                             | Descrição                                                                      |
| --------------------------------- | ------------------------------------------------------------------------------ |
| `from dearpygui.core`             | Importa as funções principais (como `add_text`, `set_value`, etc).             |
| `from dearpygui.simple`           | Importa os **contextos simplificados**, como `with window()` ou `with menu()`. |
| `with window("Janela Principal")` | Cria uma janela com título.                                                    |
| `add_input_text()`                | Caixa onde o utilizador escreve o nome.                                        |
| `add_button()`                    | Botão com uma função de **callback** associada.                                |
| `set_value()`                     | Atualiza o texto quando se clica no botão.                                     |
| `start_dearpygui()`               | Inicia o loop principal da aplicação.                                          |

---

## 💻 Executar o Programa

### No Windows ou Ubuntu:

```bash
python exemplo_gui.py
```

---

## 📚 Mais Componentes Possíveis

O DearPyGui tem muitos widgets úteis:

* `add_slider_float()`, `add_checkbox()`
* `add_color_picker()`
* `add_file_dialog()`
* `add_plot()`, `add_table()`
* `add_image()` (pode mostrar imagens com OpenGL)

---

## 🧪 Verificação Rápida

Para confirmar que está a funcionar:

1. Instala o módulo com `pip install dearpygui`
2. Guarda o script acima como `exemplo_gui.py`
3. Corre com `python exemplo_gui.py`
4. Deverás ver uma janela onde podes escrever o nome e clicar para ver a mensagem.

---
