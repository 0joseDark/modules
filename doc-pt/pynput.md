O módulo `pynput` em Python permite **controlar e monitorizar o teclado e o rato** em diferentes sistemas operativos, incluindo **Windows 10 e Ubuntu Linux**.

---

## 🔧 Instalação do `pynput`

### 💻 Windows 10 e Ubuntu:

Abrir o terminal (ou PowerShell no Windows) e executar:

```bash
pip install pynput
```

---

## 🎯 Funcionalidades principais do `pynput`:

### **1. Teclado (`pynput.keyboard`)**

* **Monitorar (ouvir)** teclas pressionadas e soltas.
* **Controlar**: escrever texto, pressionar/soltar teclas programaticamente.

### **2. Rato (`pynput.mouse`)**

* **Monitorar (ouvir)** cliques, movimentos e rolagem do rato.
* **Controlar**: mover o cursor, clicar, pressionar e soltar botões, rolar.

---

## ✅ Exemplo completo: Gravar e reproduzir teclado e rato

Este programa:

1. Cria uma janela com botões: `Gravar`, `Parar`, `Reproduzir`, `Sair`.
2. Grava movimentos/cliques do rato e teclas pressionadas.
3. Guarda no ficheiro `log.txt`.
4. Lê o ficheiro e reproduz os eventos.

---

### 📁 Estrutura do ficheiro `main.py`:

```python
import tkinter as tk
from tkinter import messagebox
from pynput import mouse, keyboard
from pynput.mouse import Controller as MouseController
from pynput.keyboard import Controller as KeyboardController, Key
import threading
import time

# Caminho do ficheiro de log
log_file = "log.txt"

# Controladores para reprodução
mouse_controller = MouseController()
keyboard_controller = KeyboardController()

# Variáveis globais
recording = False
events = []

# Funções para gravar rato e teclado
def start_recording():
    global recording, events
    events = []
    recording = True
    label_status.config(text="A gravar...")

    def on_click(x, y, button, pressed):
        if recording:
            events.append(('mouse_click', x, y, button.name, pressed, time.time()))

    def on_move(x, y):
        if recording:
            events.append(('mouse_move', x, y, time.time()))

    def on_scroll(x, y, dx, dy):
        if recording:
            events.append(('mouse_scroll', x, y, dx, dy, time.time()))

    def on_press(key):
        if recording:
            events.append(('key_press', str(key), time.time()))

    def on_release(key):
        if recording:
            events.append(('key_release', str(key), time.time()))

    mouse_listener = mouse.Listener(on_click=on_click, on_move=on_move, on_scroll=on_scroll)
    keyboard_listener = keyboard.Listener(on_press=on_press, on_release=on_release)

    mouse_listener.start()
    keyboard_listener.start()

def stop_recording():
    global recording
    recording = False
    label_status.config(text="Gravação parada.")
    with open(log_file, "w") as f:
        for event in events:
            f.write(str(event) + "\n")

def play_events():
    try:
        with open(log_file, "r") as f:
            lines = f.readlines()
        label_status.config(text="A reproduzir...")
        previous_time = None
        for line in lines:
            event = eval(line.strip())
            if event[0] == 'mouse_move':
                _, x, y, t = event
                if previous_time:
                    time.sleep(t - previous_time)
                mouse_controller.position = (x, y)
                previous_time = t
            elif event[0] == 'mouse_click':
                _, x, y, button, pressed, t = event
                if previous_time:
                    time.sleep(t - previous_time)
                mouse_controller.position = (x, y)
                btn = getattr(mouse.Button, button)
                if pressed:
                    mouse_controller.press(btn)
                else:
                    mouse_controller.release(btn)
                previous_time = t
            elif event[0] == 'mouse_scroll':
                _, x, y, dx, dy, t = event
                if previous_time:
                    time.sleep(t - previous_time)
                mouse_controller.position = (x, y)
                mouse_controller.scroll(dx, dy)
                previous_time = t
            elif event[0] == 'key_press':
                _, key, t = event
                if previous_time:
                    time.sleep(t - previous_time)
                try:
                    keyboard_controller.press(eval(key))
                except:
                    keyboard_controller.press(key.replace("'", ""))
                previous_time = t
            elif event[0] == 'key_release':
                _, key, t = event
                if previous_time:
                    time.sleep(t - previous_time)
                try:
                    keyboard_controller.release(eval(key))
                except:
                    keyboard_controller.release(key.replace("'", ""))
                previous_time = t
        label_status.config(text="Reprodução concluída.")
    except FileNotFoundError:
        messagebox.showerror("Erro", "Nenhuma gravação encontrada.")

# Interface gráfica
janela = tk.Tk()
janela.title("Gravador pynput (Windows/Linux)")
janela.geometry("400x200")

label_status = tk.Label(janela, text="Pronto.", font=("Arial", 12))
label_status.pack(pady=10)

btn_gravar = tk.Button(janela, text="Gravar", command=lambda: threading.Thread(target=start_recording).start())
btn_gravar.pack(pady=5)

btn_parar = tk.Button(janela, text="Parar", command=stop_recording)
btn_parar.pack(pady=5)

btn_reproduzir = tk.Button(janela, text="Reproduzir", command=lambda: threading.Thread(target=play_events).start())
btn_reproduzir.pack(pady=5)

btn_sair = tk.Button(janela, text="Sair", command=janela.quit)
btn_sair.pack(pady=5)

janela.mainloop()
```

---

## 📄 Explicação passo a passo:

| Linha / Secção                        | Explicação                                                        |
| ------------------------------------- | ----------------------------------------------------------------- |
| `pynput.mouse`, `pynput.keyboard`     | Importa os módulos para controlar e ouvir rato e teclado.         |
| `mouse.Listener`, `keyboard.Listener` | Captura eventos como cliques e teclas.                            |
| `Controller()`                        | Permite controlar movimentos, teclas, etc.                        |
| `threading.Thread(...)`               | Executa a gravação ou reprodução em paralelo à interface gráfica. |
| `eval(line)`                          | Converte o texto do ficheiro `log.txt` de volta para tuplos.      |
| `time.sleep(...)`                     | Reproduz o tempo real entre eventos.                              |
| `label_status`                        | Mostra na janela o estado atual.                                  |

---

## 🐧 Compatibilidade:

| Sistema      | Compatível? | Observações                                                         |
| ------------ | ----------- | ------------------------------------------------------------------- |
| Windows 10   | ✅           | Totalmente funcional. Pode precisar de executar como administrador. |
| Ubuntu Linux | ✅           | Funciona normalmente. Se não detetar eventos globais, use `sudo`.   |

---
