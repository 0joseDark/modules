- [voltar](https://github.com/0joseDark/modules/blob/main/README.md)
### **1. PyPDF2**
O **PyPDF2** é um dos módulos mais populares para manipular PDFs. Ele permite leitura, escrita, fusão e divisão de documentos PDF.

#### Funcionalidades principais:
- Ler texto de PDFs.
- Dividir ou combinar páginas.
- Adicionar senhas a documentos PDF.

#### Exemplo:
```python
from PyPDF2 import PdfReader, PdfWriter

# Ler um PDF
reader = PdfReader("exemplo.pdf")
for page in reader.pages:
    print(page.extract_text())

# Criar um novo PDF com a primeira página
writer = PdfWriter()
writer.add_page(reader.pages[0])
with open("novo_pdf.pdf", "wb") as output:
    writer.write(output)
```

---

### **2. ReportLab**
O **ReportLab** é usado para criar PDFs a partir do zero. Ele é útil para gerar relatórios, faturas ou documentos personalizados.

#### Funcionalidades principais:
- Criar PDFs dinâmicos.
- Adicionar imagens, gráficos e tabelas.

#### Exemplo:
```python
from reportlab.pdfgen import canvas

# Criar um PDF simples
c = canvas.Canvas("documento.pdf")
c.drawString(100, 750, "Olá, Mundo!")
c.save()
```

---

### **3. PyMuPDF (fitz)**
O **PyMuPDF**, também conhecido como `fitz`, é uma biblioteca poderosa para manipulação de PDFs e outros formatos como ePUB.

#### Funcionalidades principais:
- Ler e extrair texto e imagens.
- Pesquisar palavras em PDFs.
- Alterar e anotar documentos.

#### Exemplo:
```python
import fitz

# Abrir um PDF e extrair texto
doc = fitz.open("exemplo.pdf")
for page in doc:
    print(page.get_text())
doc.close()
```

---

### **4. pdfplumber**
O **pdfplumber** é especializado em extração de texto estruturado, tabelas e dados complexos de documentos PDF.

#### Funcionalidades principais:
- Extrair tabelas diretamente.
- Ler PDFs com layout estruturado.

#### Exemplo:
```python
import pdfplumber

with pdfplumber.open("exemplo.pdf") as pdf:
    for page in pdf.pages:
        print(page.extract_text())
```

---

### **5. PDFMiner**
O **PDFMiner** é uma biblioteca avançada para análise de PDFs, permitindo extração detalhada de texto e metadados.

#### Funcionalidades principais:
- Analisar estrutura de texto.
- Suporte para caracteres Unicode.

#### Exemplo:
```python
from pdfminer.high_level import extract_text

# Extrair texto de um PDF
texto = extract_text("exemplo.pdf")
print(texto)
```

---

### **6. FPDF**
O **FPDF** é uma biblioteca leve para criar PDFs simples. É uma alternativa ao ReportLab para tarefas básicas.

#### Funcionalidades principais:
- Criar PDFs rapidamente.
- Adicionar texto, imagens e links.

#### Exemplo:
```python
from fpdf import FPDF

# Criar um PDF simples
pdf = FPDF()
pdf.add_page()
pdf.set_font("Arial", size=12)
pdf.cell(200, 10, txt="Olá, Mundo!", ln=True, align="C")
pdf.output("exemplo.pdf")
```

---

### **Comparação entre Módulos**
| Módulo        | Uso Principal          | Nível de Complexidade |
|---------------|------------------------|------------------------|
| PyPDF2        | Manipulação de PDFs    | Fácil                 |
| ReportLab     | Criação de PDFs        | Médio                 |
| PyMuPDF       | Manipulação avançada   | Médio/Avançado        |
| pdfplumber    | Extração de tabelas    | Fácil                 |
| PDFMiner      | Extração detalhada     | Avançado              |
| FPDF          | Criação de PDFs        | Fácil                 |
