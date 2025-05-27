## 🧰 1. Instalar o módulo PyPDF2

### 📌 No **Windows 10** ou **Ubuntu** (terminal / linha de comandos):

```bash
pip install PyPDF2
```

---

## 📚 2. O que é o PyPDF2?

O `PyPDF2` é um módulo em Python que permite **ler**, **escrever**, **dividir**, **juntar** e **extrair texto** de ficheiros PDF.

Ele funciona em múltiplas plataformas (Windows, Linux, macOS) e **não precisa do Adobe Reader**.

---

## 🧪 3. Exemplo prático completo

### Objetivo:

* Abrir um PDF
* Extrair texto da primeira página
* Dividir as páginas em ficheiros separados
* Juntar todas as páginas novamente num novo PDF

---

## 🗂️ Estrutura de pastas

Cria uma pasta com:

* Um ficheiro PDF de exemplo: `exemplo.pdf`
  (Podes criar um PDF qualquer com 2 ou mais páginas)
* Um script Python: `manipular_pdf.py`

---

## 🐍 4. Código completo (`manipular_pdf.py`)

```python
import os
from PyPDF2 import PdfReader, PdfWriter

# Caminho do PDF original
ficheiro_origem = "exemplo.pdf"

# Verifica se o ficheiro existe
if not os.path.exists(ficheiro_origem):
    print("Ficheiro PDF não encontrado.")
    exit()

# Lê o ficheiro PDF
leitor = PdfReader(ficheiro_origem)
total_paginas = len(leitor.pages)
print(f"Total de páginas no PDF: {total_paginas}")

# Extrai texto da primeira página
pagina = leitor.pages[0]
texto = pagina.extract_text()
print("\nTexto da primeira página:\n")
print(texto)

# Divide cada página em ficheiros separados
for i, pagina in enumerate(leitor.pages):
    escritor = PdfWriter()
    escritor.add_page(pagina)
    nome_ficheiro = f"pagina_{i + 1}.pdf"
    with open(nome_ficheiro, "wb") as f:
        escritor.write(f)
    print(f"Página {i + 1} gravada em: {nome_ficheiro}")

# Junta novamente todas as páginas num novo ficheiro
novo_pdf = PdfWriter()
for i in range(total_paginas):
    leitor_temp = PdfReader(f"pagina_{i + 1}.pdf")
    novo_pdf.add_page(leitor_temp.pages[0])

# Grava o PDF combinado
with open("novo_documento.pdf", "wb") as f:
    novo_pdf.write(f)

print("\nNovo PDF combinado criado: novo_documento.pdf")
```

---

## 🖥️ 5. Como executar

### No Windows 10:

1. Abre o **cmd** ou **PowerShell**
2. Vai até à pasta:

   ```bash
   cd caminho\para\a\pasta
   ```
3. Executa:

   ```bash
   python manipular_pdf.py
   ```

### No Ubuntu:

1. Abre o terminal
2. Vai até à pasta:

   ```bash
   cd /caminho/para/a/pasta
   ```
3. Executa:

   ```bash
   python3 manipular_pdf.py
   ```

---

## ✅ Resultados esperados

* Texto da primeira página impresso no terminal
* Novos ficheiros criados: `pagina_1.pdf`, `pagina_2.pdf`, etc.
* Um novo ficheiro combinado: `novo_documento.pdf`

---

## 🧠 Dicas úteis

| Função             | Descrição                  |
| ------------------ | -------------------------- |
| `PdfReader()`      | Lê PDFs existentes         |
| `PdfWriter()`      | Cria ou modifica PDFs      |
| `.pages[n]`        | Acede à página n           |
| `.extract_text()`  | Extrai texto de uma página |
| `.add_page()`      | Adiciona uma página        |
| `.write(ficheiro)` | Escreve o novo PDF         |
