- [**voltar**](https://github.com/0joseDark/modules/blob/main/README.md)
---
O módulo `customtkinter` é uma biblioteca que **estende o módulo padrão `tkinter`**, oferecendo uma aparência **moderna e personalizável (estilo Material Design ou Windows 11)** para aplicações gráficas (GUI). Ele facilita a criação de interfaces mais bonitas e profissionais, mantendo a simplicidade da programação com `tkinter`.

---

### ✅ Vantagens do `customtkinter`:

* Estilo moderno (dark/light mode automático).
* Suporte a temas personalizados.
* Widgets atualizados (botões, sliders, entradas, etc.).
* Fácil integração com `tkinter` tradicional.
* Cross-platform (Windows, macOS, Linux).

---

### 📦 Instalação:

```bash
pip install customtkinter
```
Claro! Aqui tens um exemplo completo de uma **interface gráfica em `customtkinter`** para Windows 10, com:

* **Janela principal moderna**
* **Menu superior com opções**
* **Botões com comandos**
* **Campo de entrada**
* **Caixa de texto**
* **Modo claro/escuro alternável**

---

### ✅ Código completo com comentários passo a passo:

```python
import customtkinter as ctk
import tkinter as tk  # ainda usamos para o menu

# Configuração inicial
ctk.set_appearance_mode("system")  # pode ser: "light", "dark", "system"
ctk.set_default_color_theme("blue")  # pode ser: "blue", "green", "dark-blue"

# Criar a janela principal
janela = ctk.CTk()
janela.title("Interface Completa com customtkinter")
janela.geometry("600x400")

# === FUNÇÕES ===
def mudar_modo():
    if ctk.get_appearance_mode() == "Light":
        ctk.set_appearance_mode("dark")
    else:
        ctk.set_appearance_mode("light")

def mostrar_texto():
    texto = entrada.get()
    caixa_texto.insert("end", f"Digitado: {texto}\n")

def limpar_texto():
    caixa_texto.delete("1.0", "end")

def sair():
    janela.destroy()

# === MENU ===
barra_menu = tk.Menu(janela)
menu_arquivo = tk.Menu(barra_menu, tearoff=0)
menu_arquivo.add_command(label="Mostrar texto", command=mostrar_texto)
menu_arquivo.add_command(label="Limpar", command=limpar_texto)
menu_arquivo.add_separator()
menu_arquivo.add_command(label="Sair", command=sair)

menu_opcoes = tk.Menu(barra_menu, tearoff=0)
menu_opcoes.add_command(label="Mudar Modo", command=mudar_modo)

barra_menu.add_cascade(label="Arquivo", menu=menu_arquivo)
barra_menu.add_cascade(label="Opções", menu=menu_opcoes)
janela.config(menu=barra_menu)

# === WIDGETS ===

# Campo de entrada
entrada = ctk.CTkEntry(janela, placeholder_text="Escreve aqui...")
entrada.pack(pady=10, padx=20)

# Botões
frame_botoes = ctk.CTkFrame(janela)
frame_botoes.pack(pady=10)

btn_mostrar = ctk.CTkButton(frame_botoes, text="Mostrar", command=mostrar_texto)
btn_mostrar.grid(row=0, column=0, padx=10)

btn_limpar = ctk.CTkButton(frame_botoes, text="Limpar", command=limpar_texto)
btn_limpar.grid(row=0, column=1, padx=10)

btn_sair = ctk.CTkButton(frame_botoes, text="Sair", command=sair)
btn_sair.grid(row=0, column=2, padx=10)

# Caixa de texto para saída
caixa_texto = ctk.CTkTextbox(janela, width=500, height=200)
caixa_texto.pack(pady=10)

# Iniciar janela
janela.mainloop()
```

---

### 🖼️ Interface terá:

* Campo para digitar
* Três botões:

  * **Mostrar**: mostra o que foi digitado
  * **Limpar**: limpa a caixa de texto
  * **Sair**: fecha a aplicação
* Menu superior com:

  * **Arquivo**: mostrar, limpar, sair
  * **Opções**: mudar entre modo escuro e claro

---

### 📦 Requisitos:

```bash
pip install customtkinter
```
---

### 🧱 Exemplo simples de uso:

```python
import customtkinter as ctk

# Define o tema e aparência
ctk.set_appearance_mode("dark")  # opções: "light", "dark", "system"
ctk.set_default_color_theme("blue")  # temas: "blue", "green", "dark-blue"

# Criação da janela
janela = ctk.CTk()  # usa CTk em vez de Tk
janela.title("Exemplo com customtkinter")
janela.geometry("400x300")

# Adiciona um botão
botao = ctk.CTkButton(master=janela, text="Clique aqui", command=lambda: print("Botão clicado!"))
botao.pack(pady=20)

# Adiciona uma entrada de texto
entrada = ctk.CTkEntry(master=janela, placeholder_text="Digite algo...")
entrada.pack(pady=10)

# Inicia o loop da interface
janela.mainloop()
```

---

### 🎛️ Alguns widgets disponíveis:

| Widget          | Descrição                    |
| --------------- | ---------------------------- |
| `CTk`           | Janela principal             |
| `CTkButton`     | Botão                        |
| `CTkLabel`      | Texto/etiqueta               |
| `CTkEntry`      | Campo de texto               |
| `CTkTextbox`    | Caixa de texto grande        |
| `CTkSlider`     | Deslizador                   |
| `CTkCheckBox`   | Caixa de seleção             |
| `CTkOptionMenu` | Menu de opções               |
| `CTkFrame`      | Moldura para agrupar widgets |
| `CTkTabview`    | Separadores (tabs)           |

---

### 🌗 Modo Escuro e Temas:

```python
ctk.set_appearance_mode("dark")  # "light", "dark", "system"
ctk.set_default_color_theme("green")  # "blue", "green", "dark-blue"
```

Você pode também criar **temas personalizados** com ficheiros `.json`.

---

### 📌 Dica:

`customtkinter` é ideal para quem quer manter a simplicidade de `tkinter` mas precisa de **um design mais atual e agradável ao utilizador.**
---
Exemplo completo de uma **interface gráfica em `customtkinter`** para Windows 10, com:

* **Janela principal moderna**
* **Menu superior com opções**
* **Botões com comandos**
* **Campo de entrada**
* **Caixa de texto**
* **Modo claro/escuro alternável**

---

### ✅ Código completo com comentários passo a passo:

```python
import customtkinter as ctk
import tkinter as tk  # ainda usamos para o menu

# Configuração inicial
ctk.set_appearance_mode("system")  # pode ser: "light", "dark", "system"
ctk.set_default_color_theme("blue")  # pode ser: "blue", "green", "dark-blue"

# Criar a janela principal
janela = ctk.CTk()
janela.title("Interface Completa com customtkinter")
janela.geometry("600x400")

# === FUNÇÕES ===
def mudar_modo():
    if ctk.get_appearance_mode() == "Light":
        ctk.set_appearance_mode("dark")
    else:
        ctk.set_appearance_mode("light")

def mostrar_texto():
    texto = entrada.get()
    caixa_texto.insert("end", f"Digitado: {texto}\n")

def limpar_texto():
    caixa_texto.delete("1.0", "end")

def sair():
    janela.destroy()

# === MENU ===
barra_menu = tk.Menu(janela)
menu_arquivo = tk.Menu(barra_menu, tearoff=0)
menu_arquivo.add_command(label="Mostrar texto", command=mostrar_texto)
menu_arquivo.add_command(label="Limpar", command=limpar_texto)
menu_arquivo.add_separator()
menu_arquivo.add_command(label="Sair", command=sair)

menu_opcoes = tk.Menu(barra_menu, tearoff=0)
menu_opcoes.add_command(label="Mudar Modo", command=mudar_modo)

barra_menu.add_cascade(label="Arquivo", menu=menu_arquivo)
barra_menu.add_cascade(label="Opções", menu=menu_opcoes)
janela.config(menu=barra_menu)

# === WIDGETS ===

# Campo de entrada
entrada = ctk.CTkEntry(janela, placeholder_text="Escreve aqui...")
entrada.pack(pady=10, padx=20)

# Botões
frame_botoes = ctk.CTkFrame(janela)
frame_botoes.pack(pady=10)

btn_mostrar = ctk.CTkButton(frame_botoes, text="Mostrar", command=mostrar_texto)
btn_mostrar.grid(row=0, column=0, padx=10)

btn_limpar = ctk.CTkButton(frame_botoes, text="Limpar", command=limpar_texto)
btn_limpar.grid(row=0, column=1, padx=10)

btn_sair = ctk.CTkButton(frame_botoes, text="Sair", command=sair)
btn_sair.grid(row=0, column=2, padx=10)

# Caixa de texto para saída
caixa_texto = ctk.CTkTextbox(janela, width=500, height=200)
caixa_texto.pack(pady=10)

# Iniciar janela
janela.mainloop()
```

---

### 🖼️ Interface terá:

* Campo para digitar
* Três botões:

  * **Mostrar**: mostra o que foi digitado
  * **Limpar**: limpa a caixa de texto
  * **Sair**: fecha a aplicação
* Menu superior com:

  * **Arquivo**: mostrar, limpar, sair
  * **Opções**: mudar entre modo escuro e claro

---

### 📦 Requisitos:

```bash
pip install customtkinter
```






