O módulo **Pillow** (também conhecido como **PIL** – Python Imaging Library) é uma biblioteca em Python usada para **abrir, manipular, modificar, salvar e converter imagens**. Ele funciona no **Windows 10**, **Ubuntu Linux**, e outros sistemas.

---

## ✅ Instalação do Pillow

### 🪟 No Windows 10:

1. Abrir o **Prompt de Comando** (cmd).
2. Digitar:

```bash
pip install Pillow
```

### 🐧 No Ubuntu Linux:

1. Abrir o **Terminal**.
2. Digitar:

```bash
sudo apt update
sudo apt install python3-pip
pip3 install Pillow
```

---

## 🧠 O que o Pillow pode fazer?

Com ele, pode-se:

* Abrir e mostrar imagens.
* Redimensionar, cortar, rodar, aplicar filtros.
* Adicionar texto e formas.
* Converter para outros formatos (JPEG, PNG, BMP...).
* Criar novas imagens do zero.

---

## 💡 Exemplo completo com explicações passo a passo

Este script:

* Abre uma imagem.
* Redimensiona.
* Converte para escala de cinza.
* Escreve texto na imagem.
* Salva como novo ficheiro.

---

### 🖼️ Ficheiro de exemplo: `exemplo_pillow.py`

```python
from PIL import Image, ImageDraw, ImageFont, ImageFilter

# 1. Abrir a imagem original
imagem = Image.open("exemplo.jpg")  # Substitua por uma imagem no mesmo diretório
print("Tamanho original:", imagem.size)

# 2. Redimensionar a imagem
nova_imagem = imagem.resize((300, 300))
print("Nova dimensão:", nova_imagem.size)

# 3. Converter para tons de cinzento
imagem_cinza = nova_imagem.convert("L")  # "L" = Luminância (escala de cinza)

# 4. Aplicar um filtro de desfoque
imagem_borrada = imagem_cinza.filter(ImageFilter.GaussianBlur(2))

# 5. Adicionar texto sobre a imagem
desenho = ImageDraw.Draw(imagem_borrada)
# Tenta carregar uma fonte; se falhar, usa a padrão
try:
    fonte = ImageFont.truetype("arial.ttf", 20)  # Windows geralmente tem arial.ttf
except:
    fonte = ImageFont.load_default()

desenho.text((10, 10), "Imagem Editada", fill=255, font=fonte)

# 6. Guardar a imagem final
imagem_borrada.save("imagem_editada.jpg")
print("Imagem guardada como imagem_editada.jpg")
```

---

## 📂 Estrutura de Pastas Sugerida

```
pillow_exemplo/
│
├── exemplo_pillow.py
└── exemplo.jpg  ← (sua imagem de entrada)
```

---

## 🧪 Como correr o script

### Windows:

```bash
python exemplo_pillow.py
```

### Ubuntu:

```bash
python3 exemplo_pillow.py
```

---

## 📌 Dicas

* Para mostrar a imagem numa janela:

```python
imagem.show()  # Abre a imagem com o visualizador padrão
```

* Para criar uma imagem nova do zero:

```python
imagem_nova = Image.new("RGB", (400, 400), color="blue")
imagem_nova.save("nova_imagem.png")
```

---

## 🧰 Formatos suportados

Pillow suporta vários formatos:

* JPEG
* PNG
* BMP
* GIF
* TIFF
* WebP
