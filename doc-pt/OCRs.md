## **1. Tesseract OCR**

### **Descrição**
Tesseract é um mecanismo de OCR desenvolvido originalmente pela HP e agora mantido pelo Google. Ele suporta várias línguas e pode ser usado para extrair texto de imagens.

### **Instalação**
1. Instale o Tesseract no sistema operacional:
   - Windows: Baixe e instale [Tesseract OCR](https://github.com/tesseract-ocr/tesseract).
   - Linux: `sudo apt install tesseract-ocr`.
2. Instale o wrapper Python:
   ```bash
   pip install pytesseract
   ```

### **Exemplo**
```python
import pytesseract
from PIL import Image

# Configurar o caminho do executável do Tesseract (no Windows)
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"

# Carregar uma imagem
image_path = "exemplo.png"
image = Image.open(image_path)

# Extrair texto
texto = pytesseract.image_to_string(image, lang="por")
print("Texto extraído:")
print(texto)
```

---

## **2. Textract**

### **Descrição**
Textract é uma biblioteca que oferece suporte a OCR e leitura de documentos, como PDFs, Word e PowerPoint. Ele automatiza a extração de texto de vários formatos de arquivo.

### **Instalação**
```bash
pip install textract
```

> **Nota:** Textract exige a instalação de programas externos como `pdftotext` e `tesseract`. Certifique-se de que eles estão instalados.

### **Exemplo**
```python
import textract

# Carregar um documento (PDF, imagem, ou outro formato suportado)
arquivo = "documento.pdf"

# Extrair texto
texto = textract.process(arquivo, encoding="utf-8")
print("Texto extraído:")
print(texto.decode("utf-8"))
```

---

## **3. EasyOCR**

### **Descrição**
EasyOCR é uma biblioteca Python simples para OCR que suporta mais de 80 línguas, incluindo português. É baseada em redes neurais treinadas.

### **Instalação**
```bash
pip install easyocr
```

### **Exemplo**
```python
import easyocr

# Criar leitor
leitor = easyocr.Reader(["pt"], gpu=False)  # 'gpu=True' se tiver CUDA instalada

# Carregar uma imagem
image_path = "exemplo.png"

# Extrair texto
resultado = leitor.readtext(image_path)
print("Texto extraído:")
for detecao in resultado:
    print(detecao[1])  # O texto detectado
```

---

## **4. OCRmyPDF**

### **Descrição**
OCRmyPDF é uma ferramenta especializada para adicionar uma camada de texto pesquisável em PDFs, permitindo que sejam indexados ou pesquisados.

### **Instalação**
1. Instale o OCRmyPDF:
   ```bash
   pip install ocrmypdf
   ```
2. Certifique-se de que o Tesseract está instalado no sistema.

### **Exemplo**
```python
import os
from ocrmypdf import ocr

# Caminhos do PDF de entrada e saída
pdf_entrada = "arquivo_scaneado.pdf"
pdf_saida = "arquivo_com_ocr.pdf"

# Aplicar OCR
ocr(pdf_entrada, pdf_saida, language="por")

print(f"O OCR foi aplicado com sucesso no PDF. O arquivo está salvo em: {pdf_saida}")
```

---

## **Resumo Comparativo**
| Módulo       | Uso Principal                          | Requisitos Adicionais                  |
|--------------|----------------------------------------|----------------------------------------|
| Tesseract    | Extração básica de texto de imagens    | Tesseract instalado                   |
| Textract     | Extração de texto de vários formatos   | Programas adicionais como Tesseract   |
| EasyOCR      | OCR simples e eficiente com redes NN   | GPU opcional                          |
| OCRmyPDF     | OCR para PDFs com camada pesquisável   | Tesseract instalado                   |
