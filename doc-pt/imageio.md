O `imageio` é um módulo Python que permite **ler e escrever imagens e vídeos em vários formatos** com uma interface simples e intuitiva.

---

## ✅ 1. Instalação do `imageio`

### 🪟 Windows 10 e 🐧 Ubuntu:

No terminal ou linha de comandos:

```bash
pip install imageio
```

Se quiser suporte para leitura de vídeo (opcional):

```bash
pip install imageio[ffmpeg]
```

---

## ✅ 2. O que o `imageio` pode fazer?

* Ler e escrever **imagens**: JPG, PNG, BMP, TIFF, etc.
* Ler e escrever **vídeos**: MP4, AVI, etc. (com plugins como `ffmpeg`)
* Ler imagens de uma **webcam** (com `imageio-ffmpeg`)
* Suporte a leitura de **formatos científicos** (TIFF multipágina, DICOM, etc.)

---

## ✅ 3. Exemplo Completo: Ler, editar e gravar imagem

### Objetivo:

1. Carregar uma imagem
2. Converter para tons de cinzento
3. Gravar a imagem nova

---

### 🐍 Código completo: `editar_imagem.py`

```python
import imageio.v3 as iio  # API moderna de imageio
import numpy as np
import os

# === Caminho da imagem de entrada e saída ===
imagem_entrada = 'exemplo.jpg'
imagem_saida = 'exemplo_cinza.png'

# === Verifica se o ficheiro existe ===
if not os.path.exists(imagem_entrada):
    print(f"Erro: ficheiro '{imagem_entrada}' não encontrado.")
    exit(1)

# === 1. Ler a imagem ===
imagem = iio.imread(imagem_entrada)
print("Imagem lida com sucesso. Dimensões:", imagem.shape)

# === 2. Converter para tons de cinzento ===
# Fórmula: 0.2989 * R + 0.5870 * G + 0.1140 * B
imagem_cinza = np.dot(imagem[...,:3], [0.2989, 0.5870, 0.1140])
imagem_cinza = imagem_cinza.astype(np.uint8)  # Garantir tipo

# === 3. Gravar a nova imagem ===
iio.imwrite(imagem_saida, imagem_cinza)
print(f"Imagem gravada como '{imagem_saida}' em tons de cinzento.")
```

---

## ✅ 4. Explicação passo a passo:

| Passo                                   | Descrição                                        |
| --------------------------------------- | ------------------------------------------------ |
| `import imageio.v3`                     | Importa a nova API do `imageio` v3, recomendada. |
| `imagem = iio.imread(...)`              | Lê uma imagem do disco. Retorna um array NumPy.  |
| `np.dot(..., [0.2989, 0.5870, 0.1140])` | Aplica a fórmula para converter RGB em cinzento. |
| `imagem_cinza.astype(np.uint8)`         | Converte os valores para inteiros de 0 a 255.    |
| `iio.imwrite(...)`                      | Grava a imagem processada para o disco.          |

---

## ✅ 5. Observações específicas

### 🪟 Windows 10

* Certifica-te que tens o `pip` instalado e atualizado.
* Usa o PowerShell ou CMD para correr os scripts.

### 🐧 Ubuntu

* Instala Python e pip com:

  ```bash
  sudo apt update
  sudo apt install python3 python3-pip
  ```

---

## ✅ 6. Dica: Ver imagem com o sistema operativo

### Em Python:

```python
import webbrowser
webbrowser.open(imagem_saida)  # Abre a imagem com o visualizador padrão
```

---

## ✅ 7. Extras: Ler vídeo e extrair frames (opcional)

```python
reader = iio.imiter("meu_video.mp4")
for i, frame in enumerate(reader):
    iio.imwrite(f"frame_{i:03}.png", frame)
    if i == 9:
        break  # Extrai só 10 frames
```
