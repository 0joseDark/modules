O módulo `sounddevice` em Python é uma biblioteca poderosa e fácil de usar para **gravação e reprodução de áudio** em tempo real. Funciona tanto no **Windows 10** como no **Ubuntu Linux**, utilizando como backend o **PortAudio**.

---

## ✅ **Instalação no Windows 10 e Ubuntu**

### 📦 Instalar via `pip`:

```bash
pip install sounddevice
```

> ⚠️ No **Ubuntu**, pode ser necessário instalar dependências do PortAudio:

```bash
sudo apt update
sudo apt install libportaudio2
```

---

## 🎧 **Explicação passo a passo das funções principais**

### `sounddevice.query_devices()`

* Lista todos os dispositivos de entrada/saída disponíveis (microfones, colunas, etc).

### `sounddevice.default.device`

* Define os dispositivos padrão para entrada e saída.

### `sounddevice.rec()`

* Grava áudio por um tempo determinado (em segundos).

### `sounddevice.play()`

* Reproduz um array de áudio (por exemplo, o que foi gravado).

### `sounddevice.wait()`

* Aguarda o término de uma operação de gravação ou reprodução.

---

## 🧪 Exemplo completo: Gravar e reproduzir áudio

Este exemplo funciona tanto no **Windows 10** quanto no **Ubuntu Linux**.

```python
import sounddevice as sd
import numpy as np
import scipy.io.wavfile as wav
import os

# Configurações
duracao = 5  # duração da gravação em segundos
frequencia_amostragem = 44100  # frequência de amostragem em Hz

print("Dispositivos disponíveis:")
print(sd.query_devices())

# Define o dispositivo padrão (opcional)
# sd.default.device = (entrada, saída)

print(f"\nA gravar durante {duracao} segundos...")

# Grava som (1 canal: mono; dtype='int16' para WAV compatível)
gravacao = sd.rec(int(duracao * frequencia_amostragem), samplerate=frequencia_amostragem, channels=1, dtype='int16')
sd.wait()  # Aguarda fim da gravação

# Guarda num ficheiro WAV
ficheiro_som = "gravacao.wav"
wav.write(ficheiro_som, frequencia_amostragem, gravacao)
print(f"\nGravação guardada em: {ficheiro_som}")

# Reproduz o som gravado
print("A reproduzir a gravação...")
sd.play(gravacao, frequencia_amostragem)
sd.wait()

print("Fim da reprodução.")
```

---

## 📝 Explicação linha por linha:

1. **Importação dos módulos**:

   * `sounddevice`: para gravar e reproduzir áudio.
   * `numpy`: necessário porque `sounddevice` utiliza arrays NumPy.
   * `scipy.io.wavfile`: para salvar o ficheiro `.wav`.
   * `os`: opcional, para manipular ficheiros.

2. **Configurações básicas**:

   * `duracao` define o tempo da gravação.
   * `frequencia_amostragem` define a qualidade do som.

3. **Gravação**:

   * `sd.rec()` inicia a gravação.
   * `sd.wait()` garante que termina antes de avançar.

4. **Salvar áudio**:

   * `wav.write()` escreve num ficheiro `.wav`.

5. **Reprodução**:

   * `sd.play()` toca o som gravado.

---

## 🔍 Dica: Ver dispositivos disponíveis

Use isto para ver microfones, colunas, etc:

```python
print(sd.query_devices())
```

---

## 🛠 Solução de problemas

| Erro comum         | Solução                                            |
| ------------------ | -------------------------------------------------- |
| `PortAudioError`   | Verifique se o microfone está ligado e funcionando |
| Som muito baixo    | Verifique o volume do microfone                    |
| Nada é reproduzido | Verifique o dispositivo de saída                   |

---
