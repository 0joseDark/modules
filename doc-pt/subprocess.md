[voltar](https://github.com/0joseDark/modules/blob/main/README.md)
- O módulo `subprocess` do Python permite **executar comandos do sistema operativo** (como se estivesse no terminal ou linha de comandos) e **interagir com os processos externos**: ler a saída, enviar entrada, tratar erros, etc.

Funciona tanto no **Windows 10** como no **Ubuntu Linux** — embora os **comandos que passamos possam variar** (por exemplo, `dir` no Windows e `ls` no Linux).

---

## 🔧 Importação

```python
import subprocess
```

---

## 🔍 Explicação Passo a Passo

### 1. **Executar um comando simples**

```python
subprocess.run(["comando", "argumentos"])
```

* Executa um comando externo.
* Espera até terminar.
* Retorna um objeto `CompletedProcess`.

---

### 2. **Capturar a saída do comando**

```python
subprocess.run(["comando"], capture_output=True, text=True)
```

* `capture_output=True` → guarda o `stdout` e o `stderr`.
* `text=True` → a saída será uma string (em vez de `bytes`).

---

### 3. **Lidar com erros**

```python
subprocess.run(["comando"], check=True)
```

* `check=True` → se o comando der erro, levanta uma exceção `CalledProcessError`.

---

### 4. **Executar com entrada personalizada**

```python
subprocess.run(["comando"], input="texto", text=True)
```

---

### 5. **Exemplo Completo com Compatibilidade para Windows e Ubuntu**

```python
import subprocess
import platform

# Verificar sistema operativo
so = platform.system()
print(f"Sistema operativo: {so}")

# Comando adaptado
if so == "Windows":
    comando = ["cmd", "/c", "dir"]  # "/c" executa o comando e sai
else:
    comando = ["ls", "-l"]

try:
    resultado = subprocess.run(
        comando,
        capture_output=True,  # Captura stdout e stderr
        text=True,            # Interpreta como string (em vez de bytes)
        check=True            # Levanta erro se o comando falhar
    )

    print("=== Saída ===")
    print(resultado.stdout)
    
    if resultado.stderr:
        print("=== Erros ===")
        print(resultado.stderr)

except subprocess.CalledProcessError as erro:
    print("O comando falhou:")
    print(erro)

except FileNotFoundError:
    print("O comando não foi encontrado.")

```

---

## 🧪 Testes em:

### 🪟 Windows 10:

```bash
cmd /c dir
```

### 🐧 Ubuntu:

```bash
ls -l
```

---

## 🔁 Alternativa com `subprocess.Popen` (mais controlo)

```python
p = subprocess.Popen(["ping", "google.com"],
                     stdout=subprocess.PIPE,
                     stderr=subprocess.PIPE,
                     text=True)

out, err = p.communicate()
print("Saída:", out)
print("Erros:", err)
```

---

## 📚 Resumo

| Função                | Uso Principal                      |
| --------------------- | ---------------------------------- |
| `run()`               | Executa comando e espera fim       |
| `Popen()`             | Mais controlo, pode ser assíncrono |
| `capture_output=True` | Guarda stdout/stderr               |
| `check=True`          | Lança exceção se comando falhar    |
| `text=True`           | Trata entrada/saída como texto     |

---
**programa com interface gráfica (janela)** em Python que permite:

### ✅ Funcionalidades:

* Escolher um comando do sistema (Windows ou Ubuntu).
* Executar o comando com `subprocess`.
* Ver a **saída** e os **erros** numa área de texto.
* Botões: `Executar`, `Limpar`, `Sair`.

---

## 🖼️ Resultado visual (Tkinter):

* Caixa de entrada para o comando.
* Área de texto para mostrar o resultado.
* Botões abaixo da área de texto.

---

## 🐍 Código Completo com Comentários

```python
import subprocess
import platform
import tkinter as tk
from tkinter import messagebox, scrolledtext

# Função que executa o comando
def executar_comando():
    comando = entrada_comando.get()
    if not comando:
        messagebox.showwarning("Aviso", "Introduza um comando.")
        return

    # Detectar sistema operativo
    sistema = platform.system()

    # Preparar o comando conforme o SO
    if sistema == "Windows":
        cmd = ["cmd", "/c", comando]
    else:
        cmd = comando.split()  # separa o comando em lista para Linux/macOS

    try:
        resultado = subprocess.run(
            cmd,
            capture_output=True,
            text=True,
            check=True
        )

        texto_saida.delete(1.0, tk.END)
        texto_saida.insert(tk.END, "=== Saída ===\n")
        texto_saida.insert(tk.END, resultado.stdout)

        if resultado.stderr:
            texto_saida.insert(tk.END, "\n=== Erros ===\n")
            texto_saida.insert(tk.END, resultado.stderr)

    except subprocess.CalledProcessError as erro:
        texto_saida.delete(1.0, tk.END)
        texto_saida.insert(tk.END, "O comando falhou:\n")
        texto_saida.insert(tk.END, erro.stderr)

    except FileNotFoundError:
        texto_saida.delete(1.0, tk.END)
        texto_saida.insert(tk.END, "O comando não foi encontrado.")

# Função para limpar a área de texto
def limpar():
    texto_saida.delete(1.0, tk.END)
    entrada_comando.delete(0, tk.END)

# Função para sair do programa
def sair():
    janela.destroy()

# Criação da janela principal
janela = tk.Tk()
janela.title("Executar Comando com subprocess")
janela.geometry("600x400")
janela.resizable(False, False)

# Label e entrada do comando
tk.Label(janela, text="Comando do sistema:").pack(pady=5)
entrada_comando = tk.Entry(janela, width=60)
entrada_comando.pack(pady=5)

# Área de texto com scroll
texto_saida = scrolledtext.ScrolledText(janela, width=70, height=15)
texto_saida.pack(pady=10)

# Botões
frame_botoes = tk.Frame(janela)
frame_botoes.pack()

tk.Button(frame_botoes, text="Executar", command=executar_comando, width=15).grid(row=0, column=0, padx=5)
tk.Button(frame_botoes, text="Limpar", command=limpar, width=15).grid(row=0, column=1, padx=5)
tk.Button(frame_botoes, text="Sair", command=sair, width=15).grid(row=0, column=2, padx=5)

# Iniciar janela
janela.mainloop()
```

---

## 💡 Exemplos de Comandos a Testar

### 🪟 Windows 10:

* `dir`
* `ipconfig`
* `echo Olá Mundo`

### 🐧 Ubuntu/Linux:

* `ls -l`
* `ifconfig` ou `ip a`
* `echo "Olá Mundo"`

---

## 📦 Requisitos

* Funciona com Python 3.
* Não precisa de instalar módulos extra (Tkinter e subprocess são padrão).

---

