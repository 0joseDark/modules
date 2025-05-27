O módulo `pyalsaaudio` é um **wrapper Python para a API ALSA (Advanced Linux Sound Architecture)**, que fornece controle de som em sistemas Linux, como o Ubuntu. Ele **não é compatível com o Windows**, pois o ALSA só está disponível no Linux. Para o Windows, seria necessário usar bibliotecas como `pyaudio`, `sounddevice`, ou `winsound`.

---

## ✅ Resumo:

* **Ubuntu/Linux:** `pyalsaaudio` funciona bem.
* **Windows 10:** `pyalsaaudio` **não funciona** (ALSA não existe no Windows).

---

## ✅ Instalar `pyalsaaudio` no Ubuntu

No terminal:

```bash
sudo apt update
sudo apt install python3-pip libasound2-dev
pip3 install pyalsaaudio
```

---

## ✅ O que o `pyalsaaudio` pode fazer:

* Gravar som
* Tocar som (áudio PCM)
* Controlar volumes e dispositivos
* Listar placas de som e mixers

---

## ✅ Exemplo Completo (Gravar e Reproduzir áudio PCM no Ubuntu)

Este exemplo:

1. Grava 5 segundos de som do microfone.
2. Reproduz o som capturado nas colunas.

```python
import alsaaudio
import time
import wave

# 1. Configurar captura de áudio (microfone)
input_device = alsaaudio.PCM(alsaaudio.PCM_CAPTURE, alsaaudio.PCM_NONBLOCK)
input_device.setchannels(1)
input_device.setrate(44100)
input_device.setformat(alsaaudio.PCM_FORMAT_S16_LE)
input_device.setperiodsize(1024)

# 2. Gravar som durante 5 segundos
print("A gravar durante 5 segundos...")
frames = []
start = time.time()

while time.time() - start < 5:
    length, data = input_device.read()
    if length:
        frames.append(data)
    time.sleep(0.01)

# 3. Guardar som num ficheiro WAV
with wave.open("gravacao.wav", 'wb') as wf:
    wf.setnchannels(1)
    wf.setsampwidth(2)  # 16-bit -> 2 bytes
    wf.setframerate(44100)
    wf.writeframes(b''.join(frames))

print("Gravação terminada e guardada em 'gravacao.wav'.")

# 4. Reproduzir o som gravado
output_device = alsaaudio.PCM(alsaaudio.PCM_PLAYBACK)
output_device.setchannels(1)
output_device.setrate(44100)
output_device.setformat(alsaaudio.PCM_FORMAT_S16_LE)
output_device.setperiodsize(1024)

print("A reproduzir som...")

with wave.open("gravacao.wav", 'rb') as wf:
    data = wf.readframes(1024)
    while data:
        output_device.write(data)
        data = wf.readframes(1024)

print("Reprodução terminada.")
```

---

## ✅ Explicação Passo a Passo

| Passo | Ação                               | Detalhes                                           |
| ----- | ---------------------------------- | -------------------------------------------------- |
| 1     | Cria o dispositivo de **captura**  | `alsaaudio.PCM_CAPTURE` usa o microfone            |
| 2     | Define parâmetros                  | Mono (1 canal), 44100 Hz, 16 bits                  |
| 3     | Grava som                          | Lê pacotes pequenos e guarda na lista `frames`     |
| 4     | Guarda em ficheiro `.wav`          | Usa módulo `wave` (compatível com players normais) |
| 5     | Cria dispositivo de **reprodução** | `alsaaudio.PCM_PLAYBACK` usa as colunas            |
| 6     | Lê o ficheiro `.wav`               | Reproduz o áudio diretamente                       |

---

## ❌ Se quiser correr no Windows 10

Use `pyaudio` (funciona em Windows e Linux):

```bash
pip install pyaudio
```

Se quiser, posso mostrar o **mesmo exemplo com `pyaudio` para Windows**.

---

## ✅ Listar dispositivos e mixers disponíveis

```python
import alsaaudio

# Dispositivos de PCM
print("Dispositivos PCM:")
print(alsaaudio.pcms())

# Mixers disponíveis
print("\nMixers disponíveis:")
print(alsaaudio.mixers())
```

---

Se desejar, posso:

* Adaptar o código para Windows com `pyaudio`.
* Mostrar como gravar diretamente para MP3 ou OGG.
* Mostrar uma interface gráfica com PyQt5 ou Tkinter.
