O módulo `keyboard` em Python permite controlar e monitorar eventos do **teclado**, como pressionar teclas, ouvir combinações, ou gravar e reproduzir digitações.

---

## ✅ **Instalação do módulo `keyboard`**

### Windows 10 e Ubuntu:

```bash
pip install keyboard
```

> ❗ **No Ubuntu**, o módulo `keyboard` **requer privilégios de superusuário (sudo)** para funcionar corretamente.
> Exemplo:

```bash
sudo python3 meu_script.py
```

---

## 🧠 **Passo a passo das funcionalidades principais**

### 1. **Importar o módulo**

```python
import keyboard
```

---

### 2. **Detectar se uma tecla está pressionada**

```python
keyboard.is_pressed('a')  # Retorna True enquanto a tecla 'a' está pressionada
```

---

### 3. **Esperar uma tecla ser pressionada**

```python
keyboard.wait('esc')  # Espera até que a tecla ESC seja pressionada
```

---

### 4. **Pressionar teclas via script (automatizar digitação)**

```python
keyboard.write("Olá, mundo!")  # Simula digitação
keyboard.press_and_release('enter')  # Pressiona Enter
```

---

### 5. **Registrar eventos do teclado**

```python
eventos = keyboard.record(until='esc')  # Grava até o utilizador carregar em ESC
```

---

### 6. **Reproduzir o que foi gravado**

```python
keyboard.play(eventos)  # Reproduz as teclas gravadas
```

---

### 7. **Adicionar atalho personalizado**

```python
def acao():
    print("CTRL + SHIFT + A foi pressionado!")

keyboard.add_hotkey('ctrl+shift+a', acao)
keyboard.wait('esc')  # Aguarda o utilizador carregar em ESC
```

---

## 💡 Exemplo completo com comentários

```python
# exemplo_keyboard.py
import keyboard
import time

print("Pressiona teclas, o programa vai gravar... (carrega ESC para parar)")

# Grava até pressionar ESC
eventos = keyboard.record(until='esc')

# Mostra o que foi gravado
print("\nEventos gravados:")
for evento in eventos:
    print(f"{evento.name} - {evento.event_type} - {evento.time}")

# Espera 2 segundos antes de reproduzir
print("\nReproduzindo em 2 segundos...")
time.sleep(2)

keyboard.play(eventos, speed_factor=1)

print("Fim.")
```

### 💾 Como executar no Windows:

```bash
python exemplo_keyboard.py
```

### 🐧 Como executar no Ubuntu (com sudo):

```bash
sudo python3 exemplo_keyboard.py
```

---

## 🔐 Permissões no Linux

* No **Ubuntu/Linux**, para aceder ao teclado, o script precisa ser executado como **root (sudo)**.
* Também podes dar permissão à interface `/dev/input` usando regras `udev`, mas `sudo` é mais simples para testes.

---

## ⚠️ Notas importantes

| Plataforma | Notas                             |
| ---------- | --------------------------------- |
| Windows    | Funciona direto, sem privilégios  |
| Ubuntu     | Precisa de `sudo`                 |
| Wayland    | (Gnome novo) pode bloquear acesso |

---
