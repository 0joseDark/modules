O módulo `wave` do Python permite **ler e gravar ficheiros de áudio no formato WAV (Waveform Audio File Format)**. Ele faz parte da biblioteca padrão, portanto **não é necessário instalar nada adicional** no Windows 10 ou Ubuntu Linux.

---

## 🔧 Compatibilidade

| Sistema Operativo | Compatível com `wave`? | Pré-instalado?     |
| ----------------- | ---------------------- | ------------------ |
| **Windows 10**    | ✅ Sim                  | ✅ Sim              |
| **Ubuntu Linux**  | ✅ Sim                  | ✅ Sim (com Python) |

---

## 📚 O que o módulo `wave` pode fazer?

### Leitura:

* Abrir ficheiros `.wav`
* Obter dados: número de canais, taxa de amostragem, número de frames, etc.
* Ler o áudio como bytes

### Escrita:

* Criar novos ficheiros `.wav`
* Definir canais, taxa de amostragem, número de bits
* Escrever os frames de áudio

---

## 🔍 Estrutura básica

```python
import wave

# Abrir um ficheiro WAV para leitura
with wave.open("exemplo.wav", 'rb') as wav:
    params = wav.getparams()      # Obter parâmetros do ficheiro
    frames = wav.readframes(wav.getnframes())  # Ler todos os frames

# Criar um novo ficheiro WAV e escrever frames
with wave.open("saida.wav", 'wb') as wav_out:
    wav_out.setparams(params)     # Definir os mesmos parâmetros
    wav_out.writeframes(frames)   # Escrever os frames copiados
```

---

## 🧪 Exemplo completo: Gerar um som senoidal e gravar em WAV

Vamos gerar um som de 1 segundo com 440 Hz (nota musical **Lá**), e gravar num ficheiro `.wav`.

### ✅ Funciona em Windows 10 e Ubuntu

```python
import wave
import struct
import math

# Parâmetros do áudio
canal = 1                 # Mono
taxa_amostragem = 44100   # 44.1 kHz
duração = 1.0             # 1 segundo
frequência = 440.0        # Frequência da onda senoidal (A4)
amplitude = 32767         # Máxima amplitude para 16-bit

# Gerar os samples
n_frames = int(taxa_amostragem * duração)
frames = []

for i in range(n_frames):
    t = float(i) / taxa_amostragem
    valor = int(amplitude * math.sin(2 * math.pi * frequência * t))
    frames.append(struct.pack('<h', valor))  # '<h' = 16-bit little-endian

# Juntar os frames num único bloco
frames_bytes = b''.join(frames)

# Criar e gravar o ficheiro WAV
with wave.open("onda_seno.wav", 'wb') as ficheiro:
    ficheiro.setnchannels(canal)
    ficheiro.setsampwidth(2)  # 2 bytes = 16 bits
    ficheiro.setframerate(taxa_amostragem)
    ficheiro.writeframes(frames_bytes)

print("Ficheiro WAV gerado com sucesso: onda_seno.wav")
```

---

## 📁 Onde fica o ficheiro?

O ficheiro `onda_seno.wav` será gravado na **mesma pasta** onde o script Python for executado.

---

## 🛠️ Extras para verificar

* No **Windows**, podes clicar com o botão direito no ficheiro `.wav` > **Abrir com > Windows Media Player**
* No **Ubuntu**, usa `VLC`, `Audacity`, ou executa:

  ```bash
  aplay onda_seno.wav
  ```

---

## 🔄 Dicas e Expansões

* Para ler o som e mostrar gráfico: usar `matplotlib` e `numpy`
* Para gravar som do microfone: usar `pyaudio` ou `sounddevice`
* Para converter para MP3: usar `pydub` + `ffmpeg`

---
