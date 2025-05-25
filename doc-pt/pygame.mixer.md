O módulo `pygame.mixer` do Pygame é usado para **carregar e reproduzir sons**. Funciona tanto no **Windows 10** como no **Ubuntu**, desde que o Pygame esteja corretamente instalado. A seguir, explico passo a passo como usar `pygame.mixer`, com um **exemplo completo comentado**.

---

## ✅ 1. Instalar o Pygame

No **Windows 10** ou **Ubuntu**, podes instalar o Pygame com:

```bash
pip install pygame
```

No Ubuntu, também pode ser necessário instalar bibliotecas de som:

```bash
sudo apt install libsdl2-mixer-2.0-0
```

---

## ✅ 2. Estrutura do módulo `pygame.mixer`

### Importar:

```python
import pygame
```

### Iniciar o sistema de som:

```python
pygame.mixer.init()
```

### Carregar som:

```python
som = pygame.mixer.Sound('ficheiro.wav')
```

### Reproduzir:

```python
som.play()
```

### Parar:

```python
som.stop()
```

### Controlar volume:

```python
som.set_volume(0.5)  # De 0.0 (mudo) até 1.0 (volume máximo)
```

---

## ✅ 3. Exemplo completo com interface em Python (Tkinter + Pygame)

Este exemplo cria uma pequena janela com botões para **tocar**, **parar** e **ajustar volume** de um som `.wav`.

### 🎵 Cria um ficheiro chamado `exemplo_mixer.py`:

```python
import pygame
import tkinter as tk
from tkinter import filedialog

# Inicializar pygame.mixer
pygame.mixer.init()

# Funções
def carregar_som():
    caminho = filedialog.askopenfilename(filetypes=[("Ficheiros WAV", "*.wav")])
    if caminho:
        global som
        som = pygame.mixer.Sound(caminho)
        label_nome.config(text="Som carregado: " + caminho.split("/")[-1])

def tocar():
    if som:
        som.play()

def parar():
    if som:
        som.stop()

def volume(val):
    if som:
        som.set_volume(float(val))

# Criar interface gráfica
janela = tk.Tk()
janela.title("Exemplo Pygame Mixer")
janela.geometry("400x200")

# Widgets
btn_carregar = tk.Button(janela, text="Carregar Som", command=carregar_som)
btn_carregar.pack(pady=10)

btn_tocar = tk.Button(janela, text="Tocar", command=tocar)
btn_tocar.pack(pady=5)

btn_parar = tk.Button(janela, text="Parar", command=parar)
btn_parar.pack(pady=5)

slider_volume = tk.Scale(janela, from_=0, to=1, resolution=0.1,
                         orient='horizontal', label="Volume", command=volume)
slider_volume.set(1.0)
slider_volume.pack(pady=10)

label_nome = tk.Label(janela, text="Nenhum som carregado")
label_nome.pack()

som = None  # Variável global para armazenar o som

janela.mainloop()
```

---

## ✅ 4. Como usar

1. **Corre o script**:

   ```bash
   python exemplo_mixer.py
   ```
2. **Carrega um ficheiro `.wav`** (formato suportado por `pygame.mixer.Sound`).
3. Usa os botões para **tocar**, **parar** e ajustar o **volume**.

---

## 🛠️ Observações:

* O `pygame.mixer` suporta **WAV**, **OGG**, e eventualmente **MP3** (se o SDL\_mixer suportar).
* O módulo `pygame.mixer.music` também existe para **ficheiros longos**, como MP3s grandes (streaming).

---

## ✅ Dica extra: Usar `pygame.mixer.music` (para MP3)

```python
pygame.mixer.music.load('musica.mp3')
pygame.mixer.music.play()
pygame.mixer.music.set_volume(0.5)
```

---
