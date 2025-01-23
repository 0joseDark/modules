### Desenvolvimento com PyPDF2 no Windows 10

O **PyPDF2** é uma biblioteca em Python para manipulação de ficheiros PDF. Ele permite ler, dividir, unir, rodar páginas e extrair texto de PDFs.

---

### **Instalação do PyPDF2**

1. Abra o terminal do Windows (PowerShell ou CMD).
2. Execute:
   ```bash
   pip install PyPDF2
   ```

---

### **Funcionalidades básicas do PyPDF2**

#### 1. **Ler e extrair texto de um PDF**
```python
import PyPDF2

def extrair_texto(caminho_pdf):
    with open(caminho_pdf, 'rb') as pdf_file:
        leitor = PyPDF2.PdfReader(pdf_file)
        texto = ""
        for pagina in leitor.pages:
            texto += pagina.extract_text()
        return texto

# Exemplo de uso
caminho = "exemplo.pdf"
texto_extraido = extrair_texto(caminho)
print(texto_extraido)
```

#### 2. **Dividir um PDF em páginas individuais**
```python
def dividir_pdf(caminho_pdf, pasta_saida):
    with open(caminho_pdf, 'rb') as pdf_file:
        leitor = PyPDF2.PdfReader(pdf_file)
        for i, pagina in enumerate(leitor.pages):
            escritor = PyPDF2.PdfWriter()
            escritor.add_page(pagina)
            with open(f"{pasta_saida}/pagina_{i+1}.pdf", 'wb') as pdf_saida:
                escritor.write(pdf_saida)

# Exemplo de uso
dividir_pdf("exemplo.pdf", "paginas_saida")
```

#### 3. **Unir múltiplos PDFs**
```python
def unir_pdfs(lista_pdfs, ficheiro_saida):
    escritor = PyPDF2.PdfWriter()
    for pdf in lista_pdfs:
        with open(pdf, 'rb') as pdf_file:
            leitor = PyPDF2.PdfReader(pdf_file)
            for pagina in leitor.pages:
                escritor.add_page(pagina)
    with open(ficheiro_saida, 'wb') as saida:
        escritor.write(saida)

# Exemplo de uso
unir_pdfs(["arquivo1.pdf", "arquivo2.pdf"], "unido.pdf")
```

---

### **Interface Gráfica para Extrair Frames de PDFs**
Vamos criar uma GUI para extrair cada página de um PDF como ficheiros individuais.

#### **Código Completo**
```python
import tkinter as tk
from tkinter import filedialog, messagebox
import PyPDF2
import os

def selecionar_pdf():
    caminho_pdf = filedialog.askopenfilename(filetypes=[("PDF files", "*.pdf")])
    if caminho_pdf:
        entrada_pdf.set(caminho_pdf)

def selecionar_pasta():
    pasta = filedialog.askdirectory()
    if pasta:
        pasta_saida.set(pasta)

def extrair_frames():
    pdf_caminho = entrada_pdf.get()
    pasta_destino = pasta_saida.get()

    if not pdf_caminho or not pasta_destino:
        messagebox.showerror("Erro", "Por favor, selecione o ficheiro PDF e a pasta de destino.")
        return

    try:
        with open(pdf_caminho, 'rb') as pdf_file:
            leitor = PyPDF2.PdfReader(pdf_file)
            for i, pagina in enumerate(leitor.pages):
                escritor = PyPDF2.PdfWriter()
                escritor.add_page(pagina)
                ficheiro_saida = os.path.join(pasta_destino, f"pagina_{i+1}.pdf")
                with open(ficheiro_saida, 'wb') as pdf_saida:
                    escritor.write(pdf_saida)
        messagebox.showinfo("Sucesso", "As páginas foram extraídas com sucesso.")
    except Exception as e:
        messagebox.showerror("Erro", f"Erro ao processar o PDF: {e}")

# Configuração da interface gráfica
janela = tk.Tk()
janela.title("Extrair Frames do PDF")
janela.geometry("400x200")

entrada_pdf = tk.StringVar()
pasta_saida = tk.StringVar()

tk.Label(janela, text="Ficheiro PDF:").pack(anchor="w", padx=10)
tk.Entry(janela, textvariable=entrada_pdf, width=50).pack(padx=10)
tk.Button(janela, text="Selecionar PDF", command=selecionar_pdf).pack(pady=5)

tk.Label(janela, text="Pasta de Destino:").pack(anchor="w", padx=10)
tk.Entry(janela, textvariable=pasta_saida, width=50).pack(padx=10)
tk.Button(janela, text="Selecionar Pasta", command=selecionar_pasta).pack(pady=5)

tk.Button(janela, text="Extrair Frames", command=extrair_frames).pack(pady=10)
tk.Button(janela, text="Sair", command=janela.quit).pack(pady=10)

janela.mainloop()
```

---

### **Funcionalidades do Programa**

1. **Selecionar o ficheiro PDF**: Use o botão para navegar e escolher um ficheiro PDF.
2. **Escolher a pasta de destino**: Indique onde salvar as páginas extraídas.
3. **Extrair Frames**: Clica no botão e cada página será salva como um ficheiro PDF individual na pasta escolhida.

---

### **Explicação Passo a Passo**

1. **Configuração do PyPDF2**: O módulo lê o ficheiro PDF e divide as páginas.
2. **Uso do tkinter**: 
   - Criamos uma interface para interação.
   - `filedialog` permite selecionar ficheiros e pastas.
   - `messagebox` exibe mensagens de erro ou sucesso.
3. **Lógica do programa**:
   - Carregar o ficheiro PDF.
   - Iterar pelas páginas.
   - Salvar cada página num ficheiro separado.

Este programa é útil para manipulação de PDFs em ambiente Windows.
