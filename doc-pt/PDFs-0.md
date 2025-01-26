### Módulos para Trabalhar com PDFs em Python

Aqui está uma explicação e exemplos práticos para cada módulo mencionado:

---

## 1. **Camelot**

### Descrição
O Camelot é uma biblioteca Python para extrair tabelas de PDFs que estejam bem formatadas. Ele suporta duas abordagens: **stream** (baseado em fluxo de texto) e **lattice** (baseado em estruturas de linhas).

### Instalação
```bash
pip install camelot-py[cv]
```

### Exemplo
```python
import camelot

# Carregar o PDF e extrair tabelas
tables = camelot.read_pdf("example.pdf", pages="1", flavor="stream")

# Exibir o número de tabelas encontradas
print(f"Número de tabelas encontradas: {len(tables)}")

# Salvar a primeira tabela como CSV
tables[0].to_csv("tabela1.csv")

# Exibir a tabela como DataFrame
print(tables[0].df)
```

### Explicação
- **`flavor="stream"`**: Ideal para tabelas baseadas em texto alinhado.
- **`flavor="lattice"`**: Recomendado para tabelas com bordas visíveis.

---

## 2. **PDFPlumber**

### Descrição
O PDFPlumber é uma biblioteca poderosa que permite acessar não apenas tabelas, mas também texto, imagens e a estrutura completa de PDFs.

### Instalação
```bash
pip install pdfplumber
```

### Exemplo
```python
import pdfplumber

# Abrir o PDF
with pdfplumber.open("example.pdf") as pdf:
    # Acessar uma página específica
    page = pdf.pages[0]
    
    # Extrair texto
    texto = page.extract_text()
    print("Texto extraído:")
    print(texto)
    
    # Extrair tabelas
    tabelas = page.extract_tables()
    print("Tabelas encontradas:")
    for tabela in tabelas:
        for linha in tabela:
            print(linha)
```

### Explicação
- **`extract_text`**: Extrai texto da página.
- **`extract_tables`**: Retorna tabelas como listas de listas.

---

## 3. **Tabula-py**

### Descrição
O Tabula-py é uma interface Python para o Tabula, uma ferramenta baseada em Java que também extrai tabelas de PDFs.

### Requisitos
- Java instalado.

### Instalação
```bash
pip install tabula-py
```

### Exemplo
```python
from tabula import read_pdf
from tabula import convert_into

# Ler tabelas de um PDF
tabelas = read_pdf("example.pdf", pages="1", multiple_tables=True)

# Exibir a primeira tabela
print(tabelas[0])

# Converter todas as tabelas para CSV
convert_into("example.pdf", "tabelas.csv", output_format="csv", pages="1")
```

### Explicação
- **`read_pdf`**: Lê tabelas e as retorna como DataFrames do pandas.
- **`convert_into`**: Exporta tabelas para formatos como CSV e Excel.

---

## 4. **pdf2image**

### Descrição
O pdf2image converte páginas de PDFs para imagens, tornando possível trabalhar com PDFs como se fossem imagens.

### Instalação
```bash
pip install pdf2image
```

### Dependências
- Instale o **Poppler**:
  - Windows: Baixe do [site oficial do Poppler](https://github.com/oschwartz10612/poppler-windows).
  - Linux/Mac: Use o gerenciador de pacotes (`apt install poppler-utils` ou `brew install poppler`).

### Exemplo
```python
from pdf2image import convert_from_path

# Converter PDF para imagens
images = convert_from_path("example.pdf", poppler_path="path/to/poppler/bin")

# Salvar as imagens
for i, img in enumerate(images):
    img.save(f"pagina_{i+1}.png", "PNG")
```

### Explicação
- **`convert_from_path`**: Converte cada página do PDF em uma imagem.
- **`poppler_path`**: Necessário no Windows para especificar o caminho do Poppler.

---

## Resumo
| Módulo       | Uso Principal            | Melhor Para                     |
|--------------|--------------------------|----------------------------------|
| Camelot      | Extrair tabelas          | PDFs com tabelas estruturadas   |
| PDFPlumber   | Texto, tabelas e imagens | Análise geral de PDFs           |
| Tabula-py    | Extrair tabelas          | Alternativa ao Camelot          |
| pdf2image    | Converter PDF para imagem| PDFs visualmente complexos      |
