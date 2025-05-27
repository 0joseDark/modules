O módulo `ffmpeg-python` é uma interface (wrapper) em Python para o FFmpeg — um poderoso utilitário de linha de comandos para manipulação de áudio e vídeo. Com `ffmpeg-python`, é possível construir comandos FFmpeg usando código Python de forma intuitiva.

---

## ✅ Instalação do FFmpeg e do módulo `ffmpeg-python`

### 📌 No Windows 10:

1. **Instalar o FFmpeg:**

   * Acede a: [https://ffmpeg.org/download.html](https://ffmpeg.org/download.html)
   * Vai para **Windows > gyan.dev** ou **BtbN builds**.
   * Descarrega e extrai o `.zip` (ex: `ffmpeg-release-full.7z`).
   * Copia a pasta `bin` (contém `ffmpeg.exe`) para um local (ex: `C:\ffmpeg\bin`).
   * Adiciona `C:\ffmpeg\bin` ao **Path** do sistema:

     * Painel de Controlo > Sistema > Avançado > Variáveis de Ambiente > "Path" > Editar > Adicionar novo caminho.

2. **Verifica a instalação:**

   ```bash
   ffmpeg -version
   ```

3. **Instalar o módulo `ffmpeg-python`:**

   ```bash
   pip install ffmpeg-python
   ```

---

### 📌 No Ubuntu Linux:

1. **Instalar o FFmpeg:**

   ```bash
   sudo apt update
   sudo apt install ffmpeg
   ```

2. **Verificar se está instalado:**

   ```bash
   ffmpeg -version
   ```

3. **Instalar o módulo `ffmpeg-python`:**

   ```bash
   pip install ffmpeg-python
   ```

---

## 🔧 Exemplo Completo com `ffmpeg-python`

Vamos converter um vídeo `.mp4` para `.avi`, extrair o áudio, e redimensionar o vídeo.

### Estrutura:

* Input: `input.mp4`
* Output vídeo: `output.avi`
* Output áudio: `audio.mp3`
* Output redimensionado: `resized.mp4`

### Código Python:

```python
import ffmpeg

# 1. Converter vídeo MP4 para AVI
ffmpeg.input('input.mp4').output('output.avi').run()

# 2. Extrair apenas o áudio em MP3
ffmpeg.input('input.mp4').output('audio.mp3').run()

# 3. Redimensionar vídeo para 640x360
ffmpeg.input('input.mp4').output('resized.mp4', vf='scale=640:360').run()
```

---

## 🧠 Explicação Passo a Passo

### 1. `import ffmpeg`

Importa o módulo. Usa programação funcional para montar a pipeline do FFmpeg.

### 2. `.input('input.mp4')`

Indica o ficheiro de entrada (pode ser vídeo, áudio, stream, etc).

### 3. `.output('output.avi')`

Define o ficheiro de saída. Aqui, sem parâmetros extras, o FFmpeg decide os codecs com base na extensão.

### 4. `.run()`

Executa o comando gerado como se fosse um comando na linha de comandos.

---

## 🔍 Ver comandos gerados pelo FFmpeg

Para ver o comando FFmpeg real gerado:

```python
print(ffmpeg.input('input.mp4').output('output.avi').compile())
```

Saída:

```bash
['ffmpeg', '-i', 'input.mp4', 'output.avi']
```

---

## ✅ Dica extra: juntar vídeo e áudio

```python
video = ffmpeg.input('video.mp4')
audio = ffmpeg.input('audio.mp3')
ffmpeg.output(video, audio, 'merged_output.mp4').run()
```

---

## 🧰 Outras funcionalidades úteis

* Cortar o vídeo (de 10s até 30s):

```python
ffmpeg.input('input.mp4', ss=10, t=20).output('cut.mp4').run()
```

* Adicionar legenda (srt):

```python
ffmpeg.input('input.mp4').output('output.mp4', vf='subtitles=legenda.srt').run()
```
