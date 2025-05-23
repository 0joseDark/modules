[**voltar**](https://github.com/0joseDark/modules/blob/main/README.md)
---
O `tkinter` é um módulo **nativo do Python** usado para criar **interfaces gráficas (GUI)**. Ele fornece uma forma simples e eficaz de criar janelas, botões, menus, caixas de texto e outros elementos visuais. Funciona tanto no **Windows 10** quanto no **Ubuntu Linux**, com pequenas diferenças na instalação e comportamento visual.

---

## 🪟 **No Windows 10**

### ✔️ Instalação:

O `tkinter` já vem incluído por padrão na instalação do Python para Windows.

### ✅ Verificar se está instalado:

Abra o terminal do Python (cmd ou PowerShell) e digite:

```python
python -m tkinter
```

Se uma janela com o título "Tk" abrir, está instalado corretamente.

---

## 🐧 **No Ubuntu Linux**

### ✔️ Instalação:

Em algumas distribuições, o `tkinter` **não vem instalado por padrão**.

### ✅ Instalar via terminal:

Para Python 3:

```bash
sudo apt update
sudo apt install python3-tk
```

### ✅ Verificar se está instalado:

Digite no terminal:

```bash
python3 -m tkinter
```

Deve abrir uma pequena janela do `tkinter`.

---

## 🧪 Exemplo básico de `tkinter`:

```python
import tkinter as tk

# Criar a janela principal
janela = tk.Tk()
janela.title("Exemplo Tkinter")
janela.geometry("300x200")

# Criar um rótulo (label)
rotulo = tk.Label(janela, text="Olá, Tkinter!", font=("Arial", 16))
rotulo.pack(pady=20)

# Criar um botão
def clicar():
    rotulo.config(text="Botão clicado!")

botao = tk.Button(janela, text="Clica-me", command=clicar)
botao.pack()

# Executar a janela
janela.mainloop()
```

---

## 🧩 Componentes principais de `tkinter`:

| Componente | Função                  |
| ---------- | ----------------------- |
| `Tk()`     | Cria a janela principal |
| `Label`    | Mostra texto ou imagem  |
| `Button`   | Cria um botão clicável  |
| `Entry`    | Caixa de texto (input)  |
| `Text`     | Área de texto maior     |
| `Frame`    | Agrupa elementos        |
| `Canvas`   | Desenho gráfico         |
| `Menu`     | Menu de opções          |

---

## 📌 Dicas:

* No **Windows 10**, o visual dos botões é mais "nativo" ao sistema.
* No **Ubuntu**, pode variar conforme o tema da interface (GNOME, KDE, etc.).
* Funciona da **mesma forma** em ambos os sistemas, o que facilita a portabilidade do código.
