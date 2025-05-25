O módulo `PyAudio` é uma biblioteca Python que fornece bindings para a **PortAudio**, permitindo **gravação** e **reprodução de áudio** em tempo real em várias plataformas, incluindo **Windows 10** e **Ubuntu**.

---

### ✅ INSTALAÇÃO DO PyAudio

#### **Windows 10:**

1. Primeiro, instale o Python (por exemplo, do site [python.org](https://www.python.org/)).
2. Depois abra o terminal (CMD) e execute:

```bash
pip install pipwin
pipwin install pyaudio
```

> `pipwin` é um instalador alternativo que baixa binários compatíveis com o Windows.

---

#### **Ubuntu Linux:**

1. Primeiro instale as bibliotecas necessárias do sistema:

```bash
sudo apt update
sudo apt install python3-pyaudio portaudio19-dev python3-dev
```

2. Depois instale via `pip`:

```bash
pip install pyaudio
```

---

## 🔍 COMO FUNCIONA O PyAudio

### Componentes principais:

* `pyaudio.PyAudio()` → Inicializa o sistema de áudio.
* `.open()` → Abre um **stream de entrada ou saída** de áudio.
* `.read()` → Lê áudio do microfone.
* `.write()` → Reproduz áudio nos altifalantes.
* `.close()` → Fecha o stream.
* `.terminate()` → Liberta os recursos de áudio.

---

## 🎙️ EXEMPLO COMPLETO: gravar e reproduzir som

Este exemplo faz:

1. Grava **5 segundos** do microfone.
2. Guarda em `.wav`.
3. Reproduz o ficheiro gravado.

### 🔧 Código:

```python
import pyaudio
import wave

# PARÂMETROS DE ÁUDIO
FORMAT = pyaudio.paInt16       # Formato de 16 bits
CHANNELS = 1                   # Mono
RATE = 44100                  # Taxa de amostragem
CHUNK = 1024                  # Tamanho do bloco
DURACAO = 5                   # Segundos
NOME_FICHEIRO = "gravacao.wav"

# INICIAR PyAudio
audio = pyaudio.PyAudio()

# === GRAVAR ===
print("A gravar...")

stream = audio.open(format=FORMAT,
                    channels=CHANNELS,
                    rate=RATE,
                    input=True,
                    frames_per_buffer=CHUNK)

frames = []

for i in range(0, int(RATE / CHUNK * DURACAO)):
    data = stream.read(CHUNK)
    frames.append(data)

print("Gravação terminada.")

stream.stop_stream()
stream.close()

# GUARDAR EM FICHEIRO WAV
with wave.open(NOME_FICHEIRO, 'wb') as wf:
    wf.setnchannels(CHANNELS)
    wf.setsampwidth(audio.get_sample_size(FORMAT))
    wf.setframerate(RATE)
    wf.writeframes(b''.join(frames))

# === REPRODUZIR ===
print("A reproduzir...")

with wave.open(NOME_FICHEIRO, 'rb') as wf:
    stream = audio.open(format=audio.get_format_from_width(wf.getsampwidth()),
                        channels=wf.getnchannels(),
                        rate=wf.getframerate(),
                        output=True)

    data = wf.readframes(CHUNK)

    while data:
        stream.write(data)
        data = wf.readframes(CHUNK)

stream.stop_stream()
stream.close()
audio.terminate()
print("Fim.")
```

---

## 📝 PASSO A PASSO

| Passo | Ação                                                   |
| ----- | ------------------------------------------------------ |
| 1     | Define-se o formato, canais, taxa e chunk.             |
| 2     | Cria-se um objeto PyAudio.                             |
| 3     | Abre-se o microfone para capturar áudio.               |
| 4     | Grava-se áudio durante 5 segundos em blocos (chunks).  |
| 5     | Os dados são guardados em `frames`.                    |
| 6     | Escreve-se um ficheiro `.wav` com os dados capturados. |
| 7     | Abre-se o ficheiro `.wav` para leitura.                |
| 8     | Reproduz-se o ficheiro áudio nos altifalantes.         |
| 9     | Fecha-se tudo e termina-se o processo.                 |

---

## 🔎 DICAS

* Em **Ubuntu**, use `arecord -l` para listar dispositivos de gravação.
* Em **Windows**, use `pyaudio.get_device_info_by_index()` para listar microfones.
* Pode-se capturar áudio estéreo com `channels=2`.

---
